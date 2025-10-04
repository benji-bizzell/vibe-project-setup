# Plan Feature

Analyzes a high-level feature request and maps it to the project roadmap, identifying dependencies, blockers, and optimal implementation sequence.

## Usage

```
/plan_feature {feature-description}
```

**Examples:**
- `/plan_feature "Add real-time collaboration with WebSockets"`
- `/plan_feature "Implement PDF export with custom templates"`
- `/plan_feature "Add OAuth2 integration for GitHub and Google"`

## Process

When this command is invoked:

### Step 1: Analyze Current State

1. **Read ROADMAP.md** to understand existing specs and phases
2. **Read relevant spec files** to understand current capabilities
3. **Identify patterns** in existing specs for similar features

### Step 2: Break Down Feature Request

1. **Decompose the feature** into logical spec units:
   - What are the distinct deliverables?
   - What's the minimal viable first step?
   - What are the enhancement layers?

2. **Identify dependencies** on existing specs:
   - Does this need authentication? (Check for auth spec)
   - Does this need database? (Check for data layer spec)
   - Does this extend existing features? (Check related specs)

3. **Check for blockers**:
   - Are required foundation specs complete?
   - Are there gaps in existing specs that need to be filled first?

### Step 3: Propose Roadmap Updates

Present a structured plan:

```
## Feature Analysis: [Feature Name]

### Proposed Specs

**Spec XXX: [First Deliverable Name]**
- **Phase**: [1/2/3/etc.]
- **Priority**: [Critical/High/Medium/Low]
- **Dependencies**: [Spec numbers or "None"]
- **Description**: [One line description]
- **Effort Estimate**: [Small/Medium/Large/XL]
- **Rationale**: Why this needs to be a separate spec

**Spec YYY: [Second Deliverable Name]**
- **Phase**: [1/2/3/etc.]
- **Priority**: [Critical/High/Medium/Low]
- **Dependencies**: [Including XXX if needed]
- **Description**: [One line description]
- **Effort Estimate**: [Small/Medium/Large/XL]
- **Rationale**: Why this builds on previous spec

### Dependency Analysis

**Required Specs (Must be complete first)**:
- Spec 001: [Name] - Status: [✅/🚧/📋] - Why needed: [Explanation]
- Spec 002: [Name] - Status: [✅/🚧/📋] - Why needed: [Explanation]

**Blocked By**:
- [List any incomplete required specs]

**Can Start When**:
- [Clear conditions for when this work can begin]

### Implementation Sequence

1. **Immediate**: [What can start now if anything]
2. **Next**: [What needs to wait and why]
3. **Future**: [Enhancement layers]

### Parallel Work Opportunities

This feature [can/cannot] be developed in parallel with:
- Spec XXX: [Name] - Why: [Explanation]
- Spec YYY: [Name] - Why: [Explanation]

### Roadmap Integration

**Add to Phase [X]**:
[Table row format for easy copy-paste into ROADMAP.md]

| Spec | Status | Priority | Dependencies | Description | Location | Effort |
|------|--------|----------|--------------|-------------|----------|--------|
| XXX | 📋 Planned | [Priority] | [Deps] | [Description] | `specs/XXX-name/` | [Effort] |
```

### Step 4: Interactive Refinement

Ask clarifying questions if needed:
- "Should this be split into more granular specs?"
- "What's the priority relative to existing planned work?"
- "Are there any constraints I haven't considered?"

### Step 5: Update Roadmap (Optional)

If user approves:
1. Assign next available spec numbers
2. Add entries to appropriate phase in ROADMAP.md
3. Update "Last Updated" date
4. Suggest next steps (usually `/create_spec` for each proposed spec)

## Guidelines

### Spec Granularity
- Each spec should be independently testable
- Prefer smaller, focused specs over large multi-purpose ones
- If effort estimate is XL, consider splitting

### Dependency Detection
- Authentication/authorization needs
- Data persistence needs
- External API integrations
- Infrastructure requirements
- UI/UX dependencies

### Priority Assignment Rules
- **Critical**: Blocks multiple other specs, foundation work
- **High**: Needed for milestone completion, high user value
- **Medium**: Nice to have, can be deferred one cycle
- **Low**: Optional enhancement, technical debt reduction

### Phase Assignment
- **Phase 1**: Foundation work, no dependencies
- **Phase 2**: Core features, depends on Phase 1
- **Phase 3+**: Enhancements, depends on Phase 2

## Example Interaction

```
User: /plan_feature "Add email notifications for system events"

Agent:
## Feature Analysis: Email Notifications

I've analyzed the current roadmap and identified that this feature needs:

### Proposed Specs

**Spec 007: Email Service Integration**
- **Phase**: 2 (depends on database)
- **Priority**: High
- **Dependencies**: 002 (Database)
- **Description**: Email service provider integration and template system
- **Effort Estimate**: Medium
- **Rationale**: Foundation for all email functionality

**Spec 008: Event-Triggered Notifications**
- **Phase**: 3
- **Priority**: Medium
- **Dependencies**: 007, 003 (User Profiles)
- **Description**: Subscribe to system events and trigger emails
- **Effort Estimate**: Small
- **Rationale**: Builds on email service with event subscriptions

### Dependency Analysis

**Required Specs**:
- Spec 002: Database - Status: 📋 Planned - Why: Need to store email templates and logs
- Spec 003: User Profiles - Status: ⏸️ Blocked - Why: Need user email preferences

**Blocked By**: Spec 002 (Database) must complete first

**Can Start When**: Database spec (002) reaches Phase 2.1 (Implementation)

### Roadmap Integration

Add to ROADMAP.md:

**Phase 2 table** (after Spec 005):
| 007 | 📋 Planned | High | 002 | Email service provider integration | `specs/007-email/` | Medium |

**Phase 3 table**:
| 008 | 📋 Planned | Medium | 007, 003 | Event-triggered email notifications | `specs/008-notifications/` | Small |

Should I proceed with updating ROADMAP.md?
```

## Notes

- This command focuses on planning, not implementation
- Keep the analysis concise and actionable
- Always reference existing specs by number
- Be explicit about why dependencies exist
- Suggest breaking up large features proactively
