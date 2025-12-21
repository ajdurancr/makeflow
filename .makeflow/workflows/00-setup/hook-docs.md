# Workflow: Hook Existing Documentation

**Stage**: 00 - Setup  
**Purpose**: Connect makeflow to existing project documentation  
**Time**: 5-10 minutes  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ Your project already has a `docs/` folder or similar documentation
- ✅ You want makeflow workflows to understand your documentation structure
- ✅ You want AI agents to automatically find relevant docs for tasks

---

## Prerequisites

- [ ] Project has existing documentation folder (e.g., `docs/`, `documentation/`, etc.)
- [ ] You can describe the documentation organization
- [ ] Documentation follows some consistent structure

---

## Instructions for AI Agent

### Step 1: Discover Documentation Structure

**Ask the user**:
1. Where is the main documentation entry point? (e.g., `docs/README.md`, `README.md`, `documentation/index.md`)
2. What types of documentation exist? (patterns, specs, workflows, guides, API docs, etc.)
3. Are there any special folders or organization patterns?

**If user is unsure**, scan common locations:
```bash
# Check for common documentation locations
find . -maxdepth 2 -type d -name "docs" -o -name "documentation" -o -name "doc"
find . -maxdepth 2 -type f -name "README.md" -o -name "GUIDE.md" -o -name "DOCS.md"
```

---

### Step 2: Analyze Documentation

**Scan the documentation folder** and identify:

1. **Main entry point** - The primary README or index file
2. **Section categories** - Folders or groupings (e.g., `patterns/`, `specs/`, `guides/`)
3. **Key documents** - Important standalone files
4. **Organization pattern** - How files are named and organized

**Example analysis**:
```
Found documentation at: docs/
├── README.md (Main hub)
├── patterns/
│   ├── api-patterns.md
│   ├── component-patterns.md
│   └── testing-patterns.md
├── specs/
│   ├── feature-a.md
│   └── feature-b.md
├── workflows/
│   └── development.md
└── decisions/
    └── 0001-example.md

Organization pattern: Progressive/README-first approach
Categories detected: patterns, specs, workflows, decisions
```

---

### Step 3.5: Deep Scan for Documentation Files

**Purpose**: Ensure no documentation files are missed during index creation.

**Scan all markdown files** in the documentation area:

1. Find all `.md` files in the documentation root folder
2. Exclude special folders: `node_modules`, `.git`, `dist`, build artifacts
3. Sort the results for consistent ordering

**Categorize each file** found:

1. **Determine category** - Which section does it belong to?
   - Patterns (development patterns, best practices)
   - Specifications (feature specs, technical specs)
   - Workflows (processes, how-tos, guides)
   - Decisions (ADRs, architectural choices)
   - Other (guides, tutorials, reference, etc.)

2. **Extract purpose** - Get brief description from file:
   - Check first heading or front matter
   - Read first paragraph
   - Infer from filename if needed

3. **Check existing references** - Is it already indexed?
   - Search in any existing README or index files
   - Note if missing from primary documentation hub

**Create comprehensive file inventory**:

```markdown
## 📋 Documentation File Inventory

### Patterns (`docs/patterns/`)
- ✅ `patterns/api-patterns.md` - Backend API design conventions
- ✅ `patterns/component-patterns.md` - Frontend component structure
- ❌ `patterns/testing-patterns.md` - Not referenced in main README

### Specifications (`docs/specs/`)
- ✅ `specs/feature-x.md` - Feature X technical specification
- ❌ `specs/feature-y.md` - Not referenced in main README

### Workflows (`docs/workflows/`)
- ✅ `workflows/development.md` - Development process and tools
- ✅ `workflows/deployment.md` - Deployment procedures

### Decisions (`docs/decisions/`)
- ❌ `decisions/0001-use-typescript.md` - Not referenced in main README
- ❌ `decisions/0002-choose-database.md` - Not referenced in main README

### Other Files
- ✅ `README.md` - Main documentation hub
- ❌ `archive/old-guide.md` - Archived content (may not need indexing)
- ❌ `templates/template.md` - Template file (may not need indexing)

### Summary
- **Total files found**: 11
- **Referenced in existing indexes**: 5
- **Missing from indexes**: 6
- **Potential exclusions**: 2 (archive/templates)
```

**Cross-reference with existing indexes**:
- Compare inventory against `docs/README.md` (if it exists)
- Identify files present in filesystem but missing from index
- Identify files referenced in index but missing from filesystem (broken links)

**Show the inventory to the user** and ask:
- "I found [X] documentation files. [Y] are not currently indexed. Should these be added?"
- "Found [Z] broken references. Should these be removed or are files missing?"
- "Found archived/template files. Should these be excluded from the index?"

