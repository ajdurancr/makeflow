# Workflow: Update Documentation

**Stage**: 04 - Delivery  
**Purpose**: Update project documentation for changes  
**Time**: 15-30 minutes  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ Feature adds new APIs or components
- ✅ Feature changes existing behavior
- ✅ User guide needs updates
- ✅ README or technical docs affected

---

## Prerequisites

- [ ] Feature is implemented
- [ ] You understand what needs documenting
- [ ] You know where docs are located

---

## Instructions for AI Agent


### Step 0: Review Project Documentation Index (if available)

**Before identifying documentation needs**, check if `.makeflow/project/index.md` exists:
- **If it exists**: Review it to understand what documentation exists in this project and where it lives
- **Purpose**: This helps you identify which documentation files need to be updated based on the project's documentation structure
- **What to look for**: Documentation locations, existing guides, API reference locations, update procedures

---

### Step 0.5: Validate Current Documentation State

**Purpose**: Ensure indexes are up-to-date before making changes to prevent compounding existing documentation drift.

**Run validation checks** to compare actual files against indexes:

**Check 1: Verify index references are valid**

```bash
# Check for broken links in docs/README.md
echo "=== Validating docs/README.md links ==="
if [ -f "docs/README.md" ]; then
  grep -o '\[.*\](\.\/.*\.md)' docs/README.md | sed 's/.*](\.\/\(.*\))/\1/' | while read file; do
    if [ ! -f "docs/$file" ]; then
      echo "❌ Broken link: docs/$file"
    fi
  done
fi

# Check for broken references in .makeflow/project/index.md
echo "=== Validating .makeflow/project/index.md references ==="
if [ -f ".makeflow/project/index.md" ]; then
  grep -o '\`\.\./\.\./docs/.*\.md\`' .makeflow/project/index.md | tr -d '`' | while read file; do
    if [ ! -f "$file" ]; then
      echo "❌ Broken reference: $file"
    fi
  done
fi
```

**Check 2: Find potentially undocumented files**

```bash
# List documentation files not in main README
echo "=== Checking for undocumented files ==="
find docs/ -type f -name "*.md" \
  ! -name "README.md" \
  ! -path "*/templates/*" \
  ! -path "*/archive/*" \
  ! -path "*/node_modules/*" \
  ! -path "*/.git/*" \
  | sort
```

**Report to user**:

```markdown
## 📋 Pre-Update Documentation Validation

### Validation Results
- Broken links in docs/README.md: [N]
- Broken references in .makeflow/project/index.md: [M]
- Potentially undocumented files: [X]

### Status
[✅ No issues found - indexes are synchronized]
OR
[⚠️  Found [N+M+X] inconsistencies in documentation indexes]
```

**If inconsistencies found**:
- Show list of issues
- Ask: "Should we fix these before updating docs for current feature?"
- If user approves:
  - Fix broken links (remove or update)
  - Add missing files to indexes (with user guidance)
  - Commit fixes separately before proceeding with feature documentation

**Why this matters**:
- Prevents compounding existing documentation drift
- Ensures new documentation is added to clean, consistent indexes
- Makes it easier to track what was added for this specific feature
- Builds good documentation hygiene habits

---

### Step 1: Identify Documentation Needs

**Determine what needs updating**:

```markdown
## 📚 Documentation Assessment

**Feature**: [feature-name]

**Documentation Needed**:
- [ ] **README** - High-level project docs
- [ ] **API Documentation** - New/changed endpoints
- [ ] **Component Docs** - New components
- [ ] **User Guide** - End-user instructions
- [ ] **Setup/Install** - Installation changes
- [ ] **Examples** - Usage examples
- [ ] **Migration Guide** - Breaking changes
- [ ] **Changelog** - Version history
```

### Step 2: Update Each Documentation Type

#### README Updates

**What to add**:
- New features in features list
- Usage examples
- New dependencies
- Breaking changes

**Example**:
```markdown
## Features

- ✅ Multi-select filtering
- ✅ URL-based filter persistence
- ✅ [NEW] Multi-criteria resource filtering
```

#### API Documentation

**For new endpoints**:
```markdown
### POST /api/resources/filter

