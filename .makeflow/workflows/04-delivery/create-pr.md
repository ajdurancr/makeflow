# Workflow: Create Pull Request

**Stage**: 04 - Delivery  
**Purpose**: Create production-ready pull request  
**Time**: 10-15 minutes  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ Feature/fix is complete and tested
- ✅ All acceptance criteria met
- ✅ Ready for team review
- ✅ Code is on a feature branch

---

## Prerequisites

- [ ] All code committed to feature branch
- [ ] Tests passing
- [ ] Work documented in `.makeflow/work/[feature-name]/`

---

## Instructions for AI Agent

### Step 1: Pre-PR Checklist

**Verify before creating PR**:

```markdown
## 🔍 Pre-PR Checklist

Verifying readiness...

- [ ] All tests passing
- [ ] No linting errors
- [ ] No TypeScript/type errors
- [ ] Code follows project conventions
- [ ] All acceptance criteria met
- [ ] Documentation updated
- [ ] No console errors
- [ ] Commits are clean and descriptive
```

**If any checks fail**: Address them before proceeding

### Step 2: Generate PR Description

Create comprehensive PR description:

```markdown
## [Feature/Fix Name]

### 🎯 What

[One paragraph describing what this PR does]

**Related**: 
- Ticket: [TICKET-ID]
- makeflow: `.makeflow/work/[feature-name]/`

---

### 🔧 Changes

**Added**:
- [New feature/file 1]
- [New feature/file 2]

**Modified**:
- [Changed file/feature 1]
- [Changed file/feature 2]

**Removed**:
- [Deleted code/feature, if any]

---

### ✅ Acceptance Criteria

- [x] [Criterion 1]
- [x] [Criterion 2]
- [x] [Criterion 3]

---

### 🧪 Testing

**Test Coverage**:
- Unit tests: [X new tests]
- Integration tests: [X new tests]
- E2E tests: [X new tests, if applicable]
- Coverage: [X%]

**Manual Testing**:
- [x] [Test scenario 1]
- [x] [Test scenario 2]

**How to Test**:
1. [Step 1]
2. [Step 2]
3. [Expected result]

---

### 📸 Screenshots/Demo

[If UI changes, include screenshots or GIF]

**Before**:
[Screenshot or description]

**After**:
[Screenshot or description]

---

### 📝 Implementation Notes

**Technical Approach**:
- [Key technical decision 1]
- [Key technical decision 2]

**Challenges & Solutions**:
- **Challenge**: [Problem encountered]
- **Solution**: [How it was solved]

**Design Decisions**:
- [Decision 1 and rationale]
- [Decision 2 and rationale]

---

### 📚 Documentation

**Updated**:
- [ ] Code comments
- [ ] README
- [ ] API docs
- [ ] User guide

**Links**:
- [Link to updated docs]

---

### ⚠️ Notes for Reviewers

**Review Focus**:
- [Area to pay special attention to]
- [Specific concern or question]

**Known Limitations**:
- [Limitation 1, if any]
- [Planned follow-up work]

---

### 🔗 Links

- **Ticket**: [URL]
- **Design**: [URL, if applicable]
- **Related PRs**: [URLs, if any]
- **Deployment**: [Staging URL, if applicable]
```

### Step 3: Create the PR

**Execute PR creation**:
```bash
# Ensure branch is pushed
git push origin [branch-name]

# Create PR (using CLI or API)
gh pr create \
  --title "[Type]: [Short description]" \
  --body "[PR description from Step 2]" \
  --label "[appropriate labels]"
```

**PR Title Format**:
- `feat: Add multi-select filtering to resources`
- `fix: Handle null location in resource card`
- `refactor: Extract email validation to utility`
- `docs: Update API documentation`

### Step 4: Update Work Folder

Update `.makeflow/work/[feature-name]/AGENTS.md`:

```markdown
## 🔗 Related Links

- **Ticket**: [TICKET-ID] - [URL]
- **PR**: #[PR-NUMBER] - [URL]
- **Branch**: [branch-name]

---

## 📊 Current Progress

**Status**: 👀 In Review

### Completed
- [x] All features implemented
- [x] Tests added and passing
- [x] Documentation updated
- [x] PR created and ready for review

### Pending
- [ ] Code review
- [ ] PR approved
- [ ] Merged to main
- [ ] Work summarized to history
```

### Step 5: Present PR to User

```markdown
---

## ✅ Pull Request Created

**PR**: #[NUMBER] - [Title]  
**URL**: [Link to PR]

**Branch**: `[branch-name]` → `main`

---

### 📊 PR Summary

**What**: [One sentence summary]

**Changes**:
- [X files changed]
- [X insertions], [X deletions]

**Testing**:
- ✅ [X] tests added
- ✅ All tests passing
- ✅ Manual testing complete

**Documentation**:
- ✅ Updated

---

### 👀 Next Steps

1. **Code Review**: Share PR with team
2. **Address Feedback**: Make any requested changes
3. **Merge**: Once approved
4. **Complete Workflow**:

```
@ai Use .makeflow/workflows/04-delivery/complete.md
Feature: [feature-name]
```

---

### 📝 PR Description

[Show full PR description]

---

Ready for review! 🚀
```