---

### Step 3: Create Documentation Index

**Create** `.makeflow/project/index.md` with the following structure:

```markdown
# Project Documentation Index

> **Entry Point**: This file helps AI agents understand where project documentation lives.

## 🏠 Main Documentation Hub

**Location**: `[RELATIVE_PATH_TO_MAIN_DOC]`

[Brief description of what the main documentation contains]

## 📚 Documentation Structure

### [Category 1] (`[RELATIVE_PATH]`)
[Description of this category]:
- **[Document 1]** → [Brief description]
- **[Document 2]** → [Brief description]

### [Category 2] (`[RELATIVE_PATH]`)
[Description of this category]:
- **[Document 1]** → [Brief description]
- **[Document 2]** → [Brief description]

[Repeat for each major category]

## 🤖 AI Agent Quick Reference

### For Implementation Tasks:
Include: `[main doc]` + `[patterns docs]` + relevant specs

### For Understanding Features:
Include: `[main doc]` + `[specs docs]` + relevant decisions

### For Process Questions:
Include: `[main doc]` + `[workflow docs]`

### For Complete Context:
Include: `[root docs folder]/**/*` (everything)

## 📝 Maintenance Notes

**Last Updated**: [YYYY-MM-DD]

**Update Triggers**: 
- New top-level documentation sections added
- Major reorganization of documentation structure
- New documentation categories created

**Low Maintenance Design**: This index describes WHERE docs live, not their detailed contents. It rarely needs updates unless the documentation structure itself changes.
```

**Template Variables to Replace**:
- `[RELATIVE_PATH_TO_MAIN_DOC]` - e.g., `../../docs/README.md`
- `[Category X]` - e.g., `Patterns`, `Specifications`, `Workflows`
- `[RELATIVE_PATH]` - e.g., `../../docs/patterns/`
- `[Document X]` - Actual document names found
- `[Brief description]` - Short description of what the doc contains
- `[YYYY-MM-DD]` - Current date

---

### Step 4: Create Documentation Index

**Create** `.makeflow/project/index.md` based on the deep scan results from Step 3.5.

Follow the structure from Step 3, but ensure ALL discovered files are represented:
- Files already indexed → Listed with descriptions
- Files missing from index → Added with descriptions
- Broken references → Removed or flagged for user attention

---

### Step 4.5: Validate Index Completeness

**Purpose**: Ensure all discovered documentation is properly indexed before finalizing.

**Check 1: Are all markdown files referenced?**

Compare the file inventory from Step 3.5 against the generated index:

1. **Get list of actual files**:
   - Find all `.md` files in documentation root
   - Exclude: `README.md`, files in `templates/`, files in `archive/`, `node_modules`, `.git`
   - Sort for consistent comparison

2. **Get list of files referenced in index**:
   - Extract all file path references from `.makeflow/project/index.md`
   - Parse out the actual paths (typically in format `` `../../docs/path/to/file.md` ``)
   - Sort for consistent comparison

3. **Find files not in index**:
   - Compare the two lists
   - Identify files that exist in filesystem but not in index
   
4. **Report results**:
   - If files missing: "⚠️ Files missing from index: [list]"
   - If all indexed: "✅ All files are indexed"

**If files are missing from index**:
- List them for the user
- Ask: "Should these be added to the index?"
- If yes → Update `.makeflow/project/index.md` and `docs/README.md` (if applicable)
- If no → Document why they're excluded (e.g., templates, drafts, archives)

**Check 2: Are there broken references?**

Verify all files referenced in the index actually exist:

1. **Check references in `.makeflow/project/index.md`**:
   - Extract all file path references (format: `` `../../docs/path/to/file.md` ``)
   - For each reference, verify the file exists at that path
   - Report: "❌ Broken reference: [path]" for any missing files

2. **Check links in `docs/README.md`** (if it exists):
   - Extract all markdown links (format: `[text](./path/to/file.md)`)
   - Parse out the file paths
   - For each path, verify the file exists at `docs/[path]`
   - Report: "❌ Broken link in README: [path]" for any missing files

**If broken references found**:
- List them for the user
- Ask: "Should these be removed, or are the files missing?"
- If remove → Update both indexes to remove references
- If missing → Ask user to restore files or provide correct paths

**Check 3: Validate index format**

Ensure both indexes follow proper structure:
- `.makeflow/project/index.md` has all required sections
- `docs/README.md` has navigation links (if exists)
- Relative paths are correct
- Markdown formatting is valid

