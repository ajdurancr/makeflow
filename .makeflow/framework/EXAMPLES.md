# Real-World Examples

See makeflow in action with complete examples.

---

## Example 1: Simple Bug Fix

**Scenario**: Users report that resource names with special characters break Excel export

### Step 1: Report Bug

```markdown
@codegen Use .makeflow/workflows/01-intake/from-bug.md

Bug: Excel export fails when resource names contain "/" or "\"

Reproduction:
1. Create resource named "Test/Resource"
2. Click Export to Excel
3. Browser shows error: "Invalid filename"

Expected: Export succeeds with sanitized filename
Actual: Export fails with error

Environment: Production, all browsers
Severity: Medium (workaround: rename resource)
```

### Step 2: AI Investigation

AI creates `.makeflow/work/bug-excel-special-chars/AGENTS.md`:

```markdown
# Bug Fix: Excel Export Special Characters

**Root Cause**: Filename generation doesn't escape "/" and "\" characters

**Location**: `app/lib/excel-utils.ts:45`

**Fix**: Sanitize resource name before using in filename

**Files to Change**:
- `app/lib/excel-utils.ts` - Add sanitization
- `app/lib/excel-utils.test.ts` - Add tests
```

### Step 3: Quick Fix

```markdown
@codegen Use .makeflow/workflows/03-execution/execute-quick.md

Feature: bug-excel-special-chars
```

AI implements:

```typescript
// app/lib/excel-utils.ts
function sanitizeFilename(name: string): string {
  return name.replace(/[/\\?%*:|"<>]/g, '-');
}

export function generateExcelFilename(resourceName: string): string {
  const sanitized = sanitizeFilename(resourceName);
  const date = new Date().toISOString().split('T')[0];
  return `${sanitized}-${date}.xlsx`;
}
```

Tests:

```typescript
describe('sanitizeFilename', () => {
  it('replaces forward slashes', () => {
    expect(sanitizeFilename('Test/Resource')).toBe('Test-Resource');
  });
  
  it('replaces backslashes', () => {
    expect(sanitizeFilename('Test\\Resource')).toBe('Test-Resource');
  });
});
```

### Step 4: Create PR

```markdown
@codegen Use .makeflow/workflows/04-delivery/create-pr.md

Feature: bug-excel-special-chars
```

PR created: `fix: Sanitize special characters in Excel export filenames`

### Step 5: Complete

```markdown
@codegen Use .makeflow/workflows/04-delivery/complete.md

Feature: bug-excel-special-chars
```

Work summarized to `.makeflow/history/2025-12-09-bug-excel-special-chars/`

**Total time**: ~30 minutes from bug report to merged PR

---

## Example 2: Medium Feature (Multi-Criteria Filtering)

**Scenario**: Administrators need to filter resources by multiple criteria simultaneously

### Step 1: Start from Ticket

```markdown
@codegen Use .makeflow/workflows/01-intake/from-ticket.md

Ticket: ASG-145
```

AI reads ticket, creates `.makeflow/work/resource-multi-filter/AGENTS.md` with requirements.

### Step 2: Create Plan

```markdown
@codegen Use .makeflow/workflows/02-planning/create-plan.md

Feature: resource-multi-filter
```

AI creates `.makeflow/work/resource-multi-filter/plan.md`:

```markdown
## Phase 1: UI Components (2 hours)
- Task 1.1: Add multi-select for Type filter
- Task 1.2: Add multi-select for Status filter
- Task 1.3: Add multi-select for Location filter
- Task 1.4: Add "Clear all filters" button

## Phase 2: Filter Logic (2 hours)
- Task 2.1: Implement compound filter logic
- Task 2.2: Update URL params
- Task 2.3: Add filter state management

## Phase 3: Testing (2 hours)
- Task 3.1: Unit tests for filter logic
- Task 3.2: Performance test with 1000+ resources
- Task 3.3: E2E tests for filter flows
```

### Step 3: Execute Tasks

