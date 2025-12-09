# Workflow: Execute Task Without Tests

**Stage**: 03 - Execution  
**Purpose**: Implement task without test coverage (opt-out)  
**Time**: Variable  
**AI-Agnostic**: ✅ Works with any AI tool

---

## ⚠️ Warning

**Tests are HIGHLY RECOMMENDED** for all production code.

Only use this workflow if:
- ✅ Prototyping / proof of concept
- ✅ Temporary code / throw-away work
- ✅ Tests will be added separately later
- ✅ Code is untestable by nature (rare)

**For production code, use**:
`.makeflow/workflows/03-execution/execute-task.md` (includes tests by default)

---

## When to Use This

- ✅ Quick prototype or spike
- ✅ Exploratory work
- ✅ Documentation or config-only changes
- ✅ Tests coming in separate task

---

## Instructions for AI Agent

### Step 1: Confirm No Tests Needed

**Ask user to confirm**:
```markdown
⚠️ **Test-Free Implementation Requested**

You've asked to skip test coverage. This is not recommended for production code.

**Confirm**:
- [ ] This is a prototype/POC
- [ ] OR tests will be added separately
- [ ] OR this is non-production code

Should I proceed without tests?
```

**Wait for explicit confirmation.**

### Step 2: Implement Task

Follow same implementation steps as `execute-task.md`:

1. Read task context from AGENTS.md/plan.md
2. Understand requirements
3. Implement the code
4. Follow existing patterns

**Implementation checklist**:
- [ ] Code follows project conventions
- [ ] Error handling included
- [ ] Edge cases considered
- [ ] Comments added for complex logic

**⚠️ Note**: Document that tests are missing

### Step 3: Manual Verification Only

Since no automated tests:
- [ ] Manual testing is REQUIRED
- [ ] Test happy path thoroughly
- [ ] Test edge cases
- [ ] Test error conditions
- [ ] Verify in multiple scenarios

**Document test scenarios**:
```markdown
## Manual Test Scenarios

### Scenario 1: [Happy Path]
**Steps**:
1. [Action]
2. [Action]
3. [Action]

**Expected**: [Result]
**Actual**: [Result]
**Status**: ✅ Pass

### Scenario 2: [Edge Case]
[Same structure]

### Scenario 3: [Error Case]
[Same structure]
```

### Step 4: Update Documentation

**Update plan.md**:
```markdown
#### Task X.Y: [Task Name]
**Status**: ✅ Complete  
**Completed**: [YYYY-MM-DD]  
**Tests**: ⚠️ None (manual testing only)

**Manual Test Scenarios**: [List scenarios tested]

**TODO**: Add automated tests later
```

**Update AGENTS.md**:
```markdown
### Phase X: [Phase Name]
**Tasks**:
- [x] Task X.Y: [Description] ✅ (No tests) ⚠️

### Technical Debt
- [ ] Add tests for Task X.Y
```

### Step 5: Present Results with Warning

```markdown
---

## ✅ Task Complete (No Tests)

⚠️ **Test Coverage**: None - Manual testing only

**Task**: Task X.Y - [Task Name]

### What Was Built:
- [Summary]

### Files Modified/Created:
- `path/to/file.ext` - [Changes]

### Manual Testing:
- ✅ Scenario 1: [Happy path tested]
- ✅ Scenario 2: [Edge case tested]  
- ✅ Scenario 3: [Error case tested]

### ⚠️ Technical Debt Created:
- **Missing automated tests** for [functionality]
- **Risk Level**: [Low/Medium/High]
- **Recommendation**: Add tests before production deployment

---

## 🚀 Next Steps

**Add tests now** (recommended):
```
@ai Use .makeflow/workflows/03-execution/execute-task.md
Feature: [feature-name]
Task: Add tests for Task X.Y
```

**Continue without tests** (not recommended):
```
@ai Use .makeflow/workflows/03-execution/execute-task-without-tests.md
Feature: [feature-name]
Task: Task X.Z
```

**Proceed to next phase**:
[Show next workflow]

---

Which path would you like to take?
```

---

## Example Usage

### Example: Prototype - Try New Library

**User**:
```markdown
@codegen Use .makeflow/workflows/03-execution/execute-task-without-tests.md

Task: Spike - Try date-fns library for date formatting
Goal: See if date-fns is better than current moment.js
This is exploration only, code might be thrown away
```

**AI Response**:
```markdown
⚠️ **Test-Free Implementation Requested**

**Confirmed**: This is exploratory/prototype work

Proceeding with implementation without tests...

---

## ✅ Spike Complete (No Tests)

**Task**: Date formatting library exploration

### What Was Built:
- Created spike folder with date-fns examples
- Compared with current moment.js implementation
- Tested various format scenarios

### Files Created:
- `spikes/date-fns-spike.ts` - Example implementations
- `spikes/date-comparison.md` - Findings

### Manual Testing:
- ✅ Date formatting matches current output
- ✅ Bundle size: date-fns (15kb) vs moment (67kb)
- ✅ Performance: 2x faster for common operations

### Findings:
**Recommendation**: Switch to date-fns
- Smaller bundle size
- Better performance
- Modern API

### Next Steps:
- Create proper task to migrate
- Include tests in migration
- Remove this spike folder

This spike will not be merged to production.
```

---

## When This Is Acceptable

### ✅ Appropriate Use Cases:

**Prototypes/Spikes**:
- Exploring new library
- Trying different approach
- POC for stakeholders
- Code will be thrown away

**Non-Code Changes**:
- Documentation updates
- Configuration changes
- Readme updates
- Comment-only changes

**Test-Focused Tasks**:
- Tests will be added in next immediate task
- Explicitly planned as two-task sequence
- Clear tracking of missing tests

---

### ❌ NOT Appropriate:

**Production Features**:
- User-facing functionality
- Business logic
- Data processing
- API endpoints

**Bug Fixes**:
- Should ALWAYS include regression tests
- Prevents bug from returning

**Refactoring**:
- Tests verify behavior unchanged
- Essential for safe refactoring

---

## Technical Debt Tracking

When tests are skipped, **document the debt**:

### In AGENTS.md:
```markdown
## 📝 Technical Debt

### Missing Tests
- **Task X.Y**: [Feature name]
  - **Risk**: [Impact if this breaks]
  - **Priority**: [High/Medium/Low]
  - **Plan**: [When/how to add tests]
```

### In plan.md:
```markdown
## Technical Debt Log

| Item | Task | Risk | Status |
|------|------|------|--------|
| No tests for X | Task 2.3 | Medium | TODO |
```

---

## Validation Checklist

- [ ] User confirmed tests not needed
- [ ] Valid reason for skipping tests
- [ ] Task implemented completely
- [ ] Extensive manual testing performed
- [ ] Test scenarios documented
- [ ] Technical debt tracked in AGENTS.md
- [ ] Warning added to documentation
- [ ] Plan for adding tests later (if applicable)

---

## Integration with Other Workflows

**Add tests later**:
```
.makeflow/workflows/03-execution/execute-task.md
Task: Add tests for [previous task]
```

**Continue to next task**:
```
.makeflow/workflows/03-execution/execute-task.md
(Use the normal workflow with tests)
```

**Complete work**:
```
.makeflow/workflows/04-delivery/create-pr.md
Note: Document missing test coverage in PR
```

---

**End of Workflow**

