# Workflow: Complete and Archive

**Stage**: 04 - Delivery  
**Purpose**: Summarize work and move to history  
**Time**: 5-10 minutes  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ PR is merged
- ✅ Feature is deployed
- ✅ Work is complete
- ✅ Ready to archive work folder

---

## Prerequisites

- [ ] PR merged to main
- [ ] Feature deployed (if applicable)
- [ ] Work folder exists (`.makeflow/work/[feature-name]/`)
- [ ] All tasks complete

---

## Instructions for AI Agent

### Step 1: Verify Completion

**Check that**:
- [ ] PR is merged
- [ ] All acceptance criteria met
- [ ] Tests passing in main
- [ ] No outstanding issues
- [ ] Documentation updated

### Step 2: Create Summary

Create `.makeflow/history/[YYYY-MM-DD]-[feature-name]/SUMMARY.md`:

```markdown
# [Feature/Fix Name]

**Completed**: [YYYY-MM-DD]  
**Type**: [Feature/Bug Fix/Refactor]  
**Ticket**: [TICKET-ID]  
**PR**: #[PR-NUMBER]

---

## What Was Built

[2-3 sentences describing what was delivered]

---

## Impact

**Users Affected**: [Who benefits]

**Value Delivered**:
- [Benefit 1]
- [Benefit 2]

**Metrics** (if applicable):
- [Metric 1]: [Value]
- [Metric 2]: [Value]

---

## Implementation Summary

**Approach**: [High-level technical approach]

**Key Components**:
- [Component/file 1]
- [Component/file 2]

**Test Coverage**: [X% or X tests added]

---

## Files Changed

**Added**:
- `path/to/new-file.ext` - [Purpose]

**Modified**:
- `path/to/modified.ext` - [Changes]

**Total**: [X files changed, Y insertions, Z deletions]

---

## Decisions Made

### [Decision 1]
**What**: [Decision]  
**Why**: [Rationale]

### [Decision 2]
**What**: [Decision]  
**Why**: [Rationale]

---

## Lessons Learned

**What Went Well**:
- [Success 1]
- [Success 2]

**Challenges**:
- [Challenge 1] → [How resolved]

**For Next Time**:
- [Improvement 1]
- [Improvement 2]

---

## Links

- **Ticket**: [URL]
- **PR**: [URL]
- **Deployed**: [URL if applicable]
- **Documentation**: [URL if updated]
```

### Step 3: Create PR Link File

Create `.makeflow/history/[YYYY-MM-DD]-[feature-name]/PR-LINK.md`:

```markdown
# PR Link

**PR**: #[PR-NUMBER]  
**URL**: [Full URL to PR]  
**Merged**: [YYYY-MM-DD]  
**Merged By**: [Person who merged]

---

## PR Stats

- **Files Changed**: [X]
- **Insertions**: [Y]
- **Deletions**: [Z]
- **Commits**: [N]
- **Comments**: [N]
- **Reviewers**: [Names]
```

### Step 4: Create Changes File

Create `.makeflow/history/[YYYY-MM-DD]-[feature-name]/CHANGES.md`:

```markdown
# Changes

## Files Added ([N])

- `path/to/file1.ext` - [One-line description]
- `path/to/file2.ext` - [One-line description]

## Files Modified ([N])

- `path/to/file3.ext` - [What changed]
- `path/to/file4.ext` - [What changed]

## Files Deleted ([N])

- `path/to/old-file.ext` - [Why removed]

---

## Key Changes

### [Area 1]
- [Change description]
- **Files**: `file1.ext`, `file2.ext`

### [Area 2]
- [Change description]
- **Files**: `file3.ext`

---

## Test Coverage

**Tests Added**: [X]  
**Tests Modified**: [Y]  
**Coverage**: [Z%] → [N%]

**Test Files**:
- `path/to/test1.test.ext`
- `path/to/test2.test.ext`
```

### Step 5: Update History INDEX

Update `.makeflow/history/INDEX.md`:

Add entry to appropriate month section:

```markdown
### [YYYY-MM]

#### [YYYY-MM-DD]: [Feature Name]
- **Summary**: [One-line description]
- **PR**: #[PR-NUMBER]
- **Ticket**: [TICKET-ID]
- **Details**: [[YYYY-MM-DD]-[feature-name]/](YYYY-MM-DD-feature-name/)
- **Impact**: [Brief impact statement]
- **Changes**: [X files, Y lines]
```

Update statistics:

```markdown
## Statistics

- **Total Features**: [X]
- **Total Bug Fixes**: [Y]
- **Total Changes**: [Z]
```

### Step 6: Delete Work Folder

**After verifying history is created**:

```bash
# Remove work folder
rm -rf .makeflow/work/[feature-name]

# Commit history
git add .makeflow/history/
git commit -m "docs: Archive [feature-name] to history

- Summary created
- PR linked
- Changes documented
- Work folder cleaned up"

git push
```

