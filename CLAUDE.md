# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Technology Stack

### Core Libraries
- **Validation**: Zod - all external data validation at boundaries
- **Error Handling**: neverthrow - ALL async operations return Result types
- **Testing**: Vitest - fast, modern test runner
- **Code Quality**: Biome - unified linting and formatting (single tool)
- **Type Utilities**: type-fest - advanced TypeScript utility types
- **Pattern Matching**: ts-pattern - exhaustive matching for complex conditionals

### Decision Rules
1. Validate ALL external data with Zod schemas at boundaries
2. Return Result types for ALL operations that can fail
3. Keep handlers pure - inject dependencies via context objects
4. Use Result types for comprehensive error testing
5. Document all public APIs with TSDoc

## Development Commands

### Core Development
- `npm run dev` - Start development server
- `npm run build` - Build for production

### Code Quality & Testing
- `npm run test` - Run all tests with Vitest
- `npm run test:watch` - Run tests in watch mode for development
- `npm run test:ui` - Run tests with interactive UI
- `npm run lint` - Lint with Biome (fast Rust-based linter)
- `npm run format` - Format with Biome (replaces Prettier)
- `npm run typecheck` - TypeScript with strictest possible settings
- `npm run check` - Complete validation pipeline (typecheck + biome + test)
- `npm run fix` - Auto-fix all linting and formatting issues

## Project Architecture

This project follows a TDD Spec-Driven Development approach with systematic planning and implementation phases.

### Directory Structure

```
project/
├── specs/                    # Technical specifications & checklists
│   ├── templates/           # Spec and checklist templates
│   └── {feature-name}/      # Feature-specific specs
├── src/                     # Source code
├── tests/                   # Test files
├── docs/                    # Documentation
│   ├── patterns.md         # Code patterns and conventions
│   └── tsdoc-standards.md  # Documentation standards
└── .claude/                # Claude Code configuration
    ├── agents/             # Custom agents
    ├── commands/           # Slash commands
    └── personal-preferences.md
```

## Development Philosophy

### Type Safety First
- Use strictest TypeScript settings (`noUncheckedIndexedAccess`, etc.)
- Return Result types for ALL operations that can fail
- Implement exhaustive switch statements with `assertNever`
- Apply branded types for domain-specific strings (e.g., UserId, RequestId)
- Use advanced neverthrow patterns for error recovery and batch operations

### Testing Strategy
- Test error paths as thoroughly as success paths
- Use Result-based error testing for comprehensive coverage
- Maintain >80% coverage for business logic, 100% for error paths
- Test advanced neverthrow patterns (combine, fallback, recovery chains)

### TDD Spec-Driven Workflow
- **Phase X.0**: Write comprehensive tests before any implementation
- **Phase X.1**: Implement functionality until all Phase X.0 tests pass
- Use hierarchical Functional Requirements (FR1.1, FR1.2, etc.)
- Separate Success Criteria into Automated vs Manual verification
- Track progress via checklist.md with status indicators (✅ 🚧 📋)

## Imports
@./docs/patterns.md
@./docs/tsdoc-standards.md
@./specs/CLAUDE.md
@./.claude/personal-preferences.md
