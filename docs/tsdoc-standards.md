# TSDoc Standards

## Required Documentation

### Public Functions
Must include:
- First line: Clear purpose statement
- `@param` - Explain beyond just the type, include validation rules
- `@returns` - What the value represents (Result<T, E> for fallible operations)
- `@throws` - All error conditions with {@link} (legacy functions only)
- `@example` - At least one usage example showing success AND error cases
- `@see` - Link to related error types and external libraries

### Complex Functions
Additional requirements:
- `@remarks` - Architecture decisions and constraints
- `@see` - Related functions/docs
- Performance implications in remarks

## Maturity Markers
- `@alpha` - Experimental, will change
- `@beta` - Testing, stabilizing
- `@public` - Stable API
- `@internal` - Not for public use
- `@deprecated` - Include migration path

## Examples Required For
- Error handling patterns
- Async operations
- Complex business logic
- Validation schemas

## Result Types Documentation
- Document Result<T, E> return types explicitly in `@returns`
- `@example` must show both Ok and Err handling patterns
- Use `@see` to link related error types and recovery patterns
- Include performance implications in `@remarks` for async operations

## Example
```typescript
/**
 * Validates user input and creates a new user account.
 *
 * @param input - Raw user input data from API request
 * @returns Result containing validated User object or ValidationError
 *
 * @example
 * ```typescript
 * const result = await createUser({ email: 'test@example.com', name: 'Test' });
 * result.match(
 *   (user) => console.log('User created:', user.id),
 *   (error) => console.error('Validation failed:', error.message)
 * );
 * ```
 *
 * @see {@link ValidationError} for error details
 * @public
 */
export const createUser = (input: unknown): Result<User, ValidationError> => {
  // Implementation
};
```

## Anti-patterns
- Don't document obvious types
- Don't repeat parameter names
- Don't write "Gets X" for getX()
- Don't skip `@throws` for legacy functions
- Don't document internal helper functions unless `@public`

## Team Notes
Use `@privateRemarks` for:
- TODOs with issue numbers
- Performance measurements
- Temporary workarounds
- Architecture debt
