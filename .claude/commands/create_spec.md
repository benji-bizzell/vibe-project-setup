# Create Specification

You are tasked with creating comprehensive technical specifications through an interactive, iterative process. You should be thorough and work collaboratively with the user to produce high-quality spec-driven development documents.

## Usage

```
/create_spec {feature-name} [description]
```

**Examples:**
- `/create_spec user-authentication "Add JWT-based user authentication"`
- `/create_spec data-export "Implement CSV and JSON data export functionality"`
- `/create_spec real-time-notifications "Add WebSocket-based real-time notifications"`

## Initial Response

When this command is invoked:

1. **Check if parameters were provided**:
   - If a feature name or description was provided as a parameter, skip the default message
   - Begin the research process immediately
   - Use provided feature name for spec directory creation

2. **If no parameters provided**, respond with:
```
I'll help you create a detailed technical specification for the spec-driven workflow.

Please provide:
1. The feature name (will become the directory name in specs/)
2. Feature description or requirements
3. Any relevant context, constraints, or specific requirements
4. Links to related research or previous implementations

I'll analyze this information and work with you to create a comprehensive spec.

Tip: You can also invoke this command directly: `/create_spec user-auth "Add JWT-based authentication"`
```

Then wait for the user's input.

## Process Steps

### Step 1: Context Gathering & Initial Analysis

1. **Spawn initial research tasks to gather context**:
   Before asking the user any questions, use specialized agents to research in parallel:

   - Use the **codebase-locator** agent to find all files related to the feature/task
   - Use the **codebase-analyzer** agent to understand current implementation patterns
   - Use the **spec-locator** agent to find existing specs and patterns to follow
   - Use the **test-pattern-finder** agent to research testing approaches for Phase X.0

   These agents will:
   - Find relevant source files, configs, and tests
   - Identify project-specific patterns (Result types, neverthrow, validation)
   - Trace data flow and key functions with file:line references
   - Discover existing spec templates and successful patterns

2. **Read all files identified by research tasks**:
   - After research tasks complete, read ALL files they identified as relevant
   - Focus on existing specs in specs/ folder for pattern consistency
   - Read template files: `specs/templates/spec-template.md` and `specs/templates/checklist-template.md`

3. **Analyze and verify understanding**:
   - Cross-reference requirements with actual codebase patterns
   - Identify existing similar implementations to build upon
   - Note project-specific constraints and patterns
   - Determine true scope based on codebase reality

4. **Present informed understanding and focused questions**:
   ```
   Based on my research of the codebase, I understand we need to [accurate summary].

   I've found that:
   - [Current implementation detail with file:line reference]
   - [Relevant pattern discovered (Result types, neverthrow, etc.)]
   - [Constraint or optimization opportunity]

   Questions that my research couldn't answer:
   - [Specific technical question that requires human judgment]
   - [Business logic clarification]
   - [Design preference that affects implementation]
   ```

   Only ask questions that you genuinely cannot answer through code investigation.

### Step 2: Research & Discovery

After getting initial clarifications:

1. **Create a research todo list** using TodoWrite to track exploration tasks

2. **Spawn parallel sub-tasks for comprehensive research**:
   - Use **codebase-locator** - To find more specific files related to the feature
   - Use **codebase-analyzer** - To understand implementation details and patterns
   - Use **spec-locator** - To find similar specs we can model after
   - Use **test-pattern-finder** - To discover testing approaches for comprehensive Phase X.0

3. **Wait for ALL sub-tasks to complete** before proceeding

4. **Present findings and design options**:
   ```
   Based on my research, here's what I found:

   **Current State:**
   - [Key discovery about existing code]
   - [Pattern or convention to follow (neverthrow, Result types, etc.)]

   **Design Options:**
   1. [Option A] - [pros/cons with context]
   2. [Option B] - [pros/cons with considerations]

   **Phase Structure:**
   - Phase X.0: [Test foundation approach]
   - Phase X.1: [Implementation approach]

   Which approach aligns best with your vision?
   ```

### Step 3: Spec Structure Development

Once aligned on approach:

1. **Create initial spec outline**:
   ```
   Here's my proposed spec structure for specs/{feature-name}/

   ## Overview
   [1-2 sentence summary]

   ## Functional Requirements:
   - FR1: [High-level requirement]
     - FR1.1: [Specific sub-requirement]
     - FR1.2: [Another sub-requirement]
   - FR2: [Another high-level requirement]

   ## Implementation Phases:
   - Phase 1.0: [Test Foundation] - [what tests to create]
   - Phase 1.1: [Implementation] - [what to build]

   Does this structure make sense? Should I adjust the FRs or phasing?
   ```

2. **Get feedback on structure** before writing details

### Step 4: Detailed Spec Writing

After structure approval:

1. **Create the spec directory**: `mkdir -p specs/{feature-name}`

2. **Generate and write the spec** to `specs/{feature-name}/spec.md` using the template

3. **Write the checklist** to `specs/{feature-name}/checklist.md` using the template

### Step 5: Spec Review and Finalization

1. **Present the draft spec location**:
   ```
   I've created the technical specification at:
   - `specs/{feature-name}/spec.md` - Complete technical specification
   - `specs/{feature-name}/checklist.md` - Implementation progress tracking

   Please review and let me know:
   - Are the Functional Requirements comprehensive?
   - Are the Success Criteria measurable and specific?
   - Does the Phase structure make sense for test-driven development?
   - Any technical details that need adjustment?
   ```

2. **Iterate based on feedback** - be ready to:
   - Refine Functional Requirements hierarchy
   - Adjust Phase structure and Success Criteria
   - Add/remove scope items
   - Clarify technical architecture details

3. **Continue refining** until the user is satisfied

## Important Guidelines

1. **Be Spec-Focused**:
   - Use existing project patterns (Result types, neverthrow, branded types)
   - Follow best practices and conventions
   - Respect test-driven Phase X.0 → X.1 methodology
   - Include specific file:line references for patterns

2. **Be Interactive**:
   - Don't write the full spec in one shot
   - Get buy-in at each major step
   - Allow course corrections
   - Work collaboratively

3. **Be Thorough**:
   - Research actual code patterns using parallel sub-tasks
   - Include specific file paths and line numbers
   - Write measurable success criteria with clear automated vs manual distinction
   - Use hierarchical FR numbering (FR1.1, FR1.2, etc.)

4. **Be Test-Driven**:
   - Always structure as Phase X.0 (Test Foundation) → Phase X.1 (Implementation)
   - Phase X.0 must create comprehensive failing tests
   - Phase X.1 implements until all Phase X.0 tests pass
   - Success criteria must be verifiable

5. **Track Progress**:
   - Use TodoWrite to track planning tasks
   - Update todos as you complete research
   - Mark planning tasks complete when done

6. **No Open Questions in Final Spec**:
   - Resolve all technical uncertainties before finalizing
   - Every FR must be clear and actionable
   - Success criteria must be measurable
   - Technical architecture must be specific

## Success Criteria Guidelines

**Always separate success criteria into two categories:**

1. **Automated Verification** (can be run by CI/CD):
   - `npm run test`, `npm run typecheck`, `npm run lint`
   - Specific files that should exist
   - API endpoints that should respond correctly

2. **Manual Verification** (requires human testing):
   - Feature functionality in browser/UI
   - Performance under realistic conditions
   - Edge cases and error handling
   - User experience validation
