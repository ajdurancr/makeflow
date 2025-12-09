# 🚀 makeflow

**A lightweight, AI-agnostic specification-driven development workflow system**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Zero Dependencies](https://img.shields.io/badge/dependencies-zero-brightgreen.svg)](package.json)

> Track your features from spec to ship. Work with any AI tool. Copy to any project.

---

## ⚡ Quick Start (60 seconds)

### 1. Copy `.makeflow/` to Your Project

```bash
# Clone makeflow
git clone https://github.com/ajdurancr/makeflow.git

# Copy the workflow system to your project
cp -r makeflow/.makeflow your-project/

# That's it! You're ready to use makeflow.
```

### 2. Start Your First Workflow

Pick your AI tool and use the workflow:

**With Codegen:**
```markdown
@codegen Use .makeflow/workflows/01-intake/from-ticket.md

Linear Ticket: PROJ-123
```

**With Cursor:**
```markdown
@Cursor Follow .makeflow/workflows/01-intake/from-ticket.md

Linear Ticket: PROJ-123
```

**With Claude Code:**
```markdown
@Claude Follow .makeflow/workflows/01-intake/from-ticket.md

Linear Ticket: PROJ-123
```

### 3. Track Your Progress

makeflow automatically creates:
- `.makeflow/work/feature-name/` - Your active work-in-progress
- `.makeflow/history/YYYY-MM-DD-feature-name/` - Completed & summarized

---

## 🎯 What is makeflow?

**makeflow** is a specification-driven development workflow system designed to:

✅ **Work with any AI tool** - Codegen, Cursor, Claude, or your favorite AI assistant  
✅ **Track everything** - From first spec to final ship, all changes documented  
✅ **Portable** - Copy to any project, zero configuration needed  
✅ **Junior-to-senior friendly** - Clear workflows for all skill levels  
✅ **Zero dependencies** - Pure markdown, works everywhere  

---

## 📚 What's Inside

```
.makeflow/
├── workflows/              # 4-stage workflow system
│   ├── 01-intake/         # Clarify requirements
│   ├── 02-planning/       # Create specs and plans
│   ├── 03-execution/      # Build with validation
│   └── 04-delivery/       # Ship and document
├── work/                   # Active work-in-progress (gitignored)
│   └── feature-name/      # Current feature tracking
├── history/               # Completed work summaries
│   ├── INDEX.md           # All completed work
│   └── YYYY-MM-DD-feature/
├── docs/                  # Project documentation index
└── templates/             # Prompt templates

```

---

## 🔄 The 4-Stage Workflow

```
┌──────────┐      ┌──────────┐      ┌──────────┐      ┌──────────┐
│  INTAKE  │ ───> │ PLANNING │ ───> │EXECUTION │ ───> │ DELIVERY │
└──────────┘      └──────────┘      └──────────┘      └──────────┘
     ↓                  ↓                  ↓                  ↓
 Clarified         Spec + Plan        Working Code       Shipped +
Requirements       (AGENTS.md)        + Tests            Summarized
```

### Stage 1: Intake (Clarify)
Transform vague ideas or tickets into crystal-clear requirements.

**Workflows:**
- `from-ticket.md` - Start from existing ticket
- `from-idea.md` - Start from vague concept
- `from-bug.md` - Handle bug reports

### Stage 2: Planning (Specify)
Create executable specifications and task plans.

**Workflows:**
- `create-spec.md` - Full feature specification
- `create-plan.md` - Break into phases and tasks
- `estimate.md` - Size and estimate work

### Stage 3: Execution (Build)
Implement with validation checkpoints and test coverage.

**Workflows:**
- `execute-phase.md` - Build one phase at a time
- `execute-task.md` - Build one task with tests
- `execute-quick.md` - Quick changes (without full spec)

### Stage 4: Delivery (Ship)
Create PRs, update docs, and summarize to history.

**Workflows:**
- `create-pr.md` - Production-ready pull request
- `update-docs.md` - Keep documentation current
- `complete.md` - Summarize and move to history

---

## 🤖 Works With Any AI Tool

### Codegen
```markdown
@codegen Use .makeflow/workflows/01-intake/from-ticket.md
Ticket: PROJ-123
```

### Cursor IDE
```markdown
@Cursor Follow .makeflow/workflows/02-planning/create-spec.md
Feature: [description]
```

### Claude Code
```markdown
@Claude Execute .makeflow/workflows/03-execution/execute-task.md
Task: Phase 1, Task 1
```

### Any AI Tool
Just copy-paste the workflow content and provide the required context!

---

## 📖 Documentation

- **[Complete Guide](docs/GUIDE.md)** - Detailed walkthrough of all workflows
- **[Multi-Tool Setup](docs/MULTI-TOOL.md)** - Using makeflow with Cursor, Claude, etc.
- **[Design Decisions](docs/DECISIONS.md)** - Why we made certain choices
- **[FAQ](docs/FAQ.md)** - Frequently asked questions
- **[Examples](docs/EXAMPLES.md)** - Real-world workflow examples

---

## 🎓 Key Features

### 📝 Work-in-Progress Tracking
Active work lives in `.makeflow/work/feature-name/` with:
- `AGENTS.md` - Entry point and progress tracking
- Specs, plans, notes, decisions
- All context for AI tools to reference

### 📚 History & Summaries
Completed work moves to `.makeflow/history/YYYY-MM-DD-feature/`:
- Concise summary of changes
- Links to PRs and commits
- Indexed in `.makeflow/history/INDEX.md`
- Original work folder is deleted (keeps repo clean)

### 🧪 Tests by Default
All execution workflows include test coverage by default:
- Unit tests
- Integration tests
- Opt-out with `-without-tests` variants when needed

### ✅ Validation Gates
4 checkpoints prevent building the wrong thing:
1. "Can a junior dev understand this?"
2. "Are acceptance criteria testable?"
3. "Does implementation match the plan?"
4. "Is the PR ready to ship?"

### 🎯 Smart Defaults
Reduce decisions, increase velocity:
- Recommended workflows based on context
- Smart prompts with examples
- Clear next steps at every stage

---

## 🚀 Quick Examples

### Example 1: Feature from Ticket
```markdown
# 1. Intake
@ai Use .makeflow/workflows/01-intake/from-ticket.md
Ticket: PROJ-145

# AI validates ticket, creates .makeflow/work/feature-export/

# 2. Planning
@ai Use .makeflow/workflows/02-planning/create-plan.md
Feature: From ticket PROJ-145

# AI creates specification and task plan in work folder

# 3. Execution
@ai Use .makeflow/workflows/03-execution/execute-phase.md
Phase: 1 (Backend)

# AI implements, tests, updates progress in AGENTS.md

# 4. Delivery
@ai Use .makeflow/workflows/04-delivery/complete.md
Feature: feature-export

# AI creates PR, summarizes to history/, deletes work/
```

### Example 2: Quick Bug Fix
```markdown
@ai Use .makeflow/workflows/01-intake/from-bug.md

Bug: Export fails with special characters
Reproduction: [steps]

# Then:
@ai Use .makeflow/workflows/03-execution/execute-quick.md
Fix: Sanitize special characters in export filename
```

---

## 🏗️ Project Structure

### In Your Project
```
your-project/
├── .makeflow/              # Copy this to your project
│   ├── workflows/         # Workflow definitions
│   ├── work/              # Active work (gitignored)
│   ├── history/           # Completed summaries (committed)
│   ├── docs/              # Documentation index
│   └── templates/         # Prompt templates
├── .gitignore             # Add .makeflow/work/ to gitignore
└── [your code]
```

### .gitignore Setup
```gitignore
# makeflow work-in-progress (not committed)
.makeflow/work/

# makeflow history IS committed (summaries only)
# (no ignore needed for .makeflow/history/)
```

---

## 📐 Design Philosophy

### Specification-Driven
Every change starts with a spec. Even small changes get a micro-spec in the work folder.

### AI-Agnostic
Workflows work with any AI tool. No vendor lock-in. Pure markdown.

### Tracking-First
From first idea to final ship, everything is tracked. Work folders during dev, summaries after completion.

### Portable & Simple
Zero dependencies. Copy `.makeflow/` to any project. Works immediately.

### Progressive Complexity
Small changes use simple workflows. Large features use full 4-stage process.

---

## 🤝 Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Development
```bash
# Clone the repo
git clone https://github.com/ajdurancr/makeflow.git
cd makeflow

# Make your changes to .makeflow/

# Test with your AI tool
@ai Use .makeflow/workflows/01-intake/from-idea.md
Idea: [your test]

# Submit PR
```

---

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

---

## 🌟 Why makeflow?

**For Junior Developers:**
- Clear, step-by-step workflows
- Learn by following structured processes
- Validation checkpoints prevent mistakes
- Examples show how to use AI tools effectively

**For Senior Developers:**
- Consistent process across the team
- Easy to review AI-generated work
- Trackable decisions and changes
- Portable to any project

**For Teams:**
- Standardized development workflow
- AI tool flexibility (use what works for you)
- Complete change history
- Onboarding made simple

---

## 🔗 Links

- **Repository**: https://github.com/ajdurancr/makeflow
- **Issues**: https://github.com/ajdurancr/makeflow/issues
- **Discussions**: https://github.com/ajdurancr/makeflow/discussions

---

## 🎉 Get Started

```bash
# 1. Copy to your project
cp -r .makeflow your-project/

# 2. Add to .gitignore
echo ".makeflow/work/" >> your-project/.gitignore

# 3. Start building
@ai Use .makeflow/workflows/01-intake/from-ticket.md
```

**That's it! Happy building with makeflow! 🚀**

