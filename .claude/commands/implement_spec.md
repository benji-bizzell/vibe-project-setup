# Implement Specification

You are tasked with implementing an approved technical specification from `specs/`. These specs contain Functional Requirements (FRs) with Phase X.0 → X.1 test-driven development structure and specific success criteria.

## Usage

```
/implement_spec {spec-path}
```

**Examples:**
- `/implement_spec specs/user-authentication/spec.md`
- `/implement_spec specs/data-export/spec.md`
- `/implement_spec specs/real-time-notifications/spec.md`

## Getting Started

When given a spec path:
- Read the spec.md and checklist.md completely
- Read the original requirements and all files mentioned in the spec
- **Read files fully** - never use limit/offset parameters, you need complete context
- Think deeply about how project patterns fit together (Result types, neverthrow, validation)
- Create a todo list to track your progress through the checklist phases
- Start implementing if you understand what needs to be done

If no spec path provided, respond with:
```
I'll help you implement a technical specification using the spec-driven workflow.

Please provide the spec path, for example:
- `/implement_spec specs/user-authentication/spec.md`
- `/implement_spec specs/data-export/spec.md`

I'll read the spec and checklist, then begin the Phase X.0 → X.1 implementation process.
```

## Process

This command follows a systematic implementation approach for spec-driven development.

## Implementation Philosophy

Specs are carefully designed using project patterns, but reality can be messy. Your job is to:
- **Always start with Phase X.0 (Test Foundation)** - comprehensive test creation first
- **Only proceed to Phase X.1 (Implementation)** after all Phase X.0 tests are written and failing
- Follow the spec's Functional Requirements while adapting to what you find
- Implement each phase fully before moving to the next
- Verify your work uses project patterns (Result types, neverthrow, branded types)
- Update checkboxes in the checklist.md as you complete tasks

## Test-Driven Development Approach

This is **critical** for spec-driven implementation:

### Phase X.0: Test Foundation (ALWAYS FIRST)
1. **Read the spec's Functional Requirements completely**
2. **Create comprehensive tests covering ALL FRs for this phase**:
   - Unit tests for core functionality
   - Integration tests for system interactions
   - Error path tests using Result types
   - Edge case coverage as specified in Success Criteria
3. **Verify all tests fail appropriately** (Red phase of Red-Green-Refactor)
4. **Only mark Phase X.0 complete when test foundation is solid**

### Phase X.1: Implementation (ONLY AFTER X.0)
1. **Implement functionality until all Phase X.0 tests pass** (Green phase)
2. **Use project patterns consistently**:
   - Result types for all operations that can fail
   - neverthrow for error handling and composition
   - Branded types for domain-specific IDs
   - Zod validation at all boundaries
   - Dependency injection via context objects
3. **Refactor for clarity while keeping tests green**
4. **Run Success Criteria verification**

When Phase structure doesn't match reality:
- STOP and think deeply about why the spec can't be followed
- Present the issue clearly:
  ```
  Issue in Phase [X.Y]:
  Expected: [what the spec says]
  Found: [actual codebase situation]
  Why this matters: [explanation with file:line references]

  How should I proceed?
  ```

## Project Implementation Guidelines

### Always Use These Patterns:
- **Result Types**: `Result<T, E>` for all operations that can fail
- **neverthrow**: `.andThen()`, `.mapErr()`, `.match()` for error handling
- **Branded Types**: Domain-specific IDs with utility functions
- **Zod Validation**: Parse all external data with proper schemas
- **Context Injection**: Pass dependencies via context objects
- **TSDoc**: Document all public APIs with proper examples

## Verification Approach

After implementing a phase:

### Automated Verification (Run These):
- `npm run test` - All tests must pass
- `npm run typecheck` - Strict TypeScript validation
- `npm run lint` - Biome linting
- `npm run check` - Complete validation pipeline

