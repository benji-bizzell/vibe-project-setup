# Vibe Project Template

A Claude Code project template featuring TDD Spec-Driven Development with systematic planning and implementation phases.

## Features

- **TDD Spec-Driven Workflow**: Phase X.0 (Test Foundation) → Phase X.1 (Implementation)
- **Strict TypeScript**: Strictest possible settings for maximum type safety
- **Modern Tooling**: Biome (unified linting/formatting), Vitest (testing)
- **Result Types**: neverthrow for comprehensive error handling
- **Validation**: Zod for all external data validation
- **Pattern Matching**: ts-pattern for complex conditionals
- **Documentation Standards**: TSDoc for all public APIs

## Quick Start

```bash
# Install dependencies
npm install

# Run tests
npm test

# Run tests in watch mode
npm run test:watch

# Type check
npm run typecheck

# Lint and format
npm run lint
npm run format

# Complete validation pipeline
npm run check

# Auto-fix issues
npm run fix
```

## Project Structure

```
project/
├── .claude/              # Claude Code configuration
│   ├── agents/          # Custom agents (codebase-analyzer, spec-locator, etc.)
│   ├── commands/        # Slash commands (/create_spec, /implement_spec)
│   └── personal-preferences.md
├── specs/               # TDD Spec-Driven Development
│   ├── templates/       # spec-template.md, checklist-template.md
│   ├── CLAUDE.md        # Usage guide
│   └── {feature}/       # Feature-specific specs (spec.md + checklist.md)
├── docs/                # Architecture & patterns documentation
│   ├── patterns.md      # Code patterns and conventions
│   └── tsdoc-standards.md # Documentation standards
├── src/                 # Source code
├── tests/               # Test files
├── CLAUDE.md           # Main Claude Code instructions
├── biome.json          # Linting/formatting config
├── tsconfig.json       # TypeScript config
└── vitest.config.ts    # Test configuration
```

## Development Workflow

### Starting a Session

1. **Prime the project context** using `/prime`:
   ```
   /prime
   ```
   This loads CLAUDE.md, ROADMAP.md, and shows current status.

### Creating a New Feature

2. **Create a Spec** using `/create_spec`:
   ```
   /create_spec user-authentication "Add JWT-based authentication"
   ```
   This creates:
   - `specs/user-authentication/spec.md` - Technical specification
   - `specs/user-authentication/checklist.md` - Progress tracking

2. **Implement the Spec** using `/implement_spec`:
   ```
   /implement_spec specs/user-authentication/spec.md
   ```
   This follows the TDD workflow:
   - **Phase X.0**: Write comprehensive tests first (Red phase)
   - **Phase X.1**: Implement until tests pass (Green phase)

### Custom Claude Code Commands

- `/prime` - Load essential project context (run first!)
- `/create_spec {feature-name}` - Create a new technical specification
- `/implement_spec {spec-path}` - Implement an approved specification
- `/plan_feature {description}` - Map feature requests to roadmap

### Custom Claude Code Agents

- **codebase-analyzer** - Analyzes implementation patterns and code quality
- **spec-locator** - Discovers and analyzes existing specifications
- **test-pattern-finder** - Finds testing patterns and best practices
- **codebase-locator** - Locates relevant files and code sections

## Core Patterns

### Result Types
All operations that can fail return `Result<T, E>` using neverthrow:

```typescript
import { ok, err, Result } from 'neverthrow';

const divide = (a: number, b: number): Result<number, Error> => {
  if (b === 0) return err(new Error('Division by zero'));
  return ok(a / b);
};
```

### Branded Types
Domain-specific IDs with compile-time safety:

```typescript
type UserId = string & { readonly __brand: 'UserId' };
const createUserId = (id: string): UserId => id as UserId;
```

### Validation with Zod
All external data validated at boundaries:

```typescript
import { z } from 'zod';

const UserSchema = z.object({
  email: z.string().email(),
  name: z.string().min(1),
});

type User = z.infer<typeof UserSchema>;
```

### Dependency Injection
Dependencies injected via context objects:

```typescript
interface Context {
  db: Database;
  logger: Logger;
}

const createUser = (ctx: Context, data: UserInput): Result<User, Error> => {
  // Implementation uses ctx.db and ctx.logger
};
```

## Documentation

- `CLAUDE.md` - Main development guide for Claude Code
- `specs/CLAUDE.md` - Specs folder usage guide
- `docs/patterns.md` - Code patterns and conventions
- `docs/tsdoc-standards.md` - Documentation standards

## Tech Stack

- **TypeScript** - Strict type safety
- **Biome** - Unified linting and formatting
- **Vitest** - Fast, modern test runner
- **neverthrow** - Result types for error handling
- **Zod** - Schema validation
- **ts-pattern** - Pattern matching
- **type-fest** - Advanced TypeScript utilities

## License

ISC
