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

### Step 4: Validate with User

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

### Step 5: Finalize and Commit

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

### Step 6: Provide Next Steps

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