Filter resources by multiple criteria.

**Request**:
```json
{
  "types": ["Equipment", "Tools"],
  "statuses": ["Active"],
  "locations": ["Building A"]
}
```

**Response**:
```json
{
  "resources": [...],
  "count": 42,
  "total": 156
}
```

**Example**:
```bash
curl -X POST /api/resources/filter \
  -H "Content-Type: application/json" \
  -d '{"types": ["Equipment"]}'
```
```

#### Component Documentation

**For new components**:
```markdown
## ResourceFilters

Multi-select filter component for resources table.

**Props**:
```typescript
interface ResourceFiltersProps {
  types: string[];
  statuses: string[];
  locations: string[];
  onFilterChange: (filters: FilterState) => void;
}
```

**Usage**:
```tsx
<ResourceFilters
  types={selectedTypes}
  statuses={selectedStatuses}
  locations={selectedLocations}
  onFilterChange={handleFilterChange}
/>
```

**Example**:
[Link to Storybook or live example]
```

#### User Guide

**For end users**:
```markdown
## Filtering Resources

### Multi-Criteria Filtering

You can now filter resources by multiple criteria simultaneously:

1. Click the **Type** filter dropdown
2. Select one or more types (e.g., Equipment, Tools)
3. Click the **Status** filter dropdown
4. Select one or more statuses (e.g., Active, Maintenance)
5. Resources update automatically

**Tips**:
- All selected filters must match (AND logic)
- Share filtered views by copying the URL
- Click "Clear all filters" to reset
- The count shows "Showing X of Y resources"

**Screenshot**: [Add screenshot showing filters]
```

#### Changelog

**Add entry**:
```markdown
## [Version X.Y.Z] - YYYY-MM-DD

