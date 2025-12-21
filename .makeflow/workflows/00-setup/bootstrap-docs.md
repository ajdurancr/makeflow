# Workflow: Bootstrap Documentation Structure

**Stage**: 00 - Setup  
**Purpose**: Create documentation structure from scratch  
**Time**: 20-30 minutes  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ Your project has minimal or no documentation
- ✅ You want to establish a solid documentation foundation
- ✅ You want AI-generated initial documentation to review and refine

---

## Prerequisites

- [ ] Project codebase exists (for scanning and analysis)
- [ ] You can provide basic project information (name, description, purpose)
- [ ] You're ready to review and potentially edit generated documentation

---

## Instructions for AI Agent

### Step 1: Gather Project Information

**Ask the user for**:
1. **Project name**: What is this project called?
2. **Brief description** (1-2 sentences): What does this project do?
3. **Primary purpose**: What problem does it solve?
4. **Target users**: Who will use this project?

**Optional questions**:
5. Any specific documentation sections you know you need?
6. Any existing documentation that should be incorporated?

---

### Step 2: Propose Documentation Structure

**Show the user this recommended structure**:

```
docs/
├── README.md              # Main documentation hub
├── patterns/              # Development patterns (if applicable)
│   └── .gitkeep
├── specs/                 # Feature specifications
│   └── .gitkeep
├── workflows/             # Team processes
│   ├── .gitkeep
│   └── documentation/
│       └── guidelines.md
└── decisions/             # Architecture decisions (ADRs)
    └── .gitkeep
```