### Manual Verification:
- Test functionality in development environment
- Verify error handling works as expected
- Check performance under realistic conditions
- Validate edge cases match Success Criteria

### Progress Tracking:
- Update checklist.md with completed tasks immediately
- Mark items as ✅ (completed), 🚧 (in progress), 📋 (pending)
- Update progress percentages and status summaries
- Reference specific file:line numbers in progress notes

## Checklist Management

### Real-Time Updates:
```markdown
## Phase 1: Feature Implementation

### Phase 1.0: Test Foundation ✅
- [x] Create feature tests
- [x] Write error handling tests
- [x] Verify all tests fail appropriately

### Phase 1.1: Implementation 🚧
- [x] Implement core functionality
- [ ] Add error handling with Result types
- [ ] Verify all Phase 1.0 tests pass
```

### Status Tracking:
- Update **Current Status Summary** section with:
  - Current phase and progress percentage
  - Next immediate tasks
  - Any blockers or decisions needed
  - File:line references for work in progress

## If You Encounter Issues

### When Code Doesn't Match Spec:
1. **First**, make sure you've read all the relevant code completely
2. **Consider** if the codebase has evolved since the spec was written
3. **Check** if existing patterns provide better approaches
4. **Present the mismatch clearly** with file:line references and ask for guidance

### When Tests Are Unclear:
1. **Research existing test patterns** in the codebase
2. **Look at similar features** for testing approaches
3. **Use Result types consistently** in test expectations
4. **Ask specific questions** about testing strategy

Use specialized agents sparingly - mainly for:
- **codebase-analyzer** agent: Understanding complex existing implementations
- **test-pattern-finder** agent: Discovering testing approaches for unfamiliar areas
- **spec-locator** agent: Finding similar implementations for reference

You can spawn these agents concurrently for comprehensive research when needed.

## Resuming Work

If the checklist has existing checkmarks:
- **Trust that completed Phase X.0 work is done** (tests are written)
- **Pick up from the first unchecked item** in current phase
- **Verify previous work only if something seems off**
- **Always run tests** to ensure previous work is still valid

The implement_spec command supports resuming work from any point in the checklist by reading the current state and continuing from the next uncompleted task.

### Context Recovery:
1. **Read Current Status Summary** in checklist.md
2. **Check Session Recovery Context** for last working details
3. **Run existing tests** to understand current state
4. **Review recent file:line references** for context

## Success Criteria Validation

### After Each Phase:
1. **Run all Automated Verification steps** from spec Success Criteria
2. **Perform Manual Verification steps** as specified
3. **Update Progress sections** in checklist.md
4. **Mark phase complete** only when all criteria met

### Final Implementation:
1. **All Functional Requirements addressed** with file:line references
2. **All Success Criteria met** (both automated and manual)
3. **Project patterns used consistently** throughout
4. **Documentation updated** with proper TSDoc
5. **No regressions** in existing functionality

## Key Command Reference

Quick access to essential development commands:
```bash
# Core development
npm run dev              # Start development server
npm run build            # Build for production

# Code quality & testing
npm run test             # Run all tests
npm run test:watch       # Test in watch mode
npm run typecheck        # TypeScript validation
npm run lint             # Biome linting
npm run check            # Complete validation pipeline
npm run fix              # Auto-fix linting issues
```

## Implementation Flow Summary

1. **Read spec.md and checklist.md completely**
2. **Create TodoWrite list** from checklist phases
3. **Phase X.0: Write ALL tests first** (Red phase)
   - Verify tests fail appropriately
   - Mark Phase X.0 complete in checklist
4. **Phase X.1: Implement until tests pass** (Green phase)
   - Use project patterns consistently
   - Update checklist progress in real-time
   - Run Success Criteria validation
5. **Move to next phase** or mark spec complete

Remember: You're implementing a spec-driven solution with test-first methodology. Keep the Functional Requirements and Success Criteria in mind and maintain forward momentum through the Phase X.0 → X.1 structure.
