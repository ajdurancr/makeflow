# Workflow: Start from Bug Report

**Stage**: 01 - Intake  
**Purpose**: Investigate and document a bug for fixing  
**Time**: 10-20 minutes  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ A bug has been reported
- ✅ You need to investigate the root cause
- ✅ You want to document the fix approach
- ✅ You need to track the bug fix work

---

## Prerequisites

- [ ] Bug description or report
- [ ] Reproduction steps (or ability to find them)
- [ ] Access to relevant code/logs

---

## Instructions for AI Agent

### Step 1: Capture Bug Details

**Ask the user for**:
```markdown
Please provide:

1. **Bug Description** (What's broken?)
2. **Reproduction Steps** (How to trigger it?)
3. **Expected Behavior** (What should happen?)
4. **Actual Behavior** (What actually happens?)
5. **Environment** (Browser, OS, version, etc.)
6. **Error Messages** (Console errors, logs, stack traces)
7. **Severity** (Critical/High/Medium/Low)
```

### Step 2: Attempt to Reproduce

**If you can analyze the codebase**:
1. Search for relevant files based on error messages
2. Identify the code path that triggers the bug
3. Look for obvious issues (null checks, edge cases, etc.)

**Present findings**:
```markdown
## 🔍 Initial Investigation

**Relevant Files**:
- `path/to/file.ext` - [Why this file is relevant]

**Potential Causes**:
1. [Hypothesis 1 based on code/error]
2. [Hypothesis 2]

**Need More Info**:
- [Question about reproduction]
- [Need specific log/error output]
```

### Step 3: Assess Root Cause

**If root cause is clear**:
```markdown
## 🎯 Root Cause Identified

**Problem**: [What's causing the bug]

**Location**: `path/to/file.ext:line-number`

**Why It Happens**: [Explanation]

**Fix Approach**: [How to fix it]
```

**If root cause is unclear**:
```markdown
## 🤔 Root Cause Investigation Needed

**Hypotheses**:
1. [Possible cause 1]
2. [Possible cause 2]

**Next Steps to Diagnose**:
- [ ] [Investigation step 1]
- [ ] [Investigation step 2]

**Information Needed**:
- [What logs/data would help]
```

### Step 4: Create Work Folder

Create `.makeflow/work/bug-[bug-slug]/` with:

#### AGENTS.md
```markdown
# Bug Fix: [Bug Description]

> **Created**: [YYYY-MM-DD]  
> **Status**: 🐛 Investigation  
> **Severity**: [Critical/High/Medium/Low]  
> **Ticket**: [BUG-ID if exists]

---

## 🐛 Bug Description

**What's Broken**: [Description]

**Impact**: [Who/what is affected]

**Reproduction Steps**:
1. [Step 1]
2. [Step 2]
3. [Step 3]

**Expected**: [What should happen]

**Actual**: [What actually happens]

**Environment**:
- Browser/OS: [details]
- Version: [version]
- Environment: [dev/staging/prod]

---

## 🔍 Root Cause Analysis

**Problem**: [Root cause if known, or "Under investigation"]

**Location**: [File and line if known]

**Why It Happens**: [Explanation]

---

## 🔧 Fix Approach

**Solution**: [How to fix it]

**Files to Change**:
- `path/to/file.ext` - [What to change]

**Testing**:
- [ ] Verify bug no longer reproduces
- [ ] Add regression test
- [ ] Check related scenarios

---

## 📊 Progress

### Investigation
- [x] Bug reproduced
- [x] Root cause identified
- [ ] Fix approach validated

### Implementation
- [ ] Fix implemented
- [ ] Tests added
- [ ] Verified fix works

### Verification
- [ ] Regression test passes
- [ ] No new bugs introduced
- [ ] Related bugs checked

---

## 🚀 Next Steps

```
@ai Use .makeflow/workflows/03-execution/execute-quick.md
Feature: bug-[bug-slug]
```
```

### Step 5: Present to User

