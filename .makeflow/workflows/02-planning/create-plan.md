# Workflow: Create Task Plan

**Stage**: 02 - Planning  
**Purpose**: Break work into executable tasks
**Time**: 15-30 minutes  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ You have clear requirements
- ✅ You need a task breakdown
- ✅ Feature is medium complexity (2-8 hours)
- ✅ You want to track progress incrementally

---

## Prerequisites

- [ ] Work folder exists (`.makeflow/work/[feature-name]/`)
- [ ] Requirements documented in AGENTS.md
- [ ] (Optional) Spec.md for complex features

---

## Instructions for AI Agent

### Step 1: Review Context

Read `.makeflow/work/[feature-name]/AGENTS.md` (and spec.md if exists) to understand:
- What needs to be built
- Acceptance criteria
- Technical approach
- Constraints

### Step 2: Break Into Phases

Divide work into logical phases:
- **Phase 1**: Foundation/Setup
- **Phase 2**: Core functionality
- **Phase 3**: Testing & polish

Each phase should:
- Be completable in one session (2-4 hours max)
- Have a clear deliverable
- Enable progress verification

### Step 3: Create plan.md

Create `.makeflow/work/[feature-name]/plan.md`:

```markdown
# [Feature Name] - Task Plan

**Created**: [YYYY-MM-DD]  
**Total Estimated Time**: [X hours]  
**Complexity**: [Simple/Medium/Complex]

---

## Overview

**Goal**: [One sentence - what we're building]

**Approach**: [High-level strategy]

**Success**: [How we know it's done]

---

## Phase 1: [Phase Name]

**Goal**: [What this phase achieves]  
**Estimated**: [X hours]  
**Status**: 🔄 Not Started

### Tasks:

#### Task 1.1: [Task Name]
**What**: [Specific action to take]  
**Files**: 
- `path/to/file.ext` - [What to do]

**Acceptance**:
- [ ] [Specific criterion]

**Estimated**: [minutes/hours]

---

#### Task 1.2: [Task Name]
[Same structure]

---

## Phase 2: [Phase Name]

**Goal**: [What this phase achieves]  
**Estimated**: [X hours]  
**Status**: 📝 Pending Phase 1

[Same task structure]

---

## Phase 3: [Phase Name]

**Goal**: [What this phase achieves]  
**Estimated**: [X hours]  
**Status**: 📝 Pending Phase 2

[Same task structure]

---

## Testing Checklist

### Unit Tests
- [ ] [Test scenario 1]
- [ ] [Test scenario 2]

### Integration Tests
- [ ] [Test scenario 1]

### Manual Testing
- [ ] [Test flow 1]
- [ ] [Test flow 2]

---

## Files to Create/Modify

### New Files:
- `path/to/new-file.ext` - [Purpose]

### Modified Files:
- `path/to/existing-file.ext` - [Changes]

### Test Files:
- `path/to/test-file.test.ext` - [Tests]

---

## Dependencies

**Must be done first**:
- [Prerequisite 1]

**Can be done in parallel**:
- [Task A] and [Task B]

**Blocks other work**:
- [What this blocks]

---

## Risks

| Risk | Mitigation |
|------|------------|
| [Risk 1] | [How to handle] |
| [Risk 2] | [How to handle] |

---

## Progress Tracking

- [ ] Phase 1 complete
- [ ] Phase 2 complete
- [ ] Phase 3 complete
- [ ] All tests passing
- [ ] Documentation updated
- [ ] Ready for review

---

## Notes

[Space for notes during implementation]
```

### Step 4: Update AGENTS.md

Update `.makeflow/work/[feature-name]/AGENTS.md`:

```markdown
## 📊 Current Progress

### Phase 1: [Phase Name]
**Status**: 🔄 Ready to Start

**Tasks**:
- [ ] Task 1.1: [Description]
- [ ] Task 1.2: [Description]

[... rest of phases]
```

Add to decisions log:
```markdown
### [YYYY-MM-DD] - Task Plan Created
**Decision**: Broke work into [N] phases  
**Rationale**: [Why these phases]  
**Estimated Total**: [X hours]
```

### Step 5: Present Plan to User

```markdown
---

## 📋 Task Plan Created

**Location**: `.makeflow/work/[feature-name]/plan.md`

### Summary:
- **Phases**: [N phases]
- **Total Tasks**: [N tasks]
- **Estimated Time**: [X hours]

### Breakdown:

**Phase 1: [Name]** ([X hours])
- Task 1.1: [Name]
- Task 1.2: [Name]
- ...

**Phase 2: [Name]** ([X hours])
- Task 2.1: [Name]
- ...

**Phase 3: [Name]** ([X hours])
- Task 3.1: [Name]
- ...

---

## 🚀 Ready to Start Building

**Recommended approach**:

```
@ai Use .makeflow/workflows/03-execution/execute-task.md
Feature: [feature-name]
Task: Task 1.1
```

Or build the entire first phase:

```
@ai Use .makeflow/workflows/03-execution/execute-phase.md
Feature: [feature-name]
Phase: 1
```

Which approach do you prefer?
```

---

## Example: Resource Multi-Filter

**Requirements**: Add multi-criteria filtering to resources table

**Plan**:

### Phase 1: UI Components (2 hours)
- Task 1.1: Add multi-select filter dropdowns
- Task 1.2: Add "Clear filters" button
- Task 1.3: Add filtered count display

### Phase 2: Filter Logic (2 hours)
- Task 2.1: Implement compound filter logic
- Task 2.2: Update URL params for sharing
- Task 2.3: Add filter state management

### Phase 3: Testing & Performance (2 hours)
- Task 3.1: Unit tests for filter logic
- Task 3.2: Test with 1000+ records
- Task 3.3: E2E tests for filter flows

**Total**: 6 hours, broken into 3 phases

---

## Tips for Good Task Plans

### ✅ DO:
- Make tasks concrete and actionable
- Keep tasks small (< 1 hour each)
- Group related tasks into phases
- Include testing in the plan
- Estimate realistically

### ❌ DON'T:
- Make tasks too large or vague
- Skip test planning
- Forget about error handling
- Ignore dependencies between tasks
- Under-estimate time

---

## Task Sizing Guidelines

**Small task** (15-30 min):
- Add a button
- Update text/styling
- Simple validation rule

**Medium task** (30-60 min):
- New component with props
- API endpoint
- Database query

**Large task** (1-2 hours):
- Complex component with state
- Multi-step user flow
- Integration with external service

**If > 2 hours**: Break it down further!

---

## Validation Checklist

- [ ] Work broken into logical phases
- [ ] Each phase has clear goal
- [ ] Tasks are specific and actionable
- [ ] Tasks are sized < 1 hour
- [ ] Testing included in plan
- [ ] Dependencies identified
- [ ] Risks noted
- [ ] Plan reviewed with user
- [ ] AGENTS.md updated

---

## Integration with Other Workflows

**Next → Execute tasks**:
```
.makeflow/workflows/03-execution/execute-task.md
```

**Next → Execute phase**:
```
.makeflow/workflows/03-execution/execute-phase.md
```

**Optional → Create ticket from plan**:
```
.makeflow/workflows/02-planning/create-ticket.md
```

---

**End of Workflow**

