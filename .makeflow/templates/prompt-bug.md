# Bug Fix Prompt Template

Copy this template when requesting a bug fix from an AI tool.

---

## 🐛 Basic Bug Report

```markdown
@ai Use .makeflow/workflows/01-intake/from-bug.md

Bug: [Short description]

Reproduction Steps:
1. [Step 1]
2. [Step 2]
3. [Step 3]

Expected: [What should happen]
Actual: [What actually happens]

Error Message: [Paste error if available]
```

---

## 🐛 Bug with Known Fix

```markdown
@ai Use .makeflow/workflows/03-execution/execute-quick.md

Bug: [Description]

Root Cause: [What's causing the issue]

Fix: [What needs to be done]

Files to change:
- [path/to/file.ext]

Test: [How to verify it's fixed]
```

---

## 🐛 Complex Bug Needing Investigation

```markdown
@ai Use .makeflow/workflows/01-intake/from-bug.md

Bug: [Description]

Symptoms:
- [Symptom 1]
- [Symptom 2]
- [Symptom 3]

Environment:
- Browser: [browser version]
- OS: [operating system]
- Environment: [dev/staging/production]

Reproduction Rate: [Always / Sometimes / Rare]

Related Changes: [Recent PRs or deployments that might be related]

Logs/Screenshots: [Attach or describe]
```

---

## Examples

### Example 1: Clear Bug with Known Fix

```markdown
@codegen Use .makeflow/workflows/03-execution/execute-quick.md

Bug: Export to Excel fails when resource names contain special characters

Root Cause: Filename generation doesn't escape special characters like "/" and "\"

Fix: Sanitize resource name before using in filename

Files to change:
- app/lib/excel-utils.ts (add sanitization function)
- app/lib/excel-utils.test.ts (add test for special chars)

Test: Create resource named "Test/Resource", export to Excel, verify it works
```

### Example 2: Bug Needing Investigation

```markdown
@cursor Use .makeflow/workflows/01-intake/from-bug.md

Bug: Page crashes when filtering resources by multiple criteria

Reproduction Steps:
1. Navigate to Resources page
2. Apply filter: Type = "Equipment"
3. Add second filter: Status = "Active"
4. Page becomes unresponsive, browser console shows errors

Expected: Both filters should work simultaneously
Actual: Page crashes after adding second filter

Error Message:
```
TypeError: Cannot read property 'map' of undefined
  at ResourcesTable.tsx:145
```

Environment:
- Browser: Chrome 120
- OS: macOS 14
- Environment: Development

Reproduction Rate: Always (100%)

Related Changes: PR #234 added multi-filter support last week

Screenshots: [attached]
```

### Example 3: Intermittent Bug

```markdown
@claude Use .makeflow/workflows/01-intake/from-bug.md

Bug: Occasionally users are logged out unexpectedly

Symptoms:
- User is working normally
- Suddenly sees login screen
- No error message shown
- Happens randomly, can't reproduce consistently

Environment:
- Multiple browsers reported
- Both desktop and mobile
- Production environment only

Reproduction Rate: Rare (< 5% of sessions)

Related Changes: 
- Auth token refresh logic updated in PR #210 two weeks ago
- Session timeout increased from 30min to 2hrs in PR #215

Logs: 
- Server logs show "Invalid token" errors
- No client-side errors in browser console
- Happens more often during high traffic periods
```

---

## Bug Severity Levels

### 🔴 Critical (P0)
- System down / data loss / security breach
- Workflow: Immediate investigation → hotfix → deploy
```markdown
@ai URGENT: Use .makeflow/workflows/03-execution/execute-quick.md

Critical Bug: [description]
Impact: [who/what is affected]
[Include all details]
```

### 🟠 High (P1)
- Major feature broken / many users affected
- Workflow: Prioritize investigation → fix within 1-2 days
```markdown
@ai Use .makeflow/workflows/01-intake/from-bug.md

High Priority Bug: [description]
Impact: [who/what is affected]
[Include reproduction steps]
```

### 🟡 Medium (P2)
- Minor feature issue / workaround available
- Workflow: Normal bug fix process
```markdown
@ai Use .makeflow/workflows/01-intake/from-bug.md

Bug: [description]
[Include reproduction steps]
```

### 🟢 Low (P3)
- Cosmetic issue / nice-to-have fix
- Workflow: Fix when convenient
```markdown
@ai Use .makeflow/workflows/01-intake/from-bug.md

Low Priority Bug: [description]
Workaround: [how users can avoid it]
```

---

## Tips for Good Bug Reports

### ✅ DO:
- Provide exact reproduction steps
- Include error messages verbatim
- Specify environment (browser, OS, etc.)
- Mention when it started happening
- Attach screenshots/videos if helpful
- Note if you can reproduce consistently

### ❌ DON'T:
- Say "it doesn't work" without details
- Skip reproduction steps
- Assume the cause without investigation
- Mix multiple bugs in one report
- Forget to mention severity/impact

---

## After Bug is Fixed

```markdown
@ai Use .makeflow/workflows/04-delivery/complete.md

Feature: [bug-fix-name]

Verification:
- [ ] Bug no longer reproduces
- [ ] Tests added to prevent regression
- [ ] Related bugs checked
- [ ] Documentation updated if needed
```

---

## Related Workflows

- **Report & investigate**: `.makeflow/workflows/01-intake/from-bug.md`
- **Quick fix**: `.makeflow/workflows/03-execution/execute-quick.md`
- **Complete & verify**: `.makeflow/workflows/04-delivery/complete.md`