**Explain**:
- **README.md**: Central hub with overview, quick start, and navigation
- **patterns/**: Reusable development patterns and best practices
- **specs/**: Technical specifications for features and components
- **workflows/**: Team processes, development workflows, how-tos
- **decisions/**: Architecture Decision Records (ADRs) for significant choices
- **.gitkeep**: Placeholder files to ensure empty directories are tracked

**Ask**: 
- "Would you like to use this structure, or prefer something different?"
- "Any additional sections needed?" (e.g., `api/`, `guides/`, `tutorials/`)

**If user wants modifications**:
- Adjust structure based on feedback
- Add or remove sections as requested
- Confirm final structure before proceeding

---

### Step 3: Scan Codebase

**Analyze the project to gather**:

1. **Technology stack**:
   ```bash
   # Package managers and dependency files
   ls package.json requirements.txt Gemfile Cargo.toml go.mod pom.xml build.gradle 2>/dev/null
   
   # Framework indicators
   find . -maxdepth 3 -name "next.config.*" -o -name "vite.config.*" -o -name "angular.json" 2>/dev/null
   ```

2. **Project structure**:
   ```bash
   # Main directories
   find . -maxdepth 2 -type d ! -path "*/node_modules/*" ! -path "*/.git/*" ! -path "*/dist/*"
   ```

3. **Key files**:
   ```bash
   # Configuration and entry points
   ls -la | grep -E "^[^.].*\.(json|yaml|yml|toml|config\..*)$"
   ```

4. **Programming languages**:
   ```bash
   # Count files by extension
   find . -type f ! -path "*/node_modules/*" ! -path "*/.git/*" | sed 's/.*\.//' | sort | uniq -c | sort -rn | head -5
   ```

**Summarize findings** for the user:
```markdown
## 📊 Codebase Analysis

**Primary Language**: [Language]
**Framework**: [Framework if detected]
**Project Type**: [e.g., Web App, CLI Tool, Library, API]

**Key Technologies**:
- [Technology 1]
- [Technology 2]
- [Technology 3]

**Project Structure**:
- `[folder1]/` - [Inferred purpose]
- `[folder2]/` - [Inferred purpose]
- `[folder3]/` - [Inferred purpose]
```

---

### Step 4: Generate Initial Documentation

**Create the following files** with AI-generated content:

#### **4.1: `docs/README.md`** (Main Hub)

Use this template and fill with project-specific content:

```markdown
# [Project Name] Documentation

> [Brief tagline or description]

## 🎯 What is [Project Name]?

[2-3 paragraph description of what the project does, its purpose, and key value proposition]

## 🚀 Quick Links

- [Getting Started](#getting-started)
- [Core Concepts](#core-concepts)
- [Patterns](./patterns/) - Development patterns *(if applicable)*
- [Specifications](./specs/) - Feature specifications
- [Workflows](./workflows/) - Team processes
- [Decisions](./decisions/) - Architecture decisions

## 💡 Core Concepts

### [Concept 1]
[Brief explanation of a key concept]

### [Concept 2]
[Brief explanation of another key concept]

[Add 2-4 core concepts based on codebase analysis]

## 🏗️ Technology Stack

**[Primary Component]** (e.g., Frontend, Backend, Core):
- [Technology 1]
- [Technology 2]
- [Technology 3]

[Add additional components if applicable]

**Development Tools**:
- [Tool 1]
- [Tool 2]

## 📚 Documentation Sections

### 🎨 Patterns

Development patterns and best practices:
- [Link to patterns when created]

### 📋 Specifications

Technical specifications for features:
- [Link to specs when created]

### ⚙️ Workflows

Team workflows and processes:
- [Documentation Guidelines](./workflows/documentation/guidelines.md)

### 🗳️ Architecture Decisions

Record of significant architectural decisions:
- [Link to ADRs when created]

## 🚀 Getting Started

[Brief quick start section - can be expanded later]

### Prerequisites

- [Prerequisite 1]
- [Prerequisite 2]

### Installation

\`\`\`bash
# [Installation command based on detected package manager]
[command]
\`\`\`

### Running the Project

\`\`\`bash
# [Run command based on detected setup]
[command]
\`\`\`

## 🤝 Contributing

See [Documentation Guidelines](./workflows/documentation/guidelines.md) for how to add or update documentation.

---

**Last Updated**: [CURRENT_DATE]  
**Status**: Initial documentation - ready for expansion
```

#### **4.2: `docs/workflows/documentation/guidelines.md`**

Create this file with basic guidelines:

```markdown
# Documentation Guidelines

## When to Add Documentation

- **New features**: Add specification in `specs/`
- **Architectural decisions**: Create ADR in `decisions/`
- **Reusable patterns**: Document in `patterns/`
- **Process changes**: Update or add to `workflows/`

## Where to Add Documentation

| Documentation Type | Location | Format |
|-------------------|----------|--------|
| Feature specs | `specs/[feature-name].md` | Specification template |
| Patterns | `patterns/[pattern-name].md` | Pattern template |
| Workflows | `workflows/[workflow-name].md` | Workflow template |
| Decisions | `decisions/NNNN-[title].md` | ADR template |

## How to Structure Documents

### General Guidelines

1. **Start with overview**: What is this about?
2. **Explain context**: Why does this exist?
3. **Provide details**: How does it work?
4. **Link liberally**: Connect to related documentation
5. **Use examples**: Concrete examples clarify concepts
6. **Keep it updated**: Add "Last Updated" dates

### Document Length

- **Target**: Most docs should be 200-500 lines
- **Maximum**: ~2000 lines before considering splitting
- **Minimum**: No minimum - concise is good!

## Templates

For templates, see: `.makeflow/templates/project-docs/docs/` in the makeflow framework.

## Getting Help

If unsure how to document something:
1. Check existing documentation for similar content
2. Look at template examples
3. Ask the team for guidance

---

**Last Updated**: [CURRENT_DATE]
```

#### **4.3: Create directory structure**

```bash
mkdir -p docs/patterns docs/specs docs/workflows/documentation docs/decisions
touch docs/patterns/.gitkeep docs/specs/.gitkeep docs/decisions/.gitkeep
```

---

### Step 4.5: Initialize Pattern/Spec Index Structure

**Purpose**: Pre-populate index sections to make future additions easier and prevent drift.

**For `docs/README.md`**, ensure the documentation sections include placeholders for common patterns even if empty:

```markdown
## 📚 Documentation Sections

### 🎨 Patterns

Development patterns and best practices:
- SDK Patterns → *Will be populated as SDK patterns are identified*
- API Patterns → *Will be populated as API patterns are defined*
- Testing Patterns → *Will be populated as testing patterns emerge*
- Form Patterns → *Will be populated as form patterns are established*
- [Add pattern links here as they are created]

### 📋 Specifications

Technical specifications for features:
- [Feature specs will be added here as features are planned]

### ⚙️ Workflows

Team workflows and processes:
- [Documentation Guidelines](./workflows/documentation/guidelines.md)
- [Additional workflow docs will be added here as processes are established]

### 🗳️ Architecture Decisions

Record of significant architectural decisions:
- [ADRs will be added here as architectural decisions are made]
```

**For `.makeflow/project/index.md`**, include category descriptions with growth notes:

```markdown
### Patterns (`../../docs/patterns/`)
Development patterns and best practices for this project.

**Common Pattern Categories**:
- SDK Patterns - *Will be populated as patterns emerge*
- API Patterns - *Will be populated as patterns emerge*
- Testing Patterns - *Will be populated as patterns emerge*
- Form Patterns - *Will be populated as patterns emerge*

*Note: This section grows organically as patterns are identified and documented during development.*

### Specifications (`../../docs/specs/`)
Technical specifications for features and components.

*Will be populated as features are specified.*

### Workflows (`../../docs/workflows/`)
Team processes and development workflows:
- **Documentation Guidelines** → How to add and organize documentation
- *(Additional workflows will be added as processes are established)*

### Decisions (`../../docs/decisions/`)
Architecture Decision Records (ADRs) documenting significant technical choices.

*Will be populated as architectural decisions are made.*
```

**Why this matters**:
- Makes it obvious where new documentation should be added
- Reduces cognitive load when adding new docs
- Prevents documentation from being created without corresponding index entries
- Provides visual structure even when sections are empty

---

### Step 5: Create Makeflow Documentation Index

**Create** `.makeflow/project/index.md`:

```markdown
# Project Documentation Index

> **Entry Point**: This file helps AI agents understand where project documentation lives.

## 🏠 Main Documentation Hub

**Location**: `../../docs/README.md`

The main documentation hub contains:
- Project overview and core concepts
- Technology stack information
- Quick start guide
- Navigation to all documentation sections

## 📚 Documentation Structure

### Patterns (`../../docs/patterns/`)
Development patterns and best practices for this project.

*Will be populated as patterns emerge during development.*

### Specifications (`../../docs/specs/`)
Technical specifications for features and components.

*Will be populated as features are specified.*

### Workflows (`../../docs/workflows/`)
Team processes and development workflows:
- **Documentation Guidelines** → How to add and organize documentation

### Decisions (`../../docs/decisions/`)
Architecture Decision Records (ADRs) documenting significant technical choices.

*Will be populated as architectural decisions are made.*

## 🤖 AI Agent Quick Reference

### For Implementation Tasks:
Include: `docs/README.md` + `docs/patterns/**` + relevant specs

### For Understanding Features:
Include: `docs/README.md` + `docs/specs/**` + relevant decisions

### For Process Questions:
Include: `docs/README.md` + `docs/workflows/**`

### For Complete Context:
Include: `docs/**/*` (everything)

## 📝 Maintenance Notes

**Last Updated**: [CURRENT_DATE]

**Update Triggers**: 
- New top-level documentation sections added
- Major reorganization of docs/ structure
- New documentation categories created

**Low Maintenance Design**: This index describes WHERE docs live, not their detailed contents. It rarely needs updates unless the documentation structure itself changes.

**Progressive Growth**: Documentation starts minimal and grows organically as:
- Patterns are identified and documented
- Features are specified
- Architectural decisions are made
- Processes are established
```