**Present validation summary**:

```markdown
## 📋 Index Validation Summary

### Completeness
- ✅ Total documentation files: [X]
- ✅ Files indexed: [Y]
- ⚠️  Files not indexed: [Z] (see list above)

### Integrity
- ✅ Broken references: [N] (see list above)
- ✅ Valid references: [M]

### Next Steps
- [ ] Add [Z] missing files to index
- [ ] Fix [N] broken references
- [ ] Review and approve final index
```

**Iterate until validation passes**:
- Fix issues identified
- Re-run validation
- Repeat until all checks pass

---

### Step 5: Validate with User

**Show the generated index** to the user in a clear, readable format.

**Ask**:
1. Does this accurately reflect your documentation structure?
2. Are there any missing sections or important documents?
3. Any corrections needed to the descriptions?
4. Any additional categories or organization patterns to note?

**If corrections needed**:
- Update the index based on feedback
- Show the updated version
- Repeat until user approves

---

### Step 6: Finalize and Commit

**Save the file**:
```bash
# The index file should already be created at:
.makeflow/project/index.md
```

**Create commit**:
```bash
git add .makeflow/project/index.md
git commit -m "docs: Connect makeflow to existing project documentation

Created documentation index at .makeflow/project/index.md
- Mapped documentation structure
- Added AI agent quick reference
- Set up low-maintenance tracking

Documentation entry point: [PATH_TO_MAIN_DOC]"
```

---

### Step 7: Provide Next Steps

**Show the user**:
```markdown
## ✅ Documentation Successfully Connected!

Your project documentation is now accessible to makeflow workflows.

### 📋 What Was Created:

- **Documentation Index**: `.makeflow/project/index.md`
  - Maps your documentation structure
  - Provides AI agent context hints
  - Low-maintenance tracking system

### 🎯 How to Use:

**In makeflow workflows**, AI agents will now automatically:
1. Reference your documentation when needed
2. Find relevant docs for specific tasks
3. Suggest documentation updates when appropriate

**Manual reference**:
When working with AI tools, you can say:
```
@ai Include project documentation context from .makeflow/project/index.md
[Your task or question]
```

### 📚 Update Documentation:

When you make changes to your documentation structure, update the index:
```
@ai Use .makeflow/workflows/00-setup/hook-docs.md
```

Or manually edit: `.makeflow/project/index.md`

### 🔄 Keep Docs Updated:

When completing features, use:
```
@ai Use .makeflow/workflows/04-delivery/update-docs.md
```

This workflow will check if documentation needs updates based on your changes.
```

---

## Documentation Index Best Practices

### When to Update Indexes

**ALWAYS update indexes when**:
- ✅ Creating new documentation files in major categories (patterns/specs/workflows/decisions)
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
2. **Update `docs/README.md`** - If file is in a major category
   - Add link to new files with descriptive text
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
- ✅ **After any documentation changes** - Run quick validation
- ✅ **Before feature completion** - Deep validation to catch any missed updates
- ✅ **Monthly or before major releases** - Comprehensive audit
- ✅ **During PR reviews** - Spot check that indexes match changes

### Common Pitfalls to Avoid

**❌ DON'T**:
- Move files without updating index links → Results in broken links
- Add new docs without adding to indexes → New docs become "hidden" and undiscoverable
- Rename files without search-and-replace in indexes → Old references become stale
- Remove files without removing index entries → Broken links confuse users
- Create new documentation categories without updating index structure → Inconsistent organization
- Batch many doc changes without checking indexes → Compounding drift
- Assume indexes "auto-update" → They don't; manual maintenance required

**✅ DO**:
- Update files and indexes in the same commit → Atomic changes prevent drift
- Use descriptive link text in indexes → Helps users and AI agents find relevant docs
- Keep index descriptions concise → One-line summaries are sufficient
- Link liberally within documentation → Cross-references improve navigation
- Review indexes during PR reviews → Catch issues before merge
- Set calendar reminders for monthly audits → Proactive maintenance prevents large cleanup efforts

### Validation Approach

**Quick validation** - Check if indexes reference existing files:

**For `docs/README.md`**:
1. Extract all markdown links (format: `[text](./path/to/file.md)`)
2. Parse out the file paths from these links
3. For each path, check if the file exists at `docs/[path]`
4. Report any broken links (files that don't exist)

**For `.makeflow/project/index.md`**:
1. Extract all documentation file references (typically in format: `` `../../docs/path/to/file.md` ``)
2. For each reference, check if the file exists at that path
3. Report any broken references

**Find undocumented files** - Discover markdown files not in indexes:

1. **List all markdown files** in the `docs/` folder:
   - Include all `.md` files recursively
   - Exclude `README.md` at root (since it IS the index)
   - Exclude special folders: `node_modules`, `.git`, `templates`, `archive`
   - Exclude placeholder files like `.gitkeep`
2. **Compare against index entries** - manually review which files are listed in `docs/README.md`
3. **Identify gaps** - files that exist but aren't referenced anywhere

**Full validation** - Comprehensive check (run monthly or before releases):

1. **Check for broken links in `docs/README.md`**:
   - Extract all markdown links
   - Verify each linked file exists
   - Report: "✅ Valid: [path]" or "❌ Broken: [path]"

2. **Check for broken references in `.makeflow/project/index.md`**:
   - Extract all file path references
   - Verify each file exists
   - Report: "✅ Valid: [path]" or "❌ Broken: [path]"

3. **List potentially undocumented files**:
   - Find all markdown files in `docs/` (excluding special files)
   - Display for manual review against indexes

### Recovery from Drift

**If indexes are severely out of sync**:

1. **Run full validation** - Identify all discrepancies
2. **Create an issue** - Document what needs fixing
3. **Fix systematically**:
   - Remove broken links first
   - Add missing files next
   - Update stale descriptions last
4. **Verify fixes** - Re-run validation
5. **Commit with clear message** - Explain what was synchronized
6. **Set up preventive measures** - Add validation to PR checklist

**Example recovery commit message**:
```
docs: Synchronize documentation indexes

Fixed inconsistencies between actual docs and indexes:
- Removed 3 broken links from docs/README.md
- Added 5 missing pattern docs to indexes
- Updated 2 file paths that had moved
- Refreshed descriptions for 4 outdated entries

All documentation is now discoverable and properly indexed.
```

---

## Success Criteria

- [ ] Documentation structure discovered and analyzed
- [ ] `.makeflow/project/index.md` created with accurate mapping
- [ ] All major documentation categories included
- [ ] AI agent quick reference provided
- [ ] User validated and approved the index
- [ ] Changes committed to repository
- [ ] User understands how to use and maintain the index

---

## Example Output

**For a project with this structure**:
```
docs/
├── README.md
├── patterns/
│   ├── api-patterns.md
│   └── component-patterns.md
├── specs/
│   └── feature-spec.md
└── workflows/
    └── development.md
```

**The index would look like**:

```markdown
# Project Documentation Index

> **Entry Point**: This file helps AI agents understand where project documentation lives.

## 🏠 Main Documentation Hub

**Location**: `../../docs/README.md`

The main documentation hub contains:
- Project overview and mission
- Quick start guide
- Core concepts and terminology
- Navigation to detailed documentation

## 📚 Documentation Structure

### Patterns (`../../docs/patterns/`)
Development patterns and best practices:
- **API Patterns** → Backend API design conventions and patterns
- **Component Patterns** → Frontend component structure and composition

### Specifications (`../../docs/specs/`)
Technical specifications for features:
- **Feature Spec** → Detailed specification for the main feature

### Workflows (`../../docs/workflows/`)
Team processes and development workflows:
- **Development** → Development process, tools, and conventions

## 🤖 AI Agent Quick Reference

### For Implementation Tasks:
Include: `docs/README.md` + `docs/patterns/**` + relevant specs

### For Understanding Features:
Include: `docs/README.md` + `docs/specs/**`

### For Process Questions:
Include: `docs/README.md` + `docs/workflows/**`

### For Complete Context:
Include: `docs/**/*` (everything)

## 📝 Maintenance Notes

**Last Updated**: 2025-12-14

**Update Triggers**: 
- New top-level documentation sections added
- Major reorganization of docs/ structure
- New documentation categories created

**Low Maintenance Design**: This index describes WHERE docs live, not their detailed contents. It rarely needs updates unless the documentation structure itself changes.
```

---

## Troubleshooting

### Issue: Can't find documentation

**Problem**: No docs folder found  
**Solution**: Ask user for the location or suggest using `bootstrap-docs.md` workflow instead

### Issue: Documentation is unorganized

**Problem**: No clear structure or patterns  
**Solution**: 
1. Create index based on what exists
2. Suggest organizing documentation (optional)
3. Note in the index that organization may vary

### Issue: Multiple documentation locations

**Problem**: Docs scattered across README.md, wiki, docs/, etc.  
**Solution**: 
1. Create index that points to all locations
2. Note in "Maintenance Notes" that docs are distributed
3. Suggest consolidation (optional)

---

**Last Updated**: 2025-12-14  
**Workflow Version**: 1.0.0
