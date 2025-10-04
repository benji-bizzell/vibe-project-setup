# Code Patterns

## Result Types

Always use neverthrow for operations that can fail. Never throw exceptions in business logic.

### Basic Usage
```typescript
import { ok, err, Result } from 'neverthrow';

const divide = (a: number, b: number): Result<number, Error> => {
  if (b === 0) return err(new Error('Division by zero'));
  return ok(a / b);
};

// Chain operations
const result = divide(10, 2)
  .andThen(value => ok(value * 2))
  .map(value => value + 1);
```

### Batch Operations
```typescript
import { combine } from 'neverthrow';

// Execute multiple operations, collect all errors if any fail
const operations = [fetchUser(id1), fetchUser(id2), fetchUser(id3)];
const results = await Promise.all(operations);
const combined = combine(results);

if (combined.isOk()) {
  // All succeeded
  combined.value.forEach(user => console.log(user.name));
} else {
  // Some failed - all errors available
  combined.error.forEach(err => console.error(err.message));
}
```

### Fallback Chains
```typescript
// Multi-level fallback with graceful degradation
const fetchWithFallback = async (id: string): Promise<Result<Data, never>> => {
  const primary = await fetchFromDB(id);
  if (primary.isOk()) return primary;

  const secondary = await fetchFromCache(id);
  if (secondary.isOk()) return secondary;

  return ok(createDefaultData(id)); // Always succeeds
};
```

### Side Effects
```typescript
// Perform side effects without breaking Result chains
const result = await fetchUser(id)
  .map(user => {
    console.log('User fetched:', user.name);
    metrics.record(user.id);
    return user;
  })
  .andThen(user => validateUser(user));
```

## Branded Types

Use branded types for all domain-specific IDs. Prevents ID mixing bugs at compile-time with zero runtime cost.

```typescript
// Define branded types
type UserId = string & { readonly __brand: 'UserId' };
type RequestId = string & { readonly __brand: 'RequestId' };
type OrderId = string & { readonly __brand: 'OrderId' };

// Create constructors
const createUserId = (id: string): UserId => id as UserId;
const createRequestId = (id: string): RequestId => id as RequestId;

// Type safety enforced at compile-time
function processRequest(requestId: RequestId, userId: UserId) { ... }

// ❌ Compile error - cannot swap types
processRequest(userId, requestId);

// ✅ Correct usage
processRequest(createRequestId('req_123'), createUserId('user_456'));
```

### Domain-Specific Keys
```typescript
type CacheKey = string & { readonly __brand: 'CacheKey' };

const createCacheKey = (domain: string, key: string): CacheKey =>
  `${domain}:${key}` as CacheKey;

const userCache = createCacheKey('users', userId);
const orderCache = createCacheKey('orders', orderId);
```

## Validation

Compose schemas, don't duplicate. Parse at boundaries with branded type transforms. All validation returns Result types.

```typescript
import { z } from 'zod';
import { ok, err, Result } from 'neverthrow';

// Define schema
const UserSchema = z.object({
  email: z.string().email(),
  name: z.string().min(1),
});

type User = z.infer<typeof UserSchema>;

// Use with Result types
const validateUser = (data: unknown): Result<User, ValidationError> => {
  const parsed = UserSchema.safeParse(data);
  return parsed.success
    ? ok(parsed.data)
    : err(new ValidationError(parsed.error));
};

// Chain validation
const result = await fetchRawData()
  .andThen(data => validateUser(data))
  .andThen(user => saveUser(user));
```

## Dependency Injection

Inject dependencies via context objects for testability.

```typescript
interface Context {
  db: Database;
  logger: Logger;
  cache: Cache;
}

const createUser = (
  ctx: Context,
  data: UserInput
): Result<User, Error> => {
  return validateUser(data)
    .andThen(user => saveToDb(ctx.db, user))
    .map(user => {
      ctx.logger.info('User created', user.id);
      return user;
    });
};

// Easy to test with mock context
const mockCtx = { db: mockDb, logger: mockLogger, cache: mockCache };
const result = createUser(mockCtx, userData);
```

## Pattern Matching

Use ts-pattern for complex conditionals (>3 branches). Provides exhaustive matching and better type inference than switch statements.

```typescript
import { match } from 'ts-pattern';

const handleResult = match(result)
  .with({ status: 'success' }, (r) => processSuccess(r.data))
  .with({ status: 'error', code: 404 }, () => handleNotFound())
  .with({ status: 'error', code: 500 }, () => handleServerError())
  .exhaustive(); // Compile error if cases not covered
```

## Testing Patterns

Test error paths as thoroughly as success paths. Use Result-based assertions.

```typescript
import { describe, it, expect } from 'vitest';

describe('divide', () => {
  it('should return Ok with valid division', () => {
    const result = divide(10, 2);
    expect(result.isOk()).toBe(true);
    if (result.isOk()) {
      expect(result.value).toBe(5);
    }
  });

  it('should return Err for division by zero', () => {
    const result = divide(10, 0);
    expect(result.isErr()).toBe(true);
    if (result.isErr()) {
      expect(result.error.message).toContain('Division by zero');
    }
  });
});

// Test Result chains
describe('user creation flow', () => {
  it('should handle validation errors', () => {
    const result = createUser(ctx, invalidData);
    expect(result.isErr()).toBe(true);
    result.mapErr(err => {
      expect(err).toBeInstanceOf(ValidationError);
    });
  });
});
```

## When to Use Each Pattern

**Result Types**: All operations that can fail
**Branded Types**: All domain-specific IDs, cache keys, validated strings
**Validation**: All external data at API boundaries
**Pattern Matching**: Complex conditionals with >3 branches
**Dependency Injection**: All services and handlers
**Batch Operations**: Parallel operations where all must succeed or collect all errors
**Fallback Chains**: Critical operations requiring graceful degradation

## Performance Notes

- Branded types: Zero runtime overhead (compile-time only)
- Result types: Minimal overhead, significant reliability gains
- Fallback chains: May increase latency but improve user experience
- Batch operations: Can reduce total execution time vs sequential

## See Also

- `tsdoc-standards.md` - Documentation requirements for public APIs