---

### Step 6: User Review

**Show the user**:

1. **Generated directory structure**:
   ```bash
   tree docs/ -L 3
   ```

2. **Generated README.md preview** (first 50 lines or key sections)

3. **Ask for feedback**:
   - Does the overview accurately describe your project?
   - Any corrections to technology stack or structure?
   - Any sections that should be added or removed?
   - Any missing information that should be included?

**Iterate on feedback**:
- Make requested changes
- Show updates
- Repeat until user approves

---

### Step 7: Commit Documentation

**Create commit**:
```bash
git add docs/ .makeflow/project/index.md
git commit -m "docs: Bootstrap initial documentation structure

Created documentation foundation:
- Main documentation hub (docs/README.md)
- Directory structure (patterns, specs, workflows, decisions)
- Documentation guidelines
- Makeflow integration index

Documentation is ready for organic growth as project develops."
```

---

### Step 8: Provide Next Steps

**Show the user**:

```markdown
## ✅ Documentation Structure Created!

Your project now has a solid documentation foundation.

### 📋 What Was Created:

**Documentation Structure**:
```
docs/
├── README.md              # Main hub with overview and navigation
├── patterns/              # For development patterns (ready for content)
├── specs/                 # For feature specifications (ready for content)
├── workflows/             # Team processes
│   └── documentation/
│       └── guidelines.md  # How to add documentation
└── decisions/             # For architecture decisions (ready for content)
```

**Makeflow Integration**:
- `.makeflow/project/index.md` - AI agent documentation index

### 🎯 How to Use:

**Adding Content**:

1. **Document a pattern**:
   ```
   # Create file: docs/patterns/[pattern-name].md
   # Use template from: .makeflow/templates/project-docs/docs/patterns/pattern-template.md
   ```

2. **Specify a feature**:
   ```
   # Create file: docs/specs/[feature-name].md
   # Use template from: .makeflow/templates/project-docs/docs/specs/spec-template.md
   ```

3. **Record a decision**:
   ```
   # Create file: docs/decisions/NNNN-[decision-title].md
   # Use template from: .makeflow/templates/project-docs/docs/decisions/adr-template.md
   ```

**Documentation Guidelines**:
See `docs/workflows/documentation/guidelines.md` for how to add and organize documentation.

**Templates**:
All templates available at: `.makeflow/templates/project-docs/`

### 🔄 Keeping Docs Updated:

When completing features, use:
```
@ai Use .makeflow/workflows/04-delivery/update-docs.md
```

This workflow will check if documentation needs updates based on your changes.

### 📚 Progressive Growth:

This documentation is designed to grow organically:
- Start small with just the README
- Add patterns as you identify them
- Create specs as you plan features
- Record decisions as you make them
- Update guidelines as processes evolve

**No need to fill everything now** - let it grow naturally with your project!
```