### Step 7: Present Completion

```markdown
---

## ✅ Work Complete & Archived

**Feature**: [feature-name]  
**PR**: #[PR-NUMBER] (merged)  
**Completed**: [YYYY-MM-DD]

---

### 📊 Summary

**What Was Delivered**:
[Brief description]

**Impact**:
[Who benefits and how]

**Stats**:
- Files Changed: [X]
- Tests Added: [Y]
- Documentation: Updated

---

### 📚 History Archived

**Location**: `.makeflow/history/[YYYY-MM-DD]-[feature-name]/`

**Files Created**:
- `SUMMARY.md` - Complete summary
- `PR-LINK.md` - PR reference
- `CHANGES.md` - Detailed changes

**History INDEX**: Updated with entry

---

### 🧹 Cleanup

**Work Folder**: Deleted (`.makeflow/work/[feature-name]/`)  
**Repository**: Clean and organized

---

### 🎉 Done!

This feature is complete, merged, documented, and archived.

**View History**:
```
cat .makeflow/history/INDEX.md
```

**View Details**:
```
ls .makeflow/history/[YYYY-MM-DD]-[feature-name]/
```

---

Great work! Ready for the next feature? 🚀
```

---

## Example: Completing Resource Multi-Filter

### SUMMARY.md
```markdown
# Resource Multi-Criteria Filtering

**Completed**: 2025-12-09  
**Type**: Feature  
**Ticket**: ASG-145  
**PR**: #234

---

## What Was Built

Added multi-select filtering to the resources table, allowing administrators to filter by multiple types, statuses, and locations simultaneously using AND logic. Filters persist in URL params for shareable filtered views.

---

## Impact

**Users Affected**: All administrators generating resource reports

**Value Delivered**:
- Eliminates need to export to Excel for multi-criteria filtering
- Reduces report generation time from ~5 minutes to ~30 seconds
- Enables shareable filtered views via URL

**Metrics**:
- Filter performance: < 500ms with 1500 resources
- Test coverage: +12% (78% → 90%)
- Files affected: 4 files, 324 insertions, 12 deletions

---

## Implementation Summary

**Approach**: Extended @tanstack/react-table filtering with multi-select components and compound WHERE logic

**Key Components**:
- `app/components/filters/ResourceFilters.tsx` - Multi-select UI
- `app/lib/filters.ts` - Compound filter logic
- `app/routes/dashboard.resources.tsx` - Integration

**Test Coverage**: 90% (12 new tests)

---

## Decisions Made

### AND Logic Only (Initial Release)
**What**: Filters use AND logic (all conditions must match)  
**Why**: Covers 95% of admin use cases; simpler UX; OR logic adds UI complexity

### URL Param State Management
**What**: Store filter state in URL search params  
**Why**: Enables shareable links; bookmarkable views; back button works naturally

### Debounced Filter Updates (300ms)
**What**: Filter application debounced by 300ms  
**Why**: Prevents excessive re-renders; improves performance with large datasets

---

## Lessons Learned

**What Went Well**:
- Reusing existing MultiSelect component saved 2 hours
- Performance testing early prevented late optimization
- URL param approach worked perfectly

**Challenges**:
- Initial performance issues with 1000+ resources → solved with memoization
- URL param encoding edge cases → added comprehensive tests

**For Next Time**:
- Test with large datasets earlier
- Consider OR logic requirement upfront
- Add performance benchmarks to CI

---

## Links

- **Ticket**: [ASG-145](https://linear.app/team/ASG-145)
- **PR**: [#234](https://github.com/org/repo/pull/234)
- **Deployed**: https://app.example.com/resources
- **Documentation**: Updated in PR
```

---

## Tips for Good Summaries

### ✅ DO:
- Be concise but complete
- Include metrics and impact
- Document key decisions
- Capture lessons learned
- Link all related work

### ❌ DON'T:
- Copy entire work folder content
- Skip the "why" behind decisions
- Forget about lessons learned
- Leave out metrics
- Write excessively long summaries

---

## Validation Checklist

- [ ] PR confirmed merged
- [ ] Feature confirmed deployed
- [ ] History folder created with date prefix
- [ ] SUMMARY.md created (concise, complete)
- [ ] PR-LINK.md created
- [ ] CHANGES.md created
- [ ] INDEX.md updated with new entry
- [ ] Statistics updated in INDEX.md
- [ ] Work folder deleted
- [ ] Changes committed and pushed
- [ ] User notified of completion

---

## Integration with Other Workflows

**Start next feature**:
```
.makeflow/workflows/01-intake/from-ticket.md
```

or

```
.makeflow/workflows/01-intake/from-idea.md
```

**Update documentation**:
```
.makeflow/workflows/04-delivery/update-docs.md
```

---

**End of Workflow**

