# Workflow: Execute Single Task

**Stage**: 03 - Execution  
**Purpose**: Implement a single task with tests  
**Time**: 30 minutes - 2 hours  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ You have a specific task from a plan
- ✅ Task is well-defined and scoped
- ✅ You want to build incrementally
- ✅ Tests should be included (default)

---

## Prerequisites

- [ ] Work folder exists (`.makeflow/work/[feature-name]/`)
- [ ] Task is defined in plan.md or AGENTS.md
- [ ] Requirements are clear

---

## Instructions for AI Agent

### Step 1: Read Task Context

From `.makeflow/work/[feature-name]/`:
- Read `AGENTS.md` for overall context
- Read `plan.md` (if exists) for task details
- Find the specific task to implement

**Task should have**:
- Clear description
- Files to modify/create
- Acceptance criteria
- Test requirements

### Step 2: Implement the Task

**For each file**:
1. Read the existing file (if modifying)
2. Understand the current structure
3. Make the required changes
4. Follow existing patterns in the codebase

**Implementation checklist**:
- [ ] Code follows project conventions
- [ ] Error handling included
- [ ] Edge cases considered
- [ ] Comments added for complex logic
- [ ] Types/interfaces defined (if TypeScript)

### Step 3: Write Tests (Default)

**Test types needed**:

**Unit Tests** (required):
```typescript
// Test happy path
// Test edge cases  
// Test error conditions
// Test validation
```

**Integration Tests** (if needed):
```typescript
// Test component integration
// Test API interactions
// Test database operations
```

**Test coverage goals**:
- Core logic: 100%
- Edge cases: Major ones covered
- Error paths: Key errors tested

### Step 4: Verify Implementation

**Manual verification**:
- [ ] Run the application
- [ ] Test the implemented functionality
- [ ] Verify acceptance criteria met
- [ ] Check for console errors
- [ ] Test edge cases manually

**Automated verification**:
- [ ] All tests pass
- [ ] No linting errors
- [ ] No type errors
- [ ] Code builds successfully

### Step 5: Update Documentation

**Update plan.md**:
```markdown
#### Task X.Y: [Task Name]
**Status**: ✅ Complete  
**Completed**: [YYYY-MM-DD]

[Original task description]

**Implementation notes**:
- [Key decision made]
- [Challenge encountered]
- [How it was solved]
```

**Update AGENTS.md**:
```markdown
### Phase X: [Phase Name]
**Status**: 🔄 In Progress

**Tasks**:
- [x] Task X.Y: [Description] ✅ [YYYY-MM-DD]
- [ ] Task X.Z: [Description]
```

Add to progress log:
```markdown
### [YYYY-MM-DD]
- ✅ Completed Task X.Y: [Task Name]
- Implementation: [Brief summary]
- Tests: [Test coverage added]
- Next: Task X.Z
```

### Step 6: Present Results

```markdown
---

## ✅ Task Complete

**Task**: Task X.Y - [Task Name]

### What Was Built:
- [Summary of implementation]

### Files Modified/Created:
- `path/to/file1.ext` - [What changed]
- `path/to/file2.ext` - [What changed]  
- `path/to/test.test.ext` - [Tests added]

### Tests Added:
- ✅ Unit tests for [functionality]
- ✅ Edge case: [scenario]
- ✅ Error handling: [scenario]

**Test Results**: [X/X passing]

### Verification:
- [x] Manual testing complete
- [x] All tests pass
- [x] No linting errors
- [x] Acceptance criteria met

---

## 🚀 Next Steps

**Continue with next task**:
```
@ai Use .makeflow/workflows/03-execution/execute-task.md
Feature: [feature-name]
Task: Task X.Z
```

**Or complete the phase**:
```
@ai Use .makeflow/workflows/03-execution/execute-phase.md
Feature: [feature-name]
Phase: X
Status: continue
```

**Or if phase is done**:
Move to next phase or finalize:
```
@ai Use .makeflow/workflows/04-delivery/create-pr.md
Feature: [feature-name]
```

Which would you like to do?
```

---

## Example: Add Multi-Select Filter Component

