# Specs Folder - Claude Code Usage Guide

This document explains the structure, purpose, and usage of the `/specs` folder for LLM-assisted development.

## Overview

The `/specs` folder contains feature specifications and progress tracking for systematic development work. Each spec folder represents a distinct deliverable with its own implementation cycle.

## Folder Structure

```
specs/
├── CLAUDE.md                    # This usage guide
├── templates/
│   ├── spec-template.md         # Base specification template
│   └── checklist-template.md    # Base checklist template
└── {feature-name}/              # Individual feature folders
    ├── spec.md                  # Technical specification
    └── checklist.md             # Implementation progress tracking
```

## Document Purposes

### Spec (spec.md)
**Primary Purpose**: The authoritative source of truth for feature requirements and technical design.

**LLM Usage**: This is the guiding document that ensures all generated code aligns with intended behavior. Claude should reference this extensively during implementation.

**Content Focus**:
- Functional requirements with hierarchical numbering
- Success criteria with automated/manual verification split
- Current state analysis with codebase discoveries
- Technical architecture and implementation approach
- Explicit scope boundaries ("What We're NOT Doing")

### Checklist (checklist.md)
**Primary Purpose**: Granular progress tracking for session recovery and context maintenance.

**LLM Usage**: Updated continuously during implementation to track completed tasks, current status, and next steps. Essential for maintaining context across multiple coding sessions.

**Content Focus**:
- Phase-based task organization with completion status
- Progress percentages and status indicators
- Quick reference commands for development workflow
- Session recovery information and context preservation

## Usage Workflow

### 1. Creating New Specs
```bash
# Create new feature folder
mkdir specs/{feature-name}

# Copy templates and customize
cp specs/templates/spec-template.md specs/{feature-name}/spec.md
cp specs/templates/checklist-template.md specs/{feature-name}/checklist.md
```

### 2. Spec Development Process
1. **Research Phase**: Analyze current codebase state and constraints
2. **Requirements Definition**: Define FRs with hierarchical numbering (FR1.1, FR1.2...)
3. **Success Criteria**: Split into automated (command-runnable) and manual verification
4. **Architecture Design**: Technical approach with specific file/code references
5. **Scope Boundaries**: Explicit "What We're NOT Doing" section

### 3. Implementation Tracking
1. **Initialize Checklist**: Break spec into granular, trackable tasks
2. **Progress Updates**: Mark tasks as in_progress → completed during development
3. **Session Context**: Use checklist for resuming work after interruptions
4. **Status Communication**: Clear progress indicators for stakeholder visibility

### 4. Claude Integration Points

**During Planning**:
- Claude should read the spec completely before starting implementation
- Use spec's "Current State Analysis" to understand existing codebase
- Reference "What We're NOT Doing" to avoid scope creep
- Follow technical architecture decisions outlined in spec

**During Implementation (Test-Driven Development)**:
- **Always start with Phase X.0** (Test Foundation) before any implementation code
- Write comprehensive tests covering all FR requirements for the phase
- Ensure all tests fail appropriately (Red phase of Red-Green-Refactor)
- Only proceed to Phase X.1 (Implementation) once test foundation is complete
- Implement functionality until all Phase X.0 tests pass (Green phase)
- Update checklist continuously with task progress
- Cross-reference implementations against FR requirements
- Verify work against both automated and manual success criteria

**TDD Testing Best Practices**:
- **String matching precision**: Use partial matches for substring searches to avoid false negatives
- **Test assertion syntax**: Use proper expect syntax patterns
- **Mock data fidelity**: Test fixtures must accurately replicate actual patterns
- **Template consistency**: When tests validate against templates, ensure mock data matches structure

**During Validation**:
- Run automated verification commands from success criteria
- Guide manual testing based on success criteria definitions
- Ensure all FR requirements have been addressed
- Update checklist with final completion status

## Template Customization Guidelines

### Spec Template
- **Must-Have Sections**: Overview, Current State Analysis, Functional Requirements, Success Criteria, What We're NOT Doing
- **Optional Sections**: Risk Register (for complex features), Migration Notes (for refactoring), Performance Considerations
- **Customization**: Adjust Implementation Phases based on feature complexity

### Checklist Template
- **Must-Have Sections**: Phase organization, Progress tracking, Status summary, Quick commands
- **Optional Sections**: Migration guidelines (for complex changes), Team notes (for collaborative work)
- **Customization**: Break phases into appropriate granularity for the specific feature

## Best Practices

### For Specifications
1. **Research First**: Always analyze current codebase before writing requirements
2. **Measurable Criteria**: Success criteria should be specific and verifiable
3. **Clear Boundaries**: Explicit scope definition prevents feature creep
4. **Technical Depth**: Include specific file paths, code patterns, and architectural decisions
5. **No Open Questions**: All technical uncertainties must be resolved before finalization
6. **Test-Driven Structure**: Use Phase X.0 → Phase X.1 pattern for systematic development

### For Checklists
1. **Granular Tasks**: Break work into small, trackable units
2. **Real-time Updates**: Mark progress immediately when tasks complete
3. **Context Preservation**: Include enough detail for session recovery
4. **Status Visibility**: Use clear indicators (✅, 🚧, 📋) for quick assessment
5. **Command References**: Include relevant development commands for quick access

## Integration with Development Workflow

### Branch Management
- Spec folders typically align with feature branch names
- Specs should be created before significant implementation begins
- Checklist serves as branch-specific progress documentation

### Testing Integration
- Success criteria should reference actual test commands from the codebase
- Automated verification steps should be runnable without modification
- Manual verification should provide clear, actionable testing steps

### Code Review Process
- Specs provide context for code review discussions
- Checklists demonstrate systematic approach to requirements fulfillment
- FR traceability helps ensure complete feature implementation

## Anti-Patterns to Avoid

### Specification Issues
- Vague or unmeasurable success criteria
- Missing current state analysis
- Undefined scope boundaries
- Technical decisions left unresolved

### Checklist Issues
- Tasks too large or vague to track meaningfully
- Infrequent updates leading to stale progress information
- Missing context for session recovery
- No clear completion criteria

---

**Note**: This specs system is optimized for LLM-assisted development where systematic planning and context preservation are essential for consistent, high-quality implementation.
