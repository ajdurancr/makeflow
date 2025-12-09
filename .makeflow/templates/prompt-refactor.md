# Refactor Prompt Template

Copy this template when requesting a refactor from an AI tool.

---

## 🔧 Basic Refactor Request

```markdown
@ai Use .makeflow/workflows/03-execution/execute-task.md

Refactor: [What needs to be refactored]

Target Files:
- [path/to/file1.ext]
- [path/to/file2.ext]

Goal: [What improvement are we making]

Constraints:
- [ ] Maintain existing API/exports
- [ ] Keep backward compatibility
- [ ] All existing tests must pass
- [ ] No behavior changes
```

---

## 🔧 Extract to Utility/Component

```markdown
@ai Refactor by extracting reusable code

Current Situation:
- File: [path/to/file.ext]
- Code: [describe duplicated or complex code]

Extract To:
- New file: [path/to/new-util.ext]
- Purpose: [what this utility/component does]

Pattern to Follow:
- [path/to/similar-utility.ext]

Tests Needed:
- [ ] Unit tests for extracted code
- [ ] Existing tests still pass
```

---

## 🔧 Improve Code Quality

```markdown
@ai Refactor to improve code quality

Target: [path/to/file.ext]

Issues to Address:
- [Issue 1: e.g., "Function is too long (200+ lines)"]
- [Issue 2: e.g., "Complex nested conditionals"]
- [Issue 3: e.g., "Duplicate logic in 3 places"]

Goals:
- [ ] Reduce complexity
- [ ] Improve readability
- [ ] Make testable

Constraints:
- DO NOT change behavior
- Maintain existing API
- All existing tests must pass
```

---

## 🔧 Performance Optimization

```markdown
@ai Optimize performance

Target: [path/to/file.ext or feature name]

Performance Issue:
- [Description of slow operation]
- Current: [e.g., "Takes 5 seconds for 1000 items"]
- Target: [e.g., "Should be < 1 second"]

Profiling Data:
- [What measurements show the bottleneck]

Proposed Approach:
- [Optimization technique to try]

Constraints:
- Maintain correctness
- Don't break existing functionality
- Add performance tests
```

---

## 🔧 Type Safety Improvements

```markdown
@ai Improve type safety

Target Files:
- [path/to/file1.ts]
- [path/to/file2.ts]

Current Issues:
- [Issue 1: e.g., "Using 'any' types in 5 places"]
- [Issue 2: e.g., "Missing return type annotations"]
- [Issue 3: e.g., "Unsafe type assertions"]

Goals:
- [ ] Replace 'any' with proper types
- [ ] Add missing type annotations
- [ ] Remove unsafe assertions
- [ ] Fix TypeScript errors without @ts-ignore

Pattern:
- Follow type patterns from [path/to/well-typed-file.ts]
```

---

## Examples

### Example 1: Extract Duplicate Code

```markdown
@codegen Refactor by extracting duplicate validation logic

Current Situation:
- Files: 
  - app/routes/users.create.tsx
  - app/routes/users.edit.tsx
  - app/routes/users.import.tsx
- Code: Email validation logic duplicated in all 3 files

Extract To:
- New file: app/lib/validators/email.ts
- Purpose: Reusable email validation

Pattern to Follow:
- app/lib/validators/phone.ts (similar pattern)

Tests Needed:
- [ ] Unit tests for email validator
- [ ] All 3 route tests still pass
- [ ] Edge cases covered (invalid emails, empty, etc.)
```

### Example 2: Reduce Complexity

```markdown
@cursor Refactor to reduce complexity

Target: app/components/ResourceTable.tsx

Issues to Address:
- Main render function is 300+ lines
- 5 levels of nested conditionals
- Multiple responsibilities (rendering, filtering, sorting, pagination)

Goals:
- [ ] Extract filtering logic to custom hook
- [ ] Extract sorting logic to custom hook
- [ ] Extract pagination to separate component
- [ ] Reduce main component to < 100 lines
- [ ] Each piece should be independently testable

Constraints:
- DO NOT change table behavior or appearance
- All existing tests must pass
- Maintain same props interface
```

### Example 3: Performance Optimization

```markdown
@claude Optimize rendering performance

Target: Dashboard resources page

Performance Issue:
- Page re-renders completely on every filter change
- Current: 500ms delay with 1000 resources
- Target: < 100ms

Profiling Data:
- React DevTools shows ResourceTable re-renders all rows
- Memo not being used effectively
- Filter function runs on every render

Proposed Approach:
- Add useMemo for filtered data
- Add React.memo for table rows
- Optimize filter predicate
- Add virtual scrolling if needed

Constraints:
- Maintain all current functionality
- Don't break existing filters
- Add performance test to prevent regression
```

### Example 4: Modernize Code

```markdown
@codegen Modernize code to use latest patterns

Target: app/data/legacy-api.ts

Current Issues:
- Uses class-based approach (old pattern)
- Callbacks instead of promises
- No TypeScript types
- No error handling

Modernize To:
- Convert to functional approach
- Use async/await
- Add full TypeScript types
- Add proper error handling
- Follow pattern from app/data/modern-api.ts

Constraints:
- Maintain same public API (for backward compat)
- All existing callers must continue working
- Add tests (currently has none)
```

---

## Refactor Safety Checklist

Before starting any refactor:

- [ ] All existing tests pass
- [ ] You understand what the code currently does
- [ ] You have a clear goal for the refactor
- [ ] You know how to verify nothing broke

During refactoring:

- [ ] Make small, incremental changes
- [ ] Run tests after each change
- [ ] Commit working states frequently
- [ ] Don't mix refactor with new features

After refactoring:

- [ ] All tests still pass
- [ ] Code is more maintainable
- [ ] Performance hasn't regressed
- [ ] Documentation is updated

---

## When to Refactor

### ✅ Good Times to Refactor:
- Before adding a feature (make room for new code)
- After code review (address feedback)
- When fixing a bug (clean up while you're there)
- When code becomes hard to understand
- When you find duplicate code

### ❌ Bad Times to Refactor:
- Under time pressure for delivery
- Without understanding the code
- Without tests to verify correctness
- While adding new features
- Right before a major release

---

## Refactor Workflows

### Small Refactor (< 2 hours)
```markdown
@ai Use .makeflow/workflows/03-execution/execute-quick.md

Refactor: [description]
[Details]
```

### Medium Refactor (2-8 hours)
```markdown
@ai Use .makeflow/workflows/02-planning/create-plan.md

Refactor Project: [description]
[Break into phases]
```

### Large Refactor (8+ hours)
```markdown
@ai Use .makeflow/workflows/02-planning/create-spec.md

Refactor Initiative: [description]
[Full specification needed]
```

---

## Tips for Successful Refactoring

### ✅ DO:
- Have tests before you start
- Make small, verifiable changes
- Commit frequently
- Keep refactors focused
- Maintain backward compatibility
- Document why you're refactoring

### ❌ DON'T:
- Refactor and add features simultaneously
- Skip running tests
- Change behavior "while you're at it"
- Refactor without understanding
- Make huge changes in one commit
- Forget to update documentation

