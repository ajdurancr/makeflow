# Workflow: Execute Complete Phase

**Stage**: 03 - Execution  
**Purpose**: Implement all tasks in a single phase  
**Time**: 2-4 hours  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ You have a plan with defined phases
- ✅ You want to complete an entire phase at once
- ✅ Tasks in the phase are related and interdependent
- ✅ You have 2-4 hours for focused work

---

## Prerequisites

- [ ] Work folder exists (`.makeflow/work/[feature-name]/`)
- [ ] Plan.md exists with defined phases
- [ ] Phase tasks are clearly defined
- [ ] Previous phases completed (if applicable)

---

## Instructions for AI Agent

### Step 1: Read Phase Context

From `.makeflow/work/[feature-name]/`:
- Read `AGENTS.md` for overall context
- Read `plan.md` to find the target phase
- Identify all tasks in this phase

**Phase should have**:
- Clear goal statement
- List of tasks to complete
- Acceptance criteria for each task
- Estimated time

### Step 2: Validate Phase Readiness

**Check prerequisites**:
- [ ] Previous phases complete (or this is Phase 1)
- [ ] All task requirements are clear
- [ ] Dependencies are available
- [ ] No blockers exist

**If blocked**:
- Document the blocker in AGENTS.md
- Ask user for clarification
- Don't proceed until unblocked

### Step 3: Execute Each Task in Order

**For each task in the phase**:

#### 3.1: Read Task Details
```markdown
Task X.Y: [Task Name]
**What**: [Description]
**Files**: [Files to modify/create]
**Acceptance**: [Criteria]
```

#### 3.2: Implement the Task
- Read existing files (if modifying)
- Make required changes
- Follow project conventions
- Handle errors appropriately
- Add comments for complex logic

#### 3.3: Write Tests
- Unit tests for core logic
- Integration tests (if needed)
- Edge case coverage
- Error condition tests

#### 3.4: Verify Task Complete
- [ ] Manual testing passed
- [ ] All tests passing
- [ ] Acceptance criteria met
- [ ] No linting/type errors

#### 3.5: Mark Task Complete
Update plan.md:
```markdown
#### Task X.Y: [Task Name]
**Status**: ✅ Complete  
**Completed**: [YYYY-MM-DD]
```

#### 3.6: Continue to Next Task
Repeat steps 3.1-3.5 for all tasks in phase

### Step 4: Phase Integration Testing

**After all tasks complete**:
- [ ] Run full test suite
- [ ] Manual end-to-end testing
- [ ] Verify phase goal achieved
- [ ] Check all acceptance criteria
- [ ] Test integration between tasks

**Integration checklist**:
- [ ] All tasks work together
- [ ] No conflicts between changes
- [ ] Performance is acceptable
- [ ] UX is smooth and consistent
- [ ] Error handling is complete

### Step 5: Update Documentation

**Update plan.md**:
```markdown
## Phase X: [Phase Name]
**Status**: ✅ Complete  
**Completed**: [YYYY-MM-DD]

**Goal**: [Original goal] ✅ Achieved

### Tasks:
- [x] Task X.1: [Description] ✅ [Date]
- [x] Task X.2: [Description] ✅ [Date]
- [x] Task X.3: [Description] ✅ [Date]

**Notes**:
- [Key decision made]
- [Challenge encountered and how solved]
- [Important implementation detail]
```

**Update AGENTS.md**:
```markdown
### Phase X: [Phase Name]
**Status**: ✅ Complete  
**Completed**: [YYYY-MM-DD]

**Summary**:
- [What was built]
- [How it works]
- [What's next]

---

### Progress Log

#### [YYYY-MM-DD]
- ✅ Completed Phase X: [Phase Name]
- Tasks: [Summary of all tasks]
- Tests: [Test coverage summary]
- Integration: [How tasks work together]
- Next: Phase [X+1] or [Delivery]
```

### Step 6: Commit Changes

**Create meaningful commit**:
```bash
git add .
git commit -m "feat: Complete Phase X - [Phase Name]

Implemented:
- Task X.1: [Brief description]
- Task X.2: [Brief description]
- Task X.3: [Brief description]

Tests added:
- [Test coverage summary]

Phase goal achieved: [Goal statement]"
```

### Step 7: Present Results

