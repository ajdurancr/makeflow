# makeflow Complete Guide

Welcome to the complete guide for **makeflow** - your AI-agnostic, specification-driven development workflow system.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Core Concepts](#core-concepts)
3. [Getting Started](#getting-started)
4. [The 4-Stage Workflow](#the-4-stage-workflow)
5. [Working with AI Tools](#working-with-ai-tools)
6. [Best Practices](#best-practices)
7. [Advanced Usage](#advanced-usage)
8. [Troubleshooting](#troubleshooting)

---

## Introduction

### What is makeflow?

**makeflow** is a lightweight system for managing AI-assisted software development. It provides:

- **Clear workflows** for every stage (Intake → Planning → Execution → Delivery)
- **Work tracking** that keeps repos clean
- **AI-agnostic design** that works with any AI tool
- **Zero dependencies** - pure markdown files
- **Specification-driven approach** that prevents building the wrong thing

### Who Is This For?

**Junior Developers**:
- Learn structured development processes
- Get guidance at every step
- Build confidence with AI assistance

**Senior Developers**:
- Consistent team processes
- Better code review experience
- Clear documentation trail

**Teams**:
- Standardized workflows
- Flexibility in tool choice
- Complete change history
- Easy onboarding

---

## Core Concepts

### 1. Specification-Driven Development

Every change starts with a specification:
- **Small changes**: Micro-spec in AGENTS.md
- **Medium features**: Plan with task breakdown
- **Large features**: Full technical specification

**Why?** Prevents wasted effort building the wrong thing.

### 2. Work / History Split

**Work Folder** (`.makeflow/work/[feature-name]/`):
- Active development tracking
- Detailed notes and progress
- **Committed to repo** (AI tools need to read it)
- Deleted after completion

**History Folder** (`.makeflow/history/[YYYY-MM-DD]-[feature-name]/`):
- Concise summaries only
- Permanent record
- Links to PRs and tickets
- Indexed for easy reference

**Why split?**
- Work folder: messy but useful during development
- History folder: clean permanent record
- Keeps repo organized

### 3. AGENTS.md Entry Point

Every work folder has `AGENTS.md`:
- **What**: Overview of the feature/fix
- **Why**: Business value
- **How**: Technical approach
- **Progress**: Current state with checkboxes
- **Decisions**: Key decisions with rationale
- **Next**: What to do next

**Purpose**: Single file AI agents read to understand complete context.

### 4. No Dates in Work Folders

Work folders use feature names only: `resource-multi-filter` not `2025-12-09-resource-multi-filter`

**Why?**
- Dated folders get stale and confusing
- Feature names stay relevant
- Encourages one feature per branch
- Dates added in history when complete

---

## Getting Started

### Installation

```bash
# 1. Clone makeflow to your project
cd your-project
git clone https://github.com/ajdurancr/makeflow.git .makeflow-temp
cp -r .makeflow-temp/.makeflow .
rm -rf .makeflow-temp

# 2. .gitignore already configured correctly (work folders are committed)

# 3. Done! Start using it
```

### First Feature

```markdown
@ai Use .makeflow/workflows/01-intake/from-ticket.md

Ticket: YOUR-TICKET-ID
```

That's it! The AI will:
1. Read your ticket
2. Clarify requirements
3. Create work folder
4. Guide you through the process

---

## The 4-Stage Workflow

```
┌──────────┐      ┌──────────┐      ┌──────────┐      ┌──────────┐
│  INTAKE  │ ───> │ PLANNING │ ───> │EXECUTION │ ───> │ DELIVERY │
└──────────┘      └──────────┘      └──────────┘      └──────────┘
```

### Stage 1: Intake (Clarify)

**Purpose**: Transform vague ideas into clear requirements

**Workflows**:
- `from-ticket.md` - Start from existing ticket
- `from-idea.md` - Start from vague concept
- `from-bug.md` - Handle bug reports

**Output**: Work folder with `AGENTS.md` and clear requirements

### Stage 2: Planning (Specify)

**Purpose**: Create executable specifications and plans

**Workflows**:
- `create-spec.md` - Full technical specification (complex features)
- `create-plan.md` - Task breakdown (medium features)
- `create-ticket.md` - Create ticket from spec (bidirectional!)

**Output**: Specification and/or task plan ready to execute

### Stage 3: Execution (Build)

**Purpose**: Implement with validation and testing

**Workflows**:
- `execute-task.md` - Build one task (with tests, default)
- `execute-quick.md` - Fast implementation (< 1 hour)
- `execute-task-without-tests.md` - Opt-out variant (rare)

**Output**: Working, tested code

### Stage 4: Delivery (Ship)

**Purpose**: Create PRs, document, and archive

**Workflows**:
- `create-pr.md` - Production-ready pull request
- `update-docs.md` - Keep documentation current
- `complete.md` - Summarize and move to history

**Output**: Merged PR, updated docs, clean repo

---

## Working with AI Tools

### Codegen

```markdown
@codegen Use .makeflow/workflows/01-intake/from-ticket.md

Ticket: ASG-145
Additional Context: Product wants this for Q1 demo
```

### Cursor IDE

```markdown
@Cursor Follow the workflow in .makeflow/workflows/01-intake/from-ticket.md

Ticket: ASG-145

Please read the workflow file and follow its instructions.
```

### Claude Code

```markdown
@Claude Execute the workflow defined in .makeflow/workflows/01-intake/from-ticket.md

Context:
- Ticket: ASG-145
- Project: Resource Management System
- Role: I'm a full-stack developer

Follow the workflow steps precisely.
```

### Any AI Tool

1. **Copy** the workflow content
2. **Paste** into AI chat with your context
3. **Follow** the AI's guidance

---

## Best Practices

### 1. One Feature Per Branch

Work folders encourage this:
- No dates in folder names
- Clear feature focus
- Clean branch strategy

### 2. Tests by Default

All execution workflows include tests by default:
- Quality-first mindset
- Prevents regressions
- Opt-out available if truly needed

### 3. Commit Often

Especially during execution:
- Commit after each task
- Clear commit messages
- Easy to review progress

### 4. Keep AGENTS.md Updated

Throughout development:
- Mark tasks complete
- Add decisions
- Update progress
- Note blockers

### 5. Clean Up After Completion

Use the `complete.md` workflow:
- Summarize work concisely
- Move to history
- Delete work folder
- Update INDEX

---

## Advanced Usage

### Combining Workflows

You don't have to follow the full 4-stage process for every change:

**Simple bug fix**:
```
from-bug.md → execute-quick.md → create-pr.md → complete.md
```

**Quick feature**:
```
from-ticket.md → create-plan.md → execute-task.md × 3 → create-pr.md → complete.md
```

**Complex feature**:
```
from-idea.md → create-spec.md → create-plan.md → execute-task.md × N → create-pr.md → update-docs.md → complete.md
```

### Working Across Multiple Sessions

**Session 1**:
```markdown
@ai Use .makeflow/workflows/01-intake/from-ticket.md
Ticket: ASG-145
```

**Session 2** (later):
```markdown
@ai I'm continuing work on ASG-145

Please read `.makeflow/work/resource-multi-filter/AGENTS.md` for context.

Let's continue with the next task.
```

The AI reads AGENTS.md and knows exactly where you left off!

### Creating Tickets from Specs

Bidirectional workflow:

**Spec → Ticket**:
```markdown
@ai Use .makeflow/workflows/02-planning/create-ticket.md
Feature: resource-multi-filter
```

**Ticket → Spec**:
```markdown
@ai Use .makeflow/workflows/01-intake/from-ticket.md
Ticket: ASG-145
```

---

## Troubleshooting

### "Work folder already exists"

**Solution**: Either continue with existing work or rename:
```bash
mv .makeflow/work/feature-name .makeflow/work/feature-name-v2
```

### "Can't find AGENTS.md"

**Solution**: Create work folder first:
```markdown
@ai Use .makeflow/workflows/01-intake/from-ticket.md
Ticket: YOUR-TICKET
```

### "AI doesn't follow workflow"

**Solution**: Be explicit:
```markdown
@ai You MUST follow the workflow in .makeflow/workflows/[workflow-name].md

Read it completely and follow each step precisely.
```

### "History getting large"

**Solution**: Archive old history periodically:
```bash
mkdir .makeflow/history/archive/2024
mv .makeflow/history/2024-* .makeflow/history/archive/2024/
# Update INDEX.md accordingly
```

---

## Next Steps

- **Try it**: Start with `from-ticket.md`
- **Customize**: Adapt workflows for your team
- **Share**: Copy `.makeflow/` to other projects
- **Improve**: Suggest enhancements via GitHub

---

**Questions?** See [FAQ](DECISIONS.md#faq) or open an issue!