```markdown
@codegen Use .makeflow/workflows/03-execution/execute-task.md

Feature: resource-multi-filter
Task: Task 1.1
```

Repeat for each task... AI implements and tests each one.

### Step 4: Create PR

```markdown
@codegen Use .makeflow/workflows/04-delivery/create-pr.md

Feature: resource-multi-filter
```

PR created with comprehensive description, screenshots, testing instructions.

### Step 5: Complete

After PR merged:

```markdown
@codegen Use .makeflow/workflows/04-delivery/complete.md

Feature: resource-multi-filter
```

**Total time**: ~8 hours from ticket to shipped feature

---

## Example 3: Complex Feature (Bulk Operations)

**Scenario**: Enable bulk assignment of resources to locations

### Step 1: Start from Idea

```markdown
@codegen Use .makeflow/workflows/01-intake/from-idea.md

Feature Idea: Bulk assign resources to locations

Context:
- Users: Administrators setting up new locations
- Problem: Assigning 50+ resources one-by-one is tedious
- Current: Individual assignment only
- Desired: Select multiple, assign all at once
```

AI asks clarifying questions:

```markdown
## Clarifying Questions

1. Should users select resources via checkboxes or a separate modal?
2. What happens if some assignments fail?
3. Should this work across different resource types?
4. Any limit on bulk size?
5. How should assignment history show bulk operations?
```

User answers, AI creates work folder.

### Step 2: Create Specification

```markdown
@codegen Use .makeflow/workflows/02-planning/create-spec.md

Feature: resource-bulk-assign
```

AI creates detailed spec.md:

```markdown
# Resource Bulk Assignment - Technical Specification

## Architecture
- Checkboxes in table rows
- Bulk action toolbar when > 0 selected
- Modified assignment dialog for bulk mode
- Database transaction for atomicity

## Components
- BulkActionToolbar
- BulkAssignDialog
- useResourceSelection hook

## API
- POST /api/resources/bulk-assign
- Transaction-based for all-or-nothing

## Testing
- Unit tests for selection state
- Integration tests for transaction
- E2E tests for full flow
- Performance test with 100+ resources
```

### Step 3: Create Plan

```markdown
@codegen Use .makeflow/workflows/02-planning/create-plan.md

Feature: resource-bulk-assign
```

AI breaks into phases and tasks.

### Step 4: Create Ticket

```markdown
@codegen Use .makeflow/workflows/02-planning/create-ticket.md

Feature: resource-bulk-assign
```

Ticket created in Linear/Jira with spec details.

### Step 5: Execute in Phases

```markdown
# Phase 1
@codegen Use .makeflow/workflows/03-execution/execute-task.md
Feature: resource-bulk-assign
Task: Task 1.1

[Repeat for all Phase 1 tasks]

# Phase 2
[Repeat for all Phase 2 tasks]

# Phase 3
[Repeat for all Phase 3 tasks]
```

### Step 6: Update Documentation

```markdown
@codegen Use .makeflow/workflows/04-delivery/update-docs.md

Feature: resource-bulk-assign
```

AI updates:
- User guide with bulk operations section
- API docs with new endpoint
- Component docs

### Step 7: Create PR & Complete

```markdown
@codegen Use .makeflow/workflows/04-delivery/create-pr.md
Feature: resource-bulk-assign

# After merge:
@codegen Use .makeflow/workflows/04-delivery/complete.md
Feature: resource-bulk-assign
```

**Total time**: ~24 hours from idea to shipped feature

---

## Example 4: Working Across Multiple Sessions

**Scenario**: You start a feature, life happens, you return later

### Day 1 - Start Feature

```markdown
@codegen Use .makeflow/workflows/01-intake/from-ticket.md

Ticket: ASG-200
```

AI creates work folder, you implement first few tasks, then call it a day.

### Day 3 - Resume Work

```markdown
@codegen I'm continuing work on ASG-200.

Please read `.makeflow/work/notification-system/AGENTS.md` for full context.

What's the next task I should work on?
```