```markdown
---

## ✅ Phase Complete

**Phase**: Phase X - [Phase Name]

### Goal Achieved:
[Original phase goal and how it was met]

### Tasks Completed:
1. ✅ Task X.1: [Name] - [Brief summary]
2. ✅ Task X.2: [Name] - [Brief summary]
3. ✅ Task X.3: [Name] - [Brief summary]

### Files Modified/Created:
- `path/to/file1.ext` - [What changed]
- `path/to/file2.ext` - [What changed]
- `path/to/file3.ext` - [What changed]
- `path/to/tests.test.ext` - [Tests added]

### Tests Added:
- ✅ [X] unit tests
- ✅ [Y] integration tests
- ✅ Edge cases covered
- ✅ Error handling tested

**Test Results**: [X/X passing]

### Integration Verification:
- [x] All tasks work together
- [x] End-to-end flow tested
- [x] Phase acceptance criteria met
- [x] No conflicts or issues

---

## 🚀 Next Steps

**Continue to next phase**:
```
@ai Use .makeflow/workflows/03-execution/execute-phase.md
Feature: [feature-name]
Phase: [X+1]
```

**Execute all remaining phases**:
```
@ai Use .makeflow/workflows/03-execution/execute-all-phases.md
Feature: [feature-name]
Starting from: Phase [X+1]
```

**Or if all phases complete**:
```
@ai Use .makeflow/workflows/04-delivery/create-pr.md
Feature: [feature-name]
```

Which would you like to do?
```

---

## Example: Complete Phase 1 - Database Schema

**Phase**: Phase 1 - Database Schema & Models

**Tasks**:
1. Task 1.1: Create resources table migration
2. Task 1.2: Create Resource model with validation
3. Task 1.3: Add seed data for testing

### Task 1.1: Create Migration
```sql
-- migrations/001_create_resources.sql
CREATE TABLE resources (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(255) NOT NULL,
  type VARCHAR(50) NOT NULL,
  location_id UUID REFERENCES locations(id),
  created_at TIMESTAMP DEFAULT NOW()
);
```

**Tests**:
```typescript
describe('resources migration', () => {
  it('creates resources table', async () => { ... });
  it('has correct columns', async () => { ... });
});
```

### Task 1.2: Create Model
```typescript
// app/models/resource.server.ts
export interface Resource {
  id: string;
  name: string;
  type: ResourceType;
  locationId: string;
}

export const ResourceSchema = z.object({
  name: z.string().min(1).max(255),
  type: z.enum(['Equipment', 'Tools', 'Vehicles']),
  locationId: z.string().uuid(),
});
```

**Tests**:
```typescript
describe('Resource model', () => {
  it('validates correct data', () => { ... });
  it('rejects invalid data', () => { ... });
});
```

### Task 1.3: Add Seed Data
```typescript
// prisma/seed.ts
const resources = [
  { name: 'Excavator', type: 'Equipment', locationId: '...' },
  { name: 'Drill Set', type: 'Tools', locationId: '...' },
];
```

### Phase Complete
- ✅ Database schema created
- ✅ Models defined with validation
- ✅ Seed data available
- ✅ All 8 tests passing
- ✅ Ready for Phase 2: API Layer

---

## Tips for Phase Execution

### ✅ DO:
- Complete tasks in order (unless independent)
- Test each task before moving to next
- Keep commits focused per task
- Update documentation as you go
- Verify integration between tasks
- Take breaks between tasks if needed

### ❌ DON'T:
- Skip tasks or change order without reason
- Move to next task with failing tests
- Wait until end to test integration
- Forget to update phase status
- Rush through without verification
- Skip documentation updates

---

## Handling Issues During Phase

### If a Task is Blocked:
1. Document the blocker in AGENTS.md
2. Skip to next independent task (if any)
3. Complete what you can
4. Ask user for help with blocker
5. Come back to blocked task later

### If a Task Takes Longer Than Expected:
1. Update time estimate in plan.md
2. Consider splitting into sub-tasks
3. Complete what's working
4. Document remaining work
5. Ask user if you should continue or pause

### If Tests Are Failing:
1. Don't move to next task
2. Debug and fix the issue
3. Add tests to prevent regression
4. Update implementation if needed
5. Verify all tests pass before continuing

### If Requirements Are Unclear:
1. Stop and document the ambiguity
2. Ask user for clarification
3. Don't make assumptions
4. Wait for clear answer
5. Update plan.md with clarification

---

## Phase Completion Checklist

- [ ] All tasks in phase complete
- [ ] Each task has passing tests
- [ ] Integration testing performed
- [ ] Phase goal achieved
- [ ] Acceptance criteria met
- [ ] Documentation updated (plan.md, AGENTS.md)
- [ ] Changes committed with clear message
- [ ] No linting/type errors
- [ ] Manual testing completed
- [ ] Ready for next phase or delivery

---

## Integration with Other Workflows

**Execute single task** (if phase interrupted):
```
.makeflow/workflows/03-execution/execute-task.md
```

**Execute all phases** (continue momentum):
```
.makeflow/workflows/03-execution/execute-all-phases.md
```

**Quick fix** (if bug found during phase):
```
.makeflow/workflows/03-execution/execute-quick.md
```

**Create PR** (if all phases complete):
```
.makeflow/workflows/04-delivery/create-pr.md
```

---

**End of Workflow**