---

## Documentation Index Best Practices

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

- [ ] Project information gathered from user
- [ ] Documentation structure proposed and approved
- [ ] Codebase analyzed for technology stack and structure
- [ ] Initial documentation generated (README, guidelines)
- [ ] Documentation structure created (folders and files)
- [ ] Makeflow index created (`.makeflow/project/index.md`)
- [ ] User reviewed and approved generated content
- [ ] All changes committed to repository
- [ ] User understands how to use and grow the documentation

---

## Example Output

**For a React + TypeScript project**, the generated `docs/README.md` might include:

```markdown
# MyApp Documentation

> A modern web application for task management

## 🎯 What is MyApp?

MyApp is a task management application that helps teams organize and track their work efficiently. Built with React and TypeScript, it provides an intuitive interface for creating, assigning, and monitoring tasks across projects.

## 💡 Core Concepts

### Tasks
Individual work items with descriptions, assignees, due dates, and status tracking.

### Projects
Collections of related tasks organized by team or initiative.

### Workspaces
Top-level containers for projects, typically representing different teams or departments.

## 🏗️ Technology Stack

**Frontend**:
- React 19
- TypeScript 5
- Tailwind CSS
- React Query

**Backend**:
- Node.js
- Express
- PostgreSQL
- Prisma ORM

**Development Tools**:
- Vite
- ESLint
- Prettier

[... rest of generated content ...]
```

---

## Troubleshooting

### Issue: Can't detect technology stack

**Problem**: No obvious package.json, requirements.txt, etc.  
**Solution**: Ask user directly for technology information

### Issue: User wants different structure

**Problem**: Proposed structure doesn't fit project needs  
**Solution**: 
1. Ask user to describe their preferred structure
2. Adapt to their needs
3. Create custom structure
4. Still provide templates that can be adapted

### Issue: Generated content is too generic

**Problem**: AI-generated docs lack project-specific details  
**Solution**: 
1. Ask user for more specific information
2. Update generated content with details
3. Mark sections with `[TODO: Add project-specific details]` for user to fill

---

**Last Updated**: 2025-12-21  
**Workflow Version**: 1.1.0