AI reads AGENTS.md, sees progress, recommends next task.

```markdown
@codegen Use .makeflow/workflows/03-execution/execute-task.md

Feature: notification-system
Task: Task 2.3
```

Continue from where you left off!

### Day 5 - Another Developer Helps

```markdown
@codegen I'm helping with ASG-200.

Please read `.makeflow/work/notification-system/AGENTS.md`.

I'll work on Task 3.1 while original developer does Task 3.2.
```

Multiple developers can work on same feature using AGENTS.md as shared context.

---

## Example 5: Emergency Hotfix

**Scenario**: Production bug needs immediate fix

### Step 1: Fast Bug Report

```markdown
@codegen URGENT: Use .makeflow/workflows/01-intake/from-bug.md

Bug: Users can't login - getting 500 error
Severity: Critical (P0)
Impact: All users affected
Started: ~10 minutes ago
Error: "Cannot read property 'id' of null" in auth.ts:67
```

### Step 2: Immediate Fix

```markdown
@codegen Use .makeflow/workflows/03-execution/execute-quick.md

Feature: bug-login-500

Fix: Add null check for user object before accessing user.id
File: app/auth.ts:67
Test: Login flow still works
```

### Step 3: Fast PR

```markdown
@codegen Use .makeflow/workflows/04-delivery/create-pr.md

Feature: bug-login-500

Mark as HOTFIX and request immediate review
```

### Step 4: Deploy & Complete

After merge and deploy:

```markdown
@codegen Use .makeflow/workflows/04-delivery/complete.md

Feature: bug-login-500
```

**Total time**: ~15 minutes from discovery to deployed fix

---

## Example 6: Refactoring

**Scenario**: Extract duplicate validation logic to utility

### Step 1: Plan Refactor

```markdown
@codegen Use .makeflow/workflows/02-planning/create-plan.md

Refactor: Extract email validation to utility

Current Situation:
- Email validation duplicated in 3 files:
  - app/routes/users.create.tsx
  - app/routes/users.edit.tsx  
  - app/routes/users.import.tsx

Extract To:
- app/lib/validators/email.ts

Pattern: Follow app/lib/validators/phone.ts

Tests: Unit tests + ensure all 3 routes still work
```

### Step 2: Execute Refactor

```markdown
@codegen Use .makeflow/workflows/03-execution/execute-task.md

Feature: refactor-email-validation
Task: Task 1.1 - Extract validator
```

### Step 3: PR with Clear Intent

```markdown
@codegen Use .makeflow/workflows/04-delivery/create-pr.md

Feature: refactor-email-validation

Important: This is a refactor - NO behavior changes
```

---

## Example 7: Documentation-Only Change

**Scenario**: Update API documentation

### Quick Execution

```markdown
@codegen Use .makeflow/workflows/03-execution/execute-quick.md

Task: Update API docs for new filtering endpoint

Files:
- docs/api.md - Add POST /api/resources/filter documentation

Include:
- Request/response format
- Example curl command
- Error codes
```

### Create PR

```markdown
@codegen Use .makeflow/workflows/04-delivery/create-pr.md

Feature: docs-filter-api
Type: Documentation only
```

**Total time**: ~10 minutes

---

## Key Takeaways

### For Simple Changes
- Use `execute-quick.md` → `create-pr.md` → `complete.md`
- Total time: 15-60 minutes

### For Medium Features
- Full intake → planning → execution → delivery cycle
- Break into tasks
- Total time: 4-12 hours

### For Complex Features
- Full specification → detailed plan → phased execution
- Multiple sessions OK
- Total time: 1-5 days

### Across All Examples
- ✅ Requirements always clarified first
- ✅ Work tracked in AGENTS.md
- ✅ Tests included by default
- ✅ PRs comprehensive
- ✅ Work summarized to history

---

**Try it yourself**: Pick any scenario similar to these and follow the workflows! 🚀

