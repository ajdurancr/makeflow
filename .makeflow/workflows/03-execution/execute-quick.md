# Workflow: Quick Execution

**Stage**: 03 - Execution  
**Purpose**: Fast implementation for simple changes  
**Time**: < 1 hour  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ Simple, well-defined change (< 1 hour)
- ✅ Following existing pattern exactly
- ✅ Low risk, straightforward implementation
- ✅ No ambiguity in requirements

---

## Prerequisites

- [ ] Clear understanding of what needs to be done
- [ ] Existing pattern to follow (if applicable)
- [ ] Access to codebase

---

## Instructions for AI Agent

### Step 1: Understand the Change

**Ask user for (if not provided)**:
```markdown
Quick Change Request:

1. **What**: [What needs to be done]
2. **Where**: [Which files]
3. **Pattern**: [Similar code to follow, if any]
4. **Test**: [How to verify it works]
```

### Step 2: Implement Immediately

**No planning phase needed** - implement directly:

1. Read the target file(s)
2. Understand the context
3. Make the change
4. Follow existing patterns exactly

**Implementation checklist**:
- [ ] Code matches existing style
- [ ] No breaking changes
- [ ] Error handling (if applicable)
- [ ] Comments added (if complex)

### Step 3: Quick Tests

**For code changes**:
- Add minimal tests to prevent regression
- Or verify existing tests still pass

**For simple changes** (text, styling, etc.):
- Manual verification may be sufficient

### Step 4: Verify

**Quick verification**:
- [ ] Change works as expected
- [ ] No console errors
- [ ] Existing functionality unaffected
- [ ] Tests pass (if applicable)

### Step 5: Document Briefly

**If work folder exists**:
Update `.makeflow/work/[feature-name]/AGENTS.md`:

```markdown
### [YYYY-MM-DD]
- ✅ Quick change: [What was done]
- Files: [Files modified]
- Verified: [How you verified]
```

**If no work folder** (standalone fix):
Just commit with clear message:

```bash
git add .
git commit -m "[type]: [clear description]

- [What changed]
- [Why it changed]
- [How to verify]"
```

### Step 6: Present Results

```markdown
---

## ✅ Quick Change Complete

**What**: [Summary]

### Files Modified:
- `path/to/file.ext` - [Change]

### Verification:
- [x] Change works as expected
- [x] No errors introduced
- [x] Tests passing (if applicable)

### Testing:
[How to test this change]

---

## 🚀 Next Steps

**If part of larger feature**:
```
@ai Use .makeflow/workflows/03-execution/execute-task.md
Feature: [feature-name]
Task: [next-task]
```

**If standalone**:
```
@ai Use .makeflow/workflows/04-delivery/create-pr.md
Feature: [change-name]
```

**Or if done**:
Ready for review! Changes are committed.
```

---

## Examples

### Example 1: Fix Text/Copy

**Request**:
```markdown
@codegen Quick change: Update error message

File: app/routes/login.tsx
Line: ~45
Current: "Invalid credentials"
New: "Invalid email or password. Please try again."
```

**Implementation**:
```typescript
// app/routes/login.tsx (line 45)
- throw new Error('Invalid credentials');
+ throw new Error('Invalid email or password. Please try again.');
```

**Verification**: Login with wrong password, see new message

**Time**: 2 minutes

---

### Example 2: Add Simple Validation

**Request**:
```markdown
@cursor Quick change: Add email validation

File: app/lib/validators.ts
Pattern: Follow existing phone validation
Add: Email validation function
```

**Implementation**:
```typescript
// app/lib/validators.ts
export function validateEmail(email: string): boolean {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
}
```

**Tests**:
```typescript
// app/lib/validators.test.ts
describe('validateEmail', () => {
  it('accepts valid emails', () => {
    expect(validateEmail('user@example.com')).toBe(true);
  });
  
  it('rejects invalid emails', () => {
    expect(validateEmail('notanemail')).toBe(false);
  });
});
```

**Time**: 15 minutes

---

### Example 3: Add Button

**Request**:
```markdown
@claude Quick change: Add export button

File: app/routes/dashboard.resources.tsx
Location: Next to filter controls
Pattern: Follow existing "Add Resource" button
Action: onClick -> exportToExcel()
```

**Implementation**:
```tsx
// app/routes/dashboard.resources.tsx
<div className="flex gap-2">
  <Button onClick={exportToExcel}>
    <Download className="mr-2 h-4 w-4" />
    Export
  </Button>
  <Button onClick={openAddDialog}>
    <Plus className="mr-2 h-4 w-4" />
    Add Resource
  </Button>
</div>
```

**Verification**: Button appears, clicking calls exportToExcel()

**Time**: 10 minutes

---

### Example 4: Fix Bug

**Request**:
```markdown
@codegen Quick fix: Handle null case

Bug: App crashes when resource.location is null
File: app/components/ResourceCard.tsx
Line: ~67
Fix: Add null check before accessing location.name
```

**Implementation**:
```typescript
// app/components/ResourceCard.tsx (line 67)
- <span>{resource.location.name}</span>
+ <span>{resource.location?.name ?? 'No location'}</span>
```

**Test**:
```typescript
it('handles null location', () => {
  render(<ResourceCard resource={{ ...mockResource, location: null }} />);
  expect(screen.getByText('No location')).toBeInTheDocument();
});
```

**Time**: 10 minutes

---

## When NOT to Use Quick Execution

### ❌ DON'T use for:
- Complex features (> 1 hour)
- Novel solutions (no existing pattern)
- Ambiguous requirements
- High-risk changes
- Architectural decisions
- Changes affecting multiple systems

### ✅ Instead use:
- `.makeflow/workflows/02-planning/create-plan.md` - For medium features
- `.makeflow/workflows/02-planning/create-spec.md` - For complex features
- `.makeflow/workflows/01-intake/from-idea.md` - For unclear requirements

---

## Quick Execution Checklist

- [ ] Change is well-defined (< 1 hour)
- [ ] Low risk and straightforward
- [ ] Pattern to follow exists (or very simple)
- [ ] No ambiguity in requirements
- [ ] Implementation complete
- [ ] Quick verification done
- [ ] Tests added or existing tests pass
- [ ] Changes committed
- [ ] Ready for review

---

## Tips for Quick Execution

### ✅ DO:
- Follow existing patterns exactly
- Keep changes minimal and focused
- Verify before committing
- Write clear commit messages
- Add minimal tests for code changes

### ❌ DON'T:
- Introduce new patterns
- Make multiple unrelated changes
- Skip verification
- Rush without understanding
- Ignore existing conventions

---

## Integration with Other Workflows

**For standalone quick changes**:
```
.makeflow/workflows/04-delivery/create-pr.md
```

**If part of larger feature**:
```
.makeflow/workflows/03-execution/execute-task.md
```

**If change is more complex than expected**:
```
.makeflow/workflows/02-planning/create-plan.md
```

---

**End of Workflow**

