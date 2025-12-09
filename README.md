# makeflow

**AI-agnostic, specification-driven development workflows**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

## 🚀 60-Second Quick Start

```bash
# 1. Copy makeflow to your project
cp -r .makeflow your-project/

# 2. Start your first feature
cd your-project
```

```markdown
@ai Use .makeflow/workflows/01-intake/from-ticket.md

Ticket: YOUR-TICKET-ID
```

**That's it!** The AI will guide you through the entire process.

---

## What is makeflow?

**makeflow** helps developers work effectively with AI tools by providing clear, structured workflows for every stage of development.

### ✨ Key Features

- **📋 Specification-Driven** - Every change starts with clear requirements
- **🤖 AI-Agnostic** - Works with Codegen, Cursor, Claude, ChatGPT, any AI tool
- **📊 Complete Tracking** - From first idea to shipped code
- **🧹 Clean Repos** - Work folders → concise history summaries
- **📦 Zero Dependencies** - Pure markdown, copy to any project
- **🔄 Flexible Workflows** - Use what you need, skip what you don't

---

## The 4-Stage Workflow

```
┌──────────┐      ┌──────────┐      ┌──────────┐      ┌──────────┐
│  INTAKE  │ ───> │ PLANNING │ ───> │EXECUTION │ ───> │ DELIVERY │
└──────────┘      └──────────┘      └──────────┘      └──────────┘
     ↓                  ↓                  ↓                  ↓
 Clarified         Spec + Plan        Working Code       Shipped +
Requirements       (AGENTS.md)        + Tests            Summarized
```

### Stage 1: Intake (Clarify)
Transform vague ideas into clear requirements
- `from-ticket.md` - Start from existing ticket
- `from-idea.md` - Start from vague concept
- `from-bug.md` - Handle bug reports

### Stage 2: Planning (Specify)
Create executable specifications
- `create-spec.md` - Full technical specification
- `create-plan.md` - Break into tasks
- `create-ticket.md` - Create ticket from spec

### Stage 3: Execution (Build)
Implement with validation
- `execute-task.md` - Build one task (with tests)
- `execute-quick.md` - Fast implementation (< 1 hour)
- `execute-task-without-tests.md` - Opt-out variant

### Stage 4: Delivery (Ship)
Create PRs and archive
- `create-pr.md` - Production-ready pull request
- `update-docs.md` - Keep docs current
- `complete.md` - Summarize to history

---

## How It Works

### 1. Work-in-Progress Tracking

Active work lives in `.makeflow/work/feature-name/`:

```
.makeflow/work/feature-name/
├── AGENTS.md           # Entry point for AI agents
├── spec.md             # Feature specification
├── plan.md             # Task breakdown
└── notes.md            # Development notes
```

**Key Point**: Work folders ARE COMMITTED so cloud AI tools can read them.

### 2. History & Summaries

When complete, work is summarized and moved to `.makeflow/history/YYYY-MM-DD-feature-name/`:

```
.makeflow/history/2025-12-09-feature-export/
├── SUMMARY.md          # Concise summary
├── PR-LINK.md          # Link to merged PR
└── CHANGES.md          # List of changes
```

Original work folder is deleted (keeps repo clean).

### 3. AGENTS.md Entry Point

Single file that AI agents read to understand:
- What's being built and why
- Current progress
- Decisions made
- What needs to happen next

---

## Works with Any AI Tool

### Codegen
```markdown
@codegen Use .makeflow/workflows/01-intake/from-ticket.md
Ticket: ASG-145
```

### Cursor IDE
```markdown
@Cursor Follow .makeflow/workflows/01-intake/from-ticket.md
Ticket: ASG-145
```

### Claude Code
```markdown
@Claude Execute .makeflow/workflows/01-intake/from-ticket.md
Context: Ticket ASG-145
```

### Any AI Tool
Copy-paste the workflow content and provide your context!

See [MULTI-TOOL.md](.makeflow/docs/MULTI-TOOL.md) for detailed integration guide.

---

## Quick Examples

### Simple Bug Fix (30 minutes)
```markdown
@ai Use .makeflow/workflows/01-intake/from-bug.md
Bug: Excel export fails with special characters

# AI investigates and fixes
@ai Use .makeflow/workflows/03-execution/execute-quick.md

# Create PR and complete
@ai Use .makeflow/workflows/04-delivery/create-pr.md
@ai Use .makeflow/workflows/04-delivery/complete.md
```

### Medium Feature (4-8 hours)
```markdown
@ai Use .makeflow/workflows/01-intake/from-ticket.md
Ticket: ASG-145

# Create plan
@ai Use .makeflow/workflows/02-planning/create-plan.md

# Execute tasks
@ai Use .makeflow/workflows/03-execution/execute-task.md
Task: Task 1.1

# [Repeat for each task]

# Deliver
@ai Use .makeflow/workflows/04-delivery/create-pr.md
@ai Use .makeflow/workflows/04-delivery/complete.md
```

### Complex Feature (1-5 days)
```markdown
@ai Use .makeflow/workflows/01-intake/from-idea.md
Feature Idea: Bulk resource assignment

# Create detailed spec
@ai Use .makeflow/workflows/02-planning/create-spec.md

# Break into plan
@ai Use .makeflow/workflows/02-planning/create-plan.md

# Execute in phases
[Build iteratively]

# Update docs and deliver
@ai Use .makeflow/workflows/04-delivery/update-docs.md
@ai Use .makeflow/workflows/04-delivery/create-pr.md
@ai Use .makeflow/workflows/04-delivery/complete.md
```

---

## Why makeflow?

### The Problem

AI-assisted development often leads to:
- ❌ Building the wrong thing (unclear requirements)
- ❌ Inconsistent processes (everyone does it differently)
- ❌ Lost context (AI forgets what you were doing)
- ❌ Incomplete tracking (what changed and why?)
- ❌ Tool lock-in (tied to specific AI platform)