**Task**: Task 1.1 - Add multi-select filter dropdown for Type column

**Implementation**:

1. **Created component**:
```typescript
// app/components/filters/TypeMultiSelect.tsx
export function TypeMultiSelect({ value, onChange }) {
  const types = ['Equipment', 'Tools', 'Vehicles'];
  return (
    <MultiSelect
      options={types}
      value={value}
      onChange={onChange}
      placeholder="Filter by type..."
    />
  );
}
```

2. **Integrated into table**:
```typescript
// app/routes/dashboard.resources.tsx
const [typeFilters, setTypeFilters] = useState<string[]>([]);

// In table header
<TypeMultiSelect value={typeFilters} onChange={setTypeFilters} />
```

3. **Added tests**:
```typescript
// app/components/filters/TypeMultiSelect.test.tsx
describe('TypeMultiSelect', () => {
  it('renders all type options', () => { ... });
  it('calls onChange when options selected', () => { ... });
  it('displays selected values', () => { ... });
  it('handles clear action', () => { ... });
});
```

**Verification**:
- ✅ Component renders in table header
- ✅ Can select multiple types
- ✅ Selection updates parent state
- ✅ All 4 tests passing
- ✅ No console errors

---

## Tips for Effective Task Execution

### ✅ DO:
- Read existing code to understand patterns
- Follow project conventions
- Write tests as you code (not after)
- Commit frequently
- Test both happy and error paths
- Update documentation immediately

### ❌ DON'T:
- Introduce new patterns without discussion
- Skip tests ("I'll add them later")
- Change unrelated code
- Commit untested code
- Ignore linting/type errors
- Forget to update task status

---

## Common Task Types

### UI Component Task
**Implementation**:
- Create component file
- Define props interface
- Implement render logic
- Add styles

**Tests**:
- Rendering tests
- Interaction tests
- Props validation

---

### API Endpoint Task
**Implementation**:
- Define route handler
- Add validation
- Implement business logic
- Return response

**Tests**:
- Happy path
- Validation errors
- Error handling

---

### Database Query Task
**Implementation**:
- Write query/mutation
- Add error handling
- Optimize for performance
- Handle edge cases

**Tests**:
- Query correctness
- Edge cases (empty results, etc.)
- Error conditions

---

### Integration Task
**Implementation**:
- Connect components
- Handle data flow
- Add loading/error states
- Verify end-to-end flow

**Tests**:
- Integration tests
- E2E tests for critical paths

---

## Test-First Approach (Recommended)

### 1. Write Failing Test
```typescript
it('filters resources by selected types', () => {
  // This will fail initially
  render(<ResourceTable filters={{ types: ['Equipment'] }} />);
  expect(screen.getAllByRole('row')).toHaveLength(5);
});
```

### 2. Implement Feature
```typescript
// Add filtering logic to make test pass
const filteredResources = resources.filter(r =>
  typeFilters.length === 0 || typeFilters.includes(r.type)
);
```

### 3. Verify Test Passes
```bash
npm test -- TypeMultiSelect
```

### 4. Refactor if Needed
```typescript
// Extract filter logic for reusability
const applyFilters = (resources, filters) => { ... };
```

---

## Validation Checklist

- [ ] Task understood from plan/AGENTS.md
- [ ] Existing code patterns reviewed
- [ ] Implementation complete and tested
- [ ] All tests passing
- [ ] No linting/type errors
- [ ] Manual testing performed
- [ ] Acceptance criteria verified
- [ ] Documentation updated (plan.md, AGENTS.md)
- [ ] Changes committed
- [ ] Ready for next task or review

---

## Integration with Other Workflows

**Next task in phase**:
```
.makeflow/workflows/03-execution/execute-task.md
```

**Complete phase**:
```
.makeflow/workflows/03-execution/execute-phase.md
```

**Skip tests** (rare, only if justified):
```
.makeflow/workflows/03-execution/execute-task-without-tests.md
```

**Create PR** (when all done):
```
.makeflow/workflows/04-delivery/create-pr.md
```

---

**End of Workflow**