---

## Example PR

### Example: Multi-Select Resource Filtering

**Title**: `feat: Add multi-criteria filtering to resources table`

**Description**:
```markdown
## Multi-Criteria Resource Filtering

### 🎯 What

Adds multi-select filtering to the resources table, allowing administrators to filter by multiple types, statuses, and locations simultaneously. This eliminates the need to export to Excel for filtered reports.

**Related**: 
- Ticket: ASG-145
- makeflow: `.makeflow/work/resource-multi-filter/`

---

### 🔧 Changes

**Added**:
- Multi-select filter components for Type, Status, Location columns
- Compound filter logic with AND conditions
- "Clear all filters" button
- Filtered count display ("Showing X of Y resources")
- URL param persistence for shareable filtered views

**Modified**:
- `app/routes/dashboard.resources.tsx` - Integrated filters
- `app/lib/filters.ts` - Filter logic
- `app/components/ui/multi-select.tsx` - Extended for table use

---

### ✅ Acceptance Criteria

- [x] Can select multiple types (e.g., Equipment + Tools)
- [x] Can select multiple statuses (e.g., Active + Maintenance)
- [x] Can combine Type + Status + Location filters
- [x] Filter results update in < 500ms with 1000+ resources
- [x] URL params reflect active filters (shareable)
- [x] Clear filters button resets to unfiltered view
- [x] Shows "Showing X of Y resources" count

---

### 🧪 Testing

**Test Coverage**:
- Unit tests: 12 new tests (filter logic, components)
- Integration tests: 4 tests (table integration)
- Performance: Tested with 1500 resources (avg 320ms)

**Manual Testing**:
- [x] Applied various filter combinations
- [x] Verified URL params update correctly
- [x] Tested with large dataset (1500 resources)
- [x] Clear filters works correctly
- [x] Filters persist on page reload

**How to Test**:
1. Go to Resources page
2. Click Type filter, select "Equipment" and "Tools"
3. Click Status filter, select "Active"
4. Verify only Equipment and Tools with Active status show
5. Check URL has `?type=Equipment,Tools&status=Active`
6. Click "Clear filters" - all resources shown

---

### 📸 Screenshots

**Before**:
Single-select dropdowns, one filter at a time

**After**:
Multi-select dropdowns, multiple active filters, clear button, count display

[Screenshot showing new UI]

---

### 📝 Implementation Notes

**Technical Approach**:
- Extended existing @tanstack/react-table filtering
- Reused MultiSelect component with table-specific styling
- Filter state managed in URL search params
- Prisma queries use compound WHERE with AND logic

**Challenges & Solutions**:
- **Challenge**: Performance with 1000+ resources
- **Solution**: Memoized filter function, debounced updates (300ms)

**Design Decisions**:
- AND logic for filters (all conditions must match)
- Rationale: Most common admin use case
- OR logic considered but added complexity; can add later if needed

---

### 📚 Documentation

**Updated**:
- [x] Component comments
- [x] Filter utilities docs
- [ ] User guide (will update after merge)

---

### ⚠️ Notes for Reviewers

**Review Focus**:
- Filter logic in `app/lib/filters.ts` (complex conditionals)
- Performance with large datasets
- URL param encoding/decoding

**Known Limitations**:
- Currently only supports AND logic between filters
- Future: Add OR option or saved filter presets

---

### 🔗 Links

- **Ticket**: ASG-145
- **Design**: [Figma link]
- **Staging**: https://staging.app.com/resources
```

---

## Tips for Great PRs

### ✅ DO:
- Write clear, descriptive title
- Explain the "why" not just "what"
- Include testing instructions
- Add screenshots for UI changes
- Document decisions and trade-offs
- Link to related work
- Keep PR focused and sized appropriately

### ❌ DON'T:
- Create giant PRs (> 500 lines)
- Skip testing section
- Forget to update documentation
- Mix unrelated changes
- Use vague descriptions
- Ignore PR template
- Forget to link ticket

---

## PR Size Guidelines

**Small** (< 100 lines):
- Quick review, easy to approve
- Ideal size

**Medium** (100-500 lines):
- Reasonable review time
- Acceptable

**Large** (500-1000 lines):
- Consider splitting
- Add extra context in description
- May need multiple reviewers

**Extra Large** (> 1000 lines):
- Should be split into multiple PRs
- Hard to review effectively
- Higher risk of issues

---

## Validation Checklist

- [ ] All tests passing
- [ ] No linting/type errors
- [ ] PR description complete
- [ ] Screenshots added (if UI changes)
- [ ] Testing instructions provided
- [ ] Documentation updated
- [ ] Ticket linked
- [ ] Work folder updated with PR link
- [ ] PR created successfully
- [ ] User has PR link

---

## Integration with Other Workflows

**After PR created**:
```
.makeflow/workflows/04-delivery/complete.md
```

**If changes requested**:
Make changes, push commits, update PR

**If need to update docs**:
```
.makeflow/workflows/04-delivery/update-docs.md
```

---

**End of Workflow**

