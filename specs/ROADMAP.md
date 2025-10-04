# Project Roadmap

High-level overview of specifications, their dependencies, and implementation status. This is the primary reference for understanding project scope and planning new work.

**Last Updated**: [Will be updated when first spec is added]

---

## Understanding Phases

**Phases represent dependency waves, not project stages.**

- **Phase N**: Contains specs that can be worked on in parallel (no dependencies on each other)
- **Phase N+1**: Contains specs that depend on work from Phase N
- Phases grow dynamically as new work is planned
- Multiple unrelated features can exist in the same phase if they're independent

**Example**: Phase 5 might contain a UI feature, backend cleanup, and telemetry work - all independent tasks happening in parallel.

---

## Phase 1

| Spec | Status | Priority | Dependencies | Description | Location | Effort |
|------|--------|----------|--------------|-------------|----------|--------|
| _No specs yet_ | | | | Use `/plan_feature` to add your first spec | | |

---

## Quick Reference

### Status Legend
- ✅ **Complete** - All success criteria met, merged
- 🚧 **In Progress** - Active development
- 📋 **Planned** - Spec created, ready when dependencies clear
- ⏸️ **Blocked** - Waiting on dependencies
- ❌ **Cancelled** - No longer needed

### Priority Levels
- **Critical** - Blocking other work, must complete first
- **High** - Important for milestone completion
- **Medium** - Nice to have, can be deferred
- **Low** - Optional enhancement

### Effort Estimates (Agentic Development)
- **Small** - ~1 hour (single feature, clear boundaries)
- **Medium** - ~2-3 hours (moderate complexity, some integration)
- **Large** - Should be decomposed into multiple smaller specs

**Note**: For agentic development, specs larger than Medium should be broken down into focused, independently deliverable units. If a feature feels Large, use `/plan_feature` to decompose it into 2-3 Small/Medium specs.

---

## Adding New Specs

When creating a new spec, add an entry to the appropriate phase:

1. Assign next available spec number
2. Set initial status (usually 📋 Planned)
3. Identify priority level
4. List any dependencies (other spec numbers)
5. Write brief description (one line)
6. Note spec location
7. Estimate effort
8. **Determine phase**:
   - If no dependencies or only depends on completed specs → Add to current active phase
   - If depends on in-progress specs → Calculate phase based on dependency chain
   - Create new phase sections as needed (Phase 2, Phase 3, etc.)

Use `/plan_feature` to analyze dependencies and suggest appropriate phase placement.
Use `/create_spec` to generate the actual specification files.
