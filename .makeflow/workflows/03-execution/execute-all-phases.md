# Workflow: Execute All Phases

**Stage**: 03 - Execution  
**Purpose**: Complete entire feature implementation in one session  
**Time**: 4-8 hours  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ You have a complete plan with all phases defined
- ✅ You want to implement the full feature without interruption
- ✅ All requirements are clear and documented
- ✅ You have 4-8 hours available for focused work
- ✅ Feature is medium complexity (not too large)

---

## Prerequisites

- [ ] Work folder exists (`.makeflow/work/[feature-name]/`)
- [ ] Plan.md exists with all phases defined
- [ ] All requirements documented in AGENTS.md
- [ ] No blockers or unclear requirements
- [ ] Ready for extended work session

---

## Instructions for AI Agent

### Step 1: Read Complete Context

From `.makeflow/work/[feature-name]/`:
- Read `AGENTS.md` thoroughly
- Read `plan.md` completely
- Read `spec.md` (if exists)
- Understand all phases and their relationships

**Validate**:
- [ ] All phases have clear goals
- [ ] All tasks are well-defined
- [ ] Dependencies are documented
- [ ] Acceptance criteria exist
- [ ] Estimated time is reasonable (4-8 hours)

**If not ready**:
- Document issues in AGENTS.md
- Ask user for clarification
- Don't proceed until all is clear

### Step 2: Create Execution Plan

**Review all phases**:
```markdown
Phase 1: [Name] - [Goal] - [Est. time]
Phase 2: [Name] - [Goal] - [Est. time]
Phase 3: [Name] - [Goal] - [Est. time]
...
Total: [X hours]
```

**Identify critical paths**:
- Which tasks must be done first?
- Which phases have dependencies?
- Where are the integration points?
- What are the highest risks?

**Set checkpoints**:
- After each phase: verify integration
- After major milestones: run full tests
- Before final phase: comprehensive review

### Step 3: Execute Phase 1

Follow the complete [execute-phase.md](./execute-phase.md) workflow:

1. Read all Phase 1 tasks
2. Execute each task in order:
   - Implement functionality
   - Write tests
   - Verify completion
   - Mark as done
3. Test phase integration
4. Update documentation
5. Commit Phase 1 changes

**Phase 1 Checkpoint**:
- [ ] All Phase 1 tasks complete
- [ ] Tests passing
- [ ] Phase goal achieved
- [ ] Ready for Phase 2

### Step 4: Execute Phase 2

**Before starting**:
- [ ] Phase 1 verified and stable
- [ ] No outstanding issues
- [ ] Tests all passing

Follow the same process:
1. Read all Phase 2 tasks
2. Execute each task in order
3. Test phase integration
4. **Test integration with Phase 1**
5. Update documentation
6. Commit Phase 2 changes

**Phase 2 Checkpoint**:
- [ ] All Phase 2 tasks complete
- [ ] Tests passing
- [ ] Integrates correctly with Phase 1
- [ ] Phase goal achieved
- [ ] Ready for Phase 3

### Step 5: Execute Remaining Phases

**For each remaining phase**:

1. **Pre-phase Check**:
   - [ ] Previous phases stable
   - [ ] No test failures
   - [ ] Ready to proceed

2. **Execute Phase**:
   - Read all tasks
   - Implement each task
   - Write tests
   - Verify completion
   - Update documentation
   - Commit changes

3. **Phase Checkpoint**:
   - [ ] All tasks complete
   - [ ] Tests passing
   - [ ] Integration verified
   - [ ] Phase goal achieved

4. **Integration Check**:
   - [ ] Works with all previous phases
   - [ ] No conflicts introduced
   - [ ] End-to-end flow working

### Step 6: Final Integration & Testing

**After all phases complete**:

#### 6.1: Run Full Test Suite
```bash
npm test
# or appropriate test command
```
- [ ] All unit tests passing
- [ ] All integration tests passing
- [ ] No test failures
- [ ] Coverage goals met

#### 6.2: End-to-End Testing
- [ ] Test complete user flows
- [ ] Verify all acceptance criteria
- [ ] Test edge cases
- [ ] Test error handling
- [ ] Verify performance

#### 6.3: Manual Testing
- [ ] Run the application
- [ ] Test all new functionality
- [ ] Verify UI/UX
- [ ] Check console for errors
- [ ] Test on different scenarios