### Added
- Multi-criteria filtering for resources table (#234)
- URL parameter persistence for filters
- Clear all filters button

### Changed
- Resources table now supports compound filters

### Performance
- Filter updates optimized for datasets > 1000 items
```

### Step 3: Add Examples

**Create or update examples**:

```markdown
## Examples

### Filtering Resources by Multiple Criteria

```typescript
// Example: Filter by equipment that is active
const filters = {
  types: ['Equipment'],
  statuses: ['Active']
};

const filteredResources = await filterResources(filters);
// Returns only Equipment that is Active
```

### Sharing Filtered Views

```
# Share this URL with your team
https://app.com/resources?types=Equipment,Tools&status=Active

# Anyone opening this link will see the filtered view
```
```

### Step 4: Check for Broken Links

**Verify**:
- [ ] All internal links work
- [ ] External links valid
- [ ] Code examples are accurate
- [ ] Screenshots up-to-date

### Step 5: Update makeflow Work Folder

Update `.makeflow/work/[feature-name]/AGENTS.md`:

```markdown
## 📚 Documentation

**Updated**:
- [x] README.md - Added to features list
- [x] docs/api.md - Documented new endpoint
- [x] docs/components.md - Added ResourceFilters docs
- [x] docs/user-guide.md - Added filtering section
- [x] CHANGELOG.md - Added v1.2.0 entry

**Locations**:
- [List paths to updated docs]
```

---

### Step 6: Update Documentation Indexes

**Purpose**: Ensure all documentation updates are reflected in indexes.

**After updating documentation files**, verify they are properly indexed:

**Check for new documentation files**:

```bash
# Find markdown files added in this feature
echo "=== New documentation files in this feature ==="
git diff --name-status main...HEAD | grep "^A.*\.md$" | awk '{print $2}' | grep "^docs/"
```

**For each new file found**:
1. **Check if listed in `docs/README.md`**:
   ```bash
   # Check if file is referenced
   NEW_FILE="patterns/new-pattern.md"  # example
   grep "$NEW_FILE" docs/README.md
   ```
2. **Check if listed in `.makeflow/project/index.md`**:
   ```bash
   grep "$NEW_FILE" .makeflow/project/index.md
   ```
3. **If missing**, add appropriate reference with description:
   - In `docs/README.md`: Add as markdown link with description
   - In `.makeflow/project/index.md`: Add to appropriate category section

**Check for moved/renamed files**:

```bash
# Find renamed or moved markdown files
echo "=== Moved/renamed documentation files in this feature ==="
git diff --name-status main...HEAD | grep "^R.*\.md$" | grep "docs/"
```

**For each moved/renamed file**:
1. **Update paths in `docs/README.md`**:
   - Find old path references
   - Replace with new path
2. **Update paths in `.makeflow/project/index.md`**:
   - Find old path references
   - Replace with new path
3. **Check for internal links** that may need updating:
   ```bash
   # Find files that link to the moved file
   OLD_PATH="old-location/file.md"
   grep -r "\($OLD_PATH\)" docs/ --include="*.md"
   ```

**Check for removed files**:

```bash
# Find deleted markdown files
echo "=== Removed documentation files in this feature ==="
git diff --name-status main...HEAD | grep "^D.*\.md$" | grep "docs/"
```

**For each removed file**:
1. **Remove from `docs/README.md`** - Delete link entry
2. **Remove from `.makeflow/project/index.md`** - Delete reference
3. **Check for broken internal links**:
   ```bash
   # Find files that still link to the removed file
   REMOVED_FILE="removed-file.md"
   grep -r "\($REMOVED_FILE\)" docs/ --include="*.md"
   ```

**Validate: Run final index scan**:

```bash
# Quick validation after updates
echo "=== Final validation ==="

# Check for broken links
echo "Checking docs/README.md..."
grep -o '\[.*\](\.\/.*\.md)' docs/README.md | sed 's/.*](\.\/\(.*\))/\1/' | while read file; do
  if [ ! -f "docs/$file" ]; then
    echo "❌ Broken link: docs/$file"
  fi
done

echo "Checking .makeflow/project/index.md..."
grep -o '\`\.\./\.\./docs/.*\.md\`' .makeflow/project/index.md | tr -d '`' | while read file; do
  if [ ! -f "$file" ]; then
    echo "❌ Broken reference: $file"
  fi
done

echo "✅ Validation complete"
```

**If validation finds issues**:
- Fix them before proceeding
- Re-run validation
- Repeat until no issues remain

**Commit index updates**:

```bash
# Commit documentation and index changes together
git add docs/ .makeflow/project/index.md
git commit -m "docs: Update documentation for [feature-name]

Updated documentation:
- Added/Updated [list files]
- Updated indexes to reflect new/moved/removed files
- All links validated and working

Indexes synchronized:
- docs/README.md
- .makeflow/project/index.md"
```

---

### Step 7: Present Documentation Updates

```markdown
---

## ✅ Documentation Updated

**Feature**: [feature-name]

### Files Updated:
- `README.md` - [What was added]
- `docs/api.md` - [What was added]
- `docs/user-guide.md` - [What was added]
- `CHANGELOG.md` - [Version entry]

### What Was Documented:
- ✅ API endpoints
- ✅ Component usage
- ✅ User instructions
- ✅ Code examples
- ✅ Changelog entry

---

## 📝 Documentation Summary

**For Developers**:
- API documentation in `docs/api.md`
- Component docs in `docs/components.md`
- Examples in `docs/examples.md`

**For End Users**:
- User guide in `docs/user-guide.md`
- Screenshots added

**Changelog**:
- Version X.Y.Z entry added

---

## 🚀 Next Steps

**If PR not created yet**:
```
@ai Use .makeflow/workflows/04-delivery/create-pr.md
Feature: [feature-name]
```

**If PR exists**:
Push documentation updates to same branch

**If ready to complete**:
```
@ai Use .makeflow/workflows/04-delivery/complete.md
Feature: [feature-name]
```

---

Ready to proceed?
```

---

## Documentation Validation Commands

**Quick Reference**: Reusable bash commands for validating documentation indexes.

### Check for Broken Links

**In docs/README.md**:
```bash
# Extract and validate all relative markdown links
grep -o '\[.*\](\.\/.*\.md)' docs/README.md | sed 's/.*](\.\/\(.*\))/\1/' | while read file; do
  if [ ! -f "docs/$file" ]; then
    echo "❌ Broken link in docs/README.md: $file"
  else
    echo "✅ Valid: $file"
  fi
done
```

**In .makeflow/project/index.md**:
```bash
# Extract and validate all documentation references
grep -o '\`\.\./\.\./docs/.*\.md\`' .makeflow/project/index.md | tr -d '`' | while read file; do
  if [ ! -f "$file" ]; then
    echo "❌ Broken reference in index.md: $file"
  else
    echo "✅ Valid: $file"
  fi
done
```

### Find Undocumented Files

**List all documentation files**:
```bash
# Find all .md files excluding special files
find docs/ -type f -name "*.md" \
  ! -name "README.md" \
  ! -path "*/templates/*" \
  ! -path "*/archive/*" \
  ! -path "*/node_modules/*" \
  ! -path "*/.git/*" \
  ! -name ".gitkeep" \
  | sort
```

**Compare against indexes** (manual review):
```bash
# Save actual files to temp file
find docs/ -type f -name "*.md" ! -name "README.md" | sort > /tmp/actual-docs.txt

# Extract referenced files from README
grep -o '\[.*\](\.\/.*\.md)' docs/README.md | sed 's/.*](\.\/\(.*\))/docs\/\1/' | sort > /tmp/indexed-docs.txt

# Show files not in index
echo "=== Files not referenced in docs/README.md ==="
comm -23 /tmp/actual-docs.txt /tmp/indexed-docs.txt
```

### Check Git Changes

**Find documentation files changed in current branch**:
```bash
# Compare against main branch
git diff --name-only main...HEAD | grep '^docs/.*\.md$'
```

**Find new documentation files**:
```bash
git diff --name-status main...HEAD | grep "^A.*\.md$" | awk '{print $2}' | grep "^docs/"
```

**Find moved/renamed files**:
```bash
git diff --name-status main...HEAD | grep "^R.*\.md$" | grep "docs/"
```

**Find deleted files**:
```bash
git diff --name-status main...HEAD | grep "^D.*\.md$" | grep "docs/"
```

### Full Validation Script

**Complete validation** (run before committing documentation changes):

```bash
#!/bin/bash
# Comprehensive documentation validation

echo "═══════════════════════════════════════"
echo "📚 Documentation Index Validation"
echo "═══════════════════════════════════════"

ERRORS=0

# Check 1: Broken links in docs/README.md
echo ""
echo "1️⃣  Checking docs/README.md for broken links..."
if [ -f "docs/README.md" ]; then
  BROKEN=$(grep -o '\[.*\](\.\/.*\.md)' docs/README.md | sed 's/.*](\.\/\(.*\))/\1/' | while read file; do
    if [ ! -f "docs/$file" ]; then
      echo "❌ Broken: docs/$file"
      ((ERRORS++))
    fi
  done)
  
  if [ -z "$BROKEN" ]; then
    echo "✅ All links valid"
  else
    echo "$BROKEN"
  fi
else
  echo "⚠️  docs/README.md not found"
fi

# Check 2: Broken references in .makeflow/project/index.md
echo ""
echo "2️⃣  Checking .makeflow/project/index.md for broken references..."
if [ -f ".makeflow/project/index.md" ]; then
  BROKEN=$(grep -o '\`\.\./\.\./docs/.*\.md\`' .makeflow/project/index.md | tr -d '`' | while read file; do
    if [ ! -f "$file" ]; then
      echo "❌ Broken: $file"
      ((ERRORS++))
    fi
  done)
  
  if [ -z "$BROKEN" ]; then
    echo "✅ All references valid"
  else
    echo "$BROKEN"
  fi
else
  echo "⚠️  .makeflow/project/index.md not found"
fi

# Check 3: Find potentially undocumented files
echo ""
echo "3️⃣  Checking for potentially undocumented files..."
UNDOCUMENTED=$(find docs/ -type f -name "*.md" ! -name "README.md" ! -path "*/templates/*" ! -path "*/archive/*" ! -path "*/.*" | sort)
if [ -z "$UNDOCUMENTED" ]; then
  echo "✅ No documentation files found (or all indexed)"
else
  echo "Found these documentation files (verify they're indexed):"
  echo "$UNDOCUMENTED"
fi

# Check 4: Check for files changed in current branch
echo ""
echo "4️⃣  Checking for documentation changes in current branch..."
CHANGED=$(git diff --name-only HEAD main 2>/dev/null | grep '^docs/.*\.md$' || echo "")
if [ -z "$CHANGED" ]; then
  echo "✅ No documentation changes in current branch"
else
  echo "Changed files (ensure indexes are updated):"
  echo "$CHANGED"
fi

# Summary
echo ""
echo "═══════════════════════════════════════"
if [ $ERRORS -eq 0 ]; then
  echo "✅ Validation complete - no errors found"
else
  echo "❌ Validation found $ERRORS error(s)"
  echo "Please fix broken links before committing"
  exit 1
fi
echo "═══════════════════════════════════════"
```

**Save as**: `.makeflow/scripts/validate-docs.sh` and make executable:
```bash
chmod +x .makeflow/scripts/validate-docs.sh
```

---

## Documentation Best Practices

### When to Update Indexes

**ALWAYS update indexes when**:
- ✅ Creating new documentation files in `docs/patterns/`, `docs/specs/`, `docs/workflows/`, or `docs/decisions/`
- ✅ Moving documentation files to new locations (e.g., `docs/file.md` → `docs/patterns/file.md`)
- ✅ Renaming documentation files (e.g., `old-name.md` → `new-name.md`)
- ✅ Removing or archiving documentation files
- ✅ Changing documentation organization or structure (e.g., reorganizing patterns)
- ✅ Creating new documentation categories (e.g., adding `docs/guides/`)

**Indexes to keep synchronized**:
- 📄 `docs/README.md` - Main documentation hub (user-facing, human-readable)
- 🤖 `.makeflow/project/index.md` - AI agent reference (machine-readable, context provider)

### How to Keep Indexes Synchronized

**For each documentation change**:

1. **Update the file itself** - Make your documentation changes
2. **Update `docs/README.md`** - If file is in a major category (patterns/specs/workflows/decisions)
   - Add link to new files
   - Update links for moved files
   - Remove links for deleted files
   - Update descriptions if content changed significantly
3. **Update `.makeflow/project/index.md`** - If file is in a major category
   - Add entries for new files with brief descriptions
   - Update paths for moved files
   - Remove entries for deleted files
   - Keep AI agent quick reference section current
4. **Test all links** - Verify both indexes have working links
5. **Commit all changes together** - Use a single commit for documentation + index updates

**Validation frequency**:
- ✅ **After any documentation changes** - Run quick validation (Step 6 in this workflow)
- ✅ **Before creating PR** - Deep validation to catch any missed updates
- ✅ **During PR reviews** - Spot check that indexes match changes
- ✅ **Monthly or before major releases** - Comprehensive audit

### Common Pitfalls to Avoid

**❌ DON'T**:
- Move files without updating index links → Results in broken links
- Add new docs without adding to indexes → New docs become "hidden" and undiscoverable
- Rename files without search-and-replace in indexes → Old references become stale
- Remove files without removing index entries → Broken links confuse users
- Create new documentation categories without updating index structure → Inconsistent organization
- Batch many doc changes without checking indexes → Compounding drift
- Assume indexes "auto-update" → They don't; manual maintenance required
- Use jargon without explanation in docs
- Skip examples in technical documentation
- Write overly long docs without structure
- Forget to update changelog
- Leave broken links after moving files
- Document implementation details users don't need

**✅ DO**:
- Update files and indexes in the same commit → Atomic changes prevent drift
- Use descriptive link text in indexes → Helps users and AI agents find relevant docs
- Keep index descriptions concise → One-line summaries are sufficient
- Link liberally within documentation → Cross-references improve navigation
- Review indexes during PR reviews → Catch issues before merge
- Run validation before committing → Proactive error detection
- Write for your audience (devs vs users)
- Include code examples
- Add screenshots for UI features
- Keep examples simple and focused
- Update changelog with every feature

### Recovery from Drift

**If indexes are out of sync after feature work**:

1. **Run full validation** - Use commands from "Documentation Validation Commands" section
2. **Identify all discrepancies**:
   - Broken links
   - Missing entries for new files
   - Stale entries for moved/removed files
3. **Fix systematically**:
   - Remove broken links first
   - Add missing files next
   - Update stale paths last
4. **Verify fixes** - Re-run validation
5. **Commit with clear message** - Explain what was synchronized

**Example recovery commit message**:
```
docs: Synchronize documentation indexes for [feature-name]

Fixed inconsistencies in documentation indexes:
- Added 2 new pattern docs to indexes
- Updated 1 file path that had moved
- Removed 1 broken link from docs/README.md

All documentation is now discoverable and properly indexed.
```

---

## Documentation Types Guide

### README.md
**Audience**: New developers, users  
**Content**: Overview, features, quick start, installation  
**Tone**: Friendly, concise

### API Documentation
**Audience**: Developers integrating with your code  
**Content**: Endpoints, parameters, responses, examples  
**Tone**: Technical, precise

### User Guide
**Audience**: End users  
**Content**: How to use features, step-by-step instructions  
**Tone**: Simple, clear, no technical jargon

### Component Documentation
**Audience**: Developers using your components  
**Content**: Props, usage, examples, edge cases  
**Tone**: Technical but helpful

### Changelog
**Audience**: All stakeholders  
**Content**: What changed, when, why (if breaking)  
**Tone**: Factual, concise

---

## Example Documentation Set

### README.md Addition
```markdown
## Features

- ✅ Resource management
- ✅ Assignment tracking
- ✅ Multi-criteria filtering (NEW)
  - Filter by type, status, and location simultaneously
  - Share filtered views via URL
  - Fast performance (< 500ms with 1000+ items)
```

### API Docs (docs/api.md)
```markdown
### Filter Resources

`POST /api/resources/filter`

Apply multiple filter criteria to resources.

**Request Body**:
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| types | string[] | No | Resource types to include |
| statuses | string[] | No | Resource statuses to include |
| locations | string[] | No | Location IDs to include |

**Response**:
```json
{
  "resources": [{ Resource object }],
  "count": 42,
  "total": 156,
  "filters": { Applied filters }
}
```

**Example**:
```bash
curl -X POST /api/resources/filter \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TOKEN" \
  -d '{
    "types": ["Equipment", "Tools"],
    "statuses": ["Active"]
  }'
```

**Errors**:
- `400` - Invalid filter parameters
- `401` - Unauthorized
- `500` - Server error
```

### User Guide (docs/user-guide.md)
```markdown
## Filtering Resources

### How to Use Multi-Criteria Filters

1. **Open the Resources page**
   
2. **Select filters**:
   - Click **Type** dropdown → select one or more types
   - Click **Status** dropdown → select one or more statuses
   - Click **Location** dropdown → select one or more locations
   
3. **View results**:
   - Results update automatically as you select filters
   - See "Showing X of Y resources" at the top
   
4. **Clear filters**:
   - Click "Clear all filters" button to reset

### Tips

- **Share filtered views**: Copy the URL and share with your team
- **Bookmark common filters**: Browser bookmarks work with filtered URLs
- **Combine any filters**: All selected filters work together (AND logic)

[Screenshot: Filters in action]
```

---

## Validation Checklist

- [ ] All relevant docs identified
- [ ] README updated (if needed)
- [ ] API docs updated (if applicable)
- [ ] User guide updated (if applicable)
- [ ] Component docs updated (if applicable)
- [ ] Examples added
- [ ] Changelog updated
- [ ] Screenshots added (for UI changes)
- [ ] Links verified
- [ ] Code examples tested
- [ ] Docs committed to feature branch
- [ ] AGENTS.md updated

---

## Integration with Other Workflows

**After docs updated**:
```
.makeflow/workflows/04-delivery/create-pr.md
```

or

```
.makeflow/workflows/04-delivery/complete.md
```

---

**End of Workflow**