```markdown
---

## ✅ Bug Investigation Complete

**Bug**: `bug-[bug-slug]`  
**Severity**: [Level]  
**Work Folder**: `.makeflow/work/bug-[bug-slug]/`

---

## 🎯 Summary

**Root Cause**: [If known]

**Fix Complexity**: [Simple/Medium/Complex]

**Estimated Time**: [X hours]

**Risk Level**: [Low/Medium/High]

---

## 🚀 Recommended Next Steps

**If fix is straightforward**:
```
@ai Use .makeflow/workflows/03-execution/execute-quick.md
Feature: bug-[bug-slug]
```

**If fix is complex**:
```
@ai Use .makeflow/workflows/02-planning/create-plan.md
Feature: bug-[bug-slug]
```

**If needs more investigation**:
Continue investigation, update AGENTS.md with findings

---

Ready to proceed with the fix?
```

---

## Example Usage

### Example: Production Bug

**User**:
```markdown
@codegen Use .makeflow/workflows/01-intake/from-bug.md

Bug: Users getting logged out randomly

Reproduction: Can't reproduce consistently, happens ~5% of the time

Expected: Users stay logged in for 2 hours (session timeout)

Actual: Sometimes logged out after 10-15 minutes

Environment: Production, all browsers, happens more during high traffic

Error: Server logs show "Invalid token" errors
```

**AI Response**:
```markdown
## 🔍 Initial Investigation

**Relevant Files**:
- `app/auth/token-refresh.ts` - Token refresh logic
- `app/middleware/auth.ts` - Auth middleware
- `app/config/session.ts` - Session configuration

**Potential Causes**:
1. **Race condition in token refresh** - Under high load, multiple requests might trigger simultaneous refresh attempts
2. **Token expiry mismatch** - Server and client might have different expiry calculations
3. **Redis session store issue** - Sessions might be evicted under memory pressure

**Recent Changes**:
- PR #210 updated token refresh logic 2 weeks ago
- PR #215 increased session timeout from 30min to 2hrs

**Need More Info**:
- Can you provide server logs showing the "Invalid token" error with timestamps?
- Do users see any error message when logged out?
- Correlation with deploy times or traffic spikes?

---

## 🤔 Root Cause Investigation Needed

**Hypothesis**: Token refresh race condition under high concurrency

**Why**: 
- Bug started after PR #210 (token refresh changes)
- Happens more during high traffic (concurrency indicator)
- "Invalid token" suggests token invalidation issue

**Next Steps**:
- [ ] Review token refresh implementation in PR #210
- [ ] Check for race condition protections
- [ ] Analyze server logs for timing patterns
- [ ] Add debug logging to token refresh

**Severity Assessment**: **High** (affects user experience, data not lost but frustrating)

---

## ✅ Bug Investigation Folder Created

**Bug**: `bug-random-logout`  
**Severity**: High  
**Work Folder**: `.makeflow/work/bug-random-logout/`

I've documented everything in the work folder. 

**Recommended next steps**:
1. Provide additional logs if available
2. I'll review PR #210 implementation
3. We'll add debugging and identify the race condition
4. Implement fix with proper concurrency control

Should I proceed with code review of PR #210?
```

---

## Tips for Bug Investigation

### Reproduction is Key
- Always try to reproduce first
- Document exact steps
- Note any variations
- Identify patterns (timing, environment, etc.)

### Look for Recent Changes
- Check git history for relevant files
- Review recent PRs
- Check deploy timestamps
- Correlate with when bug started

### Consider Context
- Load/traffic patterns
- Browser/environment differences
- User permissions/roles
- Data characteristics

### Severity Guidelines

**Critical (P0)** - Fix immediately:
- System down
- Data loss
- Security breach
- All users affected

**High (P1)** - Fix within 1-2 days:
- Major feature broken
- Many users affected
- Workaround difficult

**Medium (P2)** - Fix in sprint:
- Minor feature issue
- Workaround available
- Some users affected

**Low (P3)** - Fix when convenient:
- Cosmetic issue
- Rare occurrence
- Easy workaround

---

## Validation Checklist

- [ ] Bug description captured
- [ ] Reproduction steps documented
- [ ] Environment details noted
- [ ] Initial investigation performed
- [ ] Severity assessed
- [ ] Work folder created with AGENTS.md
- [ ] Next steps recommended

---

## Integration with Other Workflows

**Simple bug → Quick fix**:
```
.makeflow/workflows/03-execution/execute-quick.md
```

**Complex bug → Plan the fix**:
```
.makeflow/workflows/02-planning/create-plan.md
```

**Unknown root cause → Continue investigation**:
Keep updating `.makeflow/work/bug-[slug]/AGENTS.md` with findings

---

**End of Workflow**