#### 6.4: Code Quality Check
- [ ] No linting errors
- [ ] No type errors
- [ ] Code follows conventions
- [ ] Comments added where needed
- [ ] No debug code left

### Step 7: Update Documentation

**Update plan.md**:
```markdown
# [Feature Name] - Task Plan

**Status**: ✅ Complete  
**Completed**: [YYYY-MM-DD]  
**Total Time**: [Actual hours]

---

## Summary

**Goal**: [Original goal] ✅ Achieved

**Implementation**:
[High-level summary of what was built]

---

## Phase 1: [Name]
**Status**: ✅ Complete ([Date])
- [x] Task 1.1: [Name]
- [x] Task 1.2: [Name]
...

## Phase 2: [Name]
**Status**: ✅ Complete ([Date])
- [x] Task 2.1: [Name]
- [x] Task 2.2: [Name]
...

[Continue for all phases]

---

## Final Notes

**Key Decisions**:
- [Important decision 1]
- [Important decision 2]

**Challenges Overcome**:
- [Challenge 1 and solution]
- [Challenge 2 and solution]

**Testing**:
- [X] unit tests
- [Y] integration tests
- All tests passing ✅

**Ready for**: Production deployment
```

**Update AGENTS.md**:
```markdown
## ✅ Implementation Complete

**Feature**: [Feature Name]  
**Completed**: [YYYY-MM-DD]  
**Total Phases**: [X]  
**Total Tasks**: [Y]

### What Was Built:
[Comprehensive summary]

### Architecture:
[Key architectural decisions]

### Testing:
- Unit tests: [X] tests
- Integration tests: [Y] tests
- E2E coverage: [Summary]
- All passing ✅

### Files Created/Modified:
[List of all files with brief descriptions]

---

### Progress Log

#### [YYYY-MM-DD] - FEATURE COMPLETE ✅

**Phase 1**: [Name] ✅
- [Task summaries]

**Phase 2**: [Name] ✅
- [Task summaries]

**Phase 3**: [Name] ✅
- [Task summaries]

**Final Integration**: ✅
- All tests passing
- End-to-end verified
- Ready for PR

**Next**: Create PR and deploy
```

### Step 8: Final Commit

**Create comprehensive commit**:
```bash
git add .
git commit -m "feat: Complete [Feature Name]

Implemented complete feature across [X] phases:

Phase 1 - [Name]:
- [Task summary]

Phase 2 - [Name]:
- [Task summary]

Phase 3 - [Name]:
- [Task summary]

Testing:
- [X] unit tests added
- [Y] integration tests added
- Full E2E coverage
- All tests passing

Closes: #[issue-number]"
```

### Step 9: Present Results

```markdown
---

## 🎉 Feature Complete!

**Feature**: [Feature Name]

### Implementation Summary:
[High-level description of what was built and how it works]

---

## Phases Completed:

### ✅ Phase 1: [Name]
**Goal**: [Goal statement]
- Task 1.1: [Name] - [Brief summary]
- Task 1.2: [Name] - [Brief summary]
- Task 1.3: [Name] - [Brief summary]

### ✅ Phase 2: [Name]
**Goal**: [Goal statement]
- Task 2.1: [Name] - [Brief summary]
- Task 2.2: [Name] - [Brief summary]

### ✅ Phase 3: [Name]
**Goal**: [Goal statement]
- Task 3.1: [Name] - [Brief summary]
- Task 3.2: [Name] - [Brief summary]

---

## Files Created/Modified:

**New Files** ([X] files):
- `path/to/new/file1.ext` - [Purpose]
- `path/to/new/file2.ext` - [Purpose]

**Modified Files** ([Y] files):
- `path/to/existing/file1.ext` - [What changed]
- `path/to/existing/file2.ext` - [What changed]

**Test Files** ([Z] files):
- `path/to/test1.test.ext` - [Coverage]
- `path/to/test2.test.ext` - [Coverage]

---

## Testing & Verification:

### Test Coverage:
- ✅ **Unit Tests**: [X] tests - All passing
- ✅ **Integration Tests**: [Y] tests - All passing
- ✅ **E2E Testing**: Complete user flows verified
- ✅ **Manual Testing**: All functionality verified

### Code Quality:
- ✅ No linting errors
- ✅ No type errors
- ✅ Follows project conventions
- ✅ Code review ready

### Acceptance Criteria:
- [x] [Criterion 1] ✅
- [x] [Criterion 2] ✅
- [x] [Criterion 3] ✅

---

## Key Highlights:

**Architectural Decisions**:
- [Decision 1 and rationale]
- [Decision 2 and rationale]

**Challenges Overcome**:
- [Challenge 1 and how it was solved]
- [Challenge 2 and how it was solved]

**Performance**:
- [Any performance considerations or optimizations]

---

## 🚀 Next Steps

**Create Pull Request**:
```
@ai Use .makeflow/workflows/04-delivery/create-pr.md
Feature: [feature-name]
```

**Or update documentation first**:
```
@ai Use .makeflow/workflows/04-delivery/update-docs.md
Feature: [feature-name]
```

**Ready to proceed?**
```

