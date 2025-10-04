# Project Roadmap

High-level overview of specifications, their dependencies, and implementation status. This is the primary reference for understanding project scope and planning new work.

**Last Updated**: [Date]

---

## Phase 1: Foundation

| Spec | Status | Priority | Dependencies | Description | Location | Effort |
|------|--------|----------|--------------|-------------|----------|--------|
| 001 | 🚧 In Progress | Critical | None | Core authentication and user management | `specs/001-auth/` | Large |
| 002 | 📋 Planned | Critical | None | Database schema and migrations | `specs/002-database/` | Medium |
| 004 | 📋 Planned | Low | None | Development tooling and scripts | `specs/004-tooling/` | Small |

---

## Phase 2: Core Features

| Spec | Status | Priority | Dependencies | Description | Location | Effort |
|------|--------|----------|--------------|-------------|----------|--------|
| 003 | ⏸️ Blocked | High | 001, 002 | User profile management with authentication | `specs/003-profiles/` | Medium |
| 005 | 📋 Planned | High | 002 | Data export functionality (CSV, JSON) | `specs/005-export/` | Small |

---

## Phase 3: Enhancements

| Spec | Status | Priority | Dependencies | Description | Location | Effort |
|------|--------|----------|--------------|-------------|----------|--------|
| 006 | 📋 Planned | Medium | 003 | Real-time notifications | `specs/006-notifications/` | Large |

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

### Effort Estimates
- **Small** - 1-3 days
- **Medium** - 4-7 days
- **Large** - 1-2 weeks
- **XL** - 2+ weeks

---

## Adding New Specs

When creating a new spec, add an entry to the appropriate phase table:

1. Assign next available spec number
2. Set initial status (usually 📋 Planned)
3. Identify priority level
4. List any dependencies (other spec numbers)
5. Write brief description (one line)
6. Note spec location
7. Estimate effort

Use `/create_spec` to generate the actual specification files.