### The Solution

makeflow provides:
- ✅ **Clarity First**: Spec before code prevents wasted work
- ✅ **Consistent Process**: Same workflow for whole team
- ✅ **Persistent Context**: AGENTS.md keeps AI on track
- ✅ **Complete History**: Every change documented
- ✅ **Tool Freedom**: Works with any AI platform

---

## Project Structure

```
your-project/
├── .makeflow/
│   ├── README.md                      # System overview
│   ├── workflows/
│   │   ├── 01-intake/                 # Clarify requirements
│   │   │   ├── from-ticket.md
│   │   │   ├── from-idea.md
│   │   │   └── from-bug.md
│   │   ├── 02-planning/               # Create specifications
│   │   │   ├── create-spec.md
│   │   │   ├── create-plan.md
│   │   │   └── create-ticket.md
│   │   ├── 03-execution/              # Build with validation
│   │   │   ├── execute-task.md
│   │   │   ├── execute-quick.md
│   │   │   └── execute-task-without-tests.md
│   │   └── 04-delivery/               # Ship and document
│   │       ├── create-pr.md
│   │       ├── update-docs.md
│   │       └── complete.md
│   ├── templates/
│   │   ├── agents-template.md         # AGENTS.md structure
│   │   ├── prompt-feature.md          # Feature request templates
│   │   ├── prompt-bug.md              # Bug report templates
│   │   └── prompt-refactor.md         # Refactor templates
│   ├── work/                           # Active work (COMMITTED)
│   │   └── [feature-name]/
│   │       └── AGENTS.md
│   ├── history/                        # Completed work (COMMITTED)
│   │   ├── INDEX.md
│   │   └── [YYYY-MM-DD-feature-name]/
│   └── docs/
│       ├── GUIDE.md                    # Complete guide
│       ├── MULTI-TOOL.md               # AI tool integration
│       ├── DECISIONS.md                # Design decisions & FAQ
│       └── EXAMPLES.md                 # Real-world examples
└── [your project files]
```

---

## Documentation

- **[Complete Guide](.makeflow/docs/GUIDE.md)** - Everything you need to know
- **[Multi-Tool Integration](.makeflow/docs/MULTI-TOOL.md)** - Using different AI tools
- **[Design Decisions & FAQ](.makeflow/docs/DECISIONS.md)** - Why makeflow is designed this way
- **[Real-World Examples](.makeflow/docs/EXAMPLES.md)** - See it in action
- **[Workflows](.makeflow/workflows/)** - Browse all 12 workflows

---

## Philosophy

### 1. Specification-Driven
Every change starts with a spec (even micro-specs for small changes).  
**Why?** Prevents building the wrong thing.

### 2. AI-Agnostic
Pure markdown works with any AI tool.  
**Why?** No vendor lock-in, future-proof.

### 3. Tracking-First
From first idea to final ship, everything is tracked.  
**Why?** Complete traceability, easy code review.

### 4. Portable & Simple
Zero dependencies, copy to any project.  
**Why?** Maximum portability, no setup friction.

---

## Who Uses makeflow?

### Solo Developers
- Structure for AI-assisted development
- Clear process to follow
- Complete change history

### Small Teams
- Consistent workflow across team
- Flexible tool choices
- Easy onboarding

### Growing Teams
- Standardized processes
- Clear documentation trail
- Scales with complexity

---

## Key Design Decisions

### Work Folders Are Committed
**Why?** Cloud AI tools need to read them to understand current state.

### No Dates in Work Folder Names
**Why?** `feature-export` stays relevant; dates added in history when complete.

### Tests by Default (Opt-Out)
**Why?** Quality-first mindset; tests should be the norm, not the exception.

### Work/History Split with Cleanup
**Why?** Detailed tracking during development, concise summaries forever.

See [DECISIONS.md](.makeflow/docs/DECISIONS.md) for complete rationale.

---

## Getting Help

- **[FAQ](.makeflow/docs/DECISIONS.md#faq)** - Common questions answered
- **[Examples](.makeflow/docs/EXAMPLES.md)** - Real-world usage
- **[Issues](https://github.com/ajdurancr/makeflow/issues)** - Report bugs or request features
- **[Discussions](https://github.com/ajdurancr/makeflow/discussions)** - Ask questions, share experiences

---

## Contributing

makeflow is designed to evolve based on real-world usage.

**Ways to contribute**:
- 🐛 Report bugs or issues
- 💡 Suggest workflow improvements
- 📝 Share your usage examples
- 🔧 Submit workflow customizations
- 📚 Improve documentation

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

---

## License

MIT License - See [LICENSE](LICENSE)

**TL;DR**: Use makeflow anywhere, modify it freely, no attribution required.

---

## Acknowledgments

makeflow is built on the principle that **clear requirements + structured processes + AI assistance = better software faster**.

Inspired by countless hours of AI-assisted development and the lessons learned along the way.

---

## Quick Links

- **[📚 Complete Guide](.makeflow/docs/GUIDE.md)** - Start here
- **[🔧 Workflows](.makeflow/workflows/)** - Browse all workflows
- **[🤖 Multi-Tool Guide](.makeflow/docs/MULTI-TOOL.md)** - Codegen, Cursor, Claude, etc.
- **[💡 Examples](.makeflow/docs/EXAMPLES.md)** - See it in action
- **[❓ FAQ](.makeflow/docs/DECISIONS.md#faq)** - Common questions

---

**Ready to start?** Try your first workflow:

```markdown
@ai Use .makeflow/workflows/01-intake/from-ticket.md

Ticket: YOUR-TICKET-ID
```

Happy building! 🚀