---

## Example: Complete E-Commerce Checkout Feature

**Feature**: E-Commerce Checkout Flow

### Phase 1: Cart Management ✅
**Tasks**:
- 1.1: Create Cart model and database schema
- 1.2: Implement Add to Cart functionality
- 1.3: Build Cart display component
- 1.4: Add quantity adjustment and removal

**Result**: Fully functional shopping cart

### Phase 2: Checkout Process ✅
**Tasks**:
- 2.1: Create Checkout page with steps
- 2.2: Implement shipping information form
- 2.3: Add payment information form
- 2.4: Build order review component

**Result**: Complete checkout flow UI

### Phase 3: Order Processing ✅
**Tasks**:
- 3.1: Implement order creation logic
- 3.2: Integrate payment processing
- 3.3: Add email confirmation
- 3.4: Create order history view

**Result**: Full order processing system

### Complete Implementation:
- **Files**: 24 files created/modified
- **Tests**: 87 tests (78 unit, 9 integration)
- **Time**: 6.5 hours
- **Status**: ✅ All acceptance criteria met

---

## Tips for Multi-Phase Execution

### ✅ DO:
- Take breaks between phases
- Verify integration after each phase
- Commit after each phase
- Keep documentation updated
- Test incrementally, not just at end
- Ask for help if blocked

### ❌ DON'T:
- Rush through phases
- Skip testing between phases
- Wait until end to commit
- Ignore integration issues
- Continue if previous phase has problems
- Make assumptions about unclear requirements

---

## Handling Long Sessions

### Stay Focused:
- Take 5-10 minute breaks between phases
- Keep water/snacks nearby
- Eliminate distractions
- Focus on one task at a time

### Maintain Quality:
- Don't rush as you get tired
- Double-check work before moving on
- Take extra time for testing
- Review commits before finalizing

### If Session Runs Long:
- It's OK to pause between phases
- Commit completed phase
- Document where you stopped
- Resume later with next phase

### Communication:
- Update user on progress
- Report if taking longer than expected
- Ask for help if stuck
- Celebrate completed phases

---

## Validation Checklist

- [ ] All phases planned and understood
- [ ] Phase 1 complete and verified
- [ ] Phase 2 complete and verified
- [ ] Phase 3 complete and verified
- [ ] [Add more phases as needed]
- [ ] All phases integrate correctly
- [ ] Full test suite passing
- [ ] End-to-end testing complete
- [ ] Manual testing complete
- [ ] Code quality verified
- [ ] All acceptance criteria met
- [ ] Documentation updated
- [ ] Changes committed
- [ ] Ready for PR

---

## When NOT to Use This Workflow

### ❌ DON'T use for:
- Features requiring > 8 hours
- Unclear or incomplete requirements
- When significant discovery needed
- When blocked on external dependencies
- When requirements likely to change

### ✅ Instead use:
- **Large features**: Break into multiple PRs
- **Unclear requirements**: Use planning workflows first
- **Discovery needed**: Use spike/research approach
- **External blockers**: Execute unblocked phases only

---

## Integration with Other Workflows

**Execute single phase** (if need to pause):
```
.makeflow/workflows/03-execution/execute-phase.md
```

**Execute single task** (if interrupted):
```
.makeflow/workflows/03-execution/execute-task.md
```

**Create PR** (when complete):
```
.makeflow/workflows/04-delivery/create-pr.md
```

**Update docs** (before PR):
```
.makeflow/workflows/04-delivery/update-docs.md
```

---

**End of Workflow**

