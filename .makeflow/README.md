# .makeflow/

This is the **makeflow** specification-driven development workflow system.

## Structure

```
.makeflow/
├── workflows/              # Workflow definitions for AI tools
│   ├── 00-setup/          # Setup and configuration
│   ├── 01-intake/         # Clarify requirements
│   ├── 02-planning/       # Create specifications
│   ├── 03-execution/      # Build with validation
│   └── 04-delivery/       # Ship and document
├── work/                   # Active work-in-progress (COMMITTED for AI access)
│   └── [feature-name]/    # Current feature being built
│       └── AGENTS.md      # Entry point for AI agents
├── history/               # Completed work summaries (committed)
│   ├── INDEX.md           # Index of all completed work
│   └── [YYYY-MM-DD-feature]/  # Summarized completed work
├── framework/             # Makeflow framework documentation
│   ├── DECISIONS.md       # Framework design decisions
│   ├── EXAMPLES.md        # Usage examples
│   ├── GUIDE.md           # Complete guide
│   └── MULTI-TOOL.md      # Multi-tool integration guide
├── project/               # Host project documentation entry point
│   └── index.md           # AI agent documentation index
└── templates/             # Prompt templates for AI tools
    ├── agents-template.md
    ├── prompt-*.md
    └── project-docs/      # Documentation templates for host projects
```

## Quick Start

### 1. Start a New Feature

```markdown
@ai Use .makeflow/workflows/01-intake/from-ticket.md
Ticket: PROJ-123
```

### 2. The AI Will:
- Validate the ticket
- Create `.makeflow/work/feature-name/`
- Create `AGENTS.md` as the entry point
- Guide you through the workflow

### 3. Track Progress

All work is tracked in `.makeflow/work/feature-name/AGENTS.md`:
- Current phase
- Completed tasks
- Next steps
- Decisions made

### 4. Complete the Feature

```markdown
@ai Use .makeflow/workflows/04-delivery/complete.md
Feature: feature-name
```

The AI will:
- Create a PR
- Summarize all work
- Move summary to `.makeflow/history/`
- Delete the work folder
- Update history INDEX

## Work vs History

### `.makeflow/work/` (COMMITTED - but deleted after completion)
- **Active work in progress**
- **Committed to repo** so cloud AI tools (Codegen, Claude Code) can read it
- Detailed tracking during development
- `AGENTS.md` entry point for AI context
- **MUST be deleted after feature is complete** (keeps repo clean)

### `.makeflow/history/` (committed)
- **Concise summaries only**
- Permanent record of changes
- Links to PRs and commits
- Indexed for easy reference

## Why This Structure?

### No Dates in Work Folders
Work folders use feature names only (not dates) because:
- ❌ Dated folders get stale ("started 2 weeks ago, still working on it")
- ✅ Feature names stay relevant
- ✅ One feature per branch enforced
- ✅ Dates added in history when complete

### Separate Work & History
- **Work folder**: Detailed, evolving, temporary
- **History folder**: Concise, permanent, indexed
- Keeps repo clean while maintaining full traceability

### AGENTS.md as Entry Point
- Single file AI agents can read for full context
- Always up-to-date with current state
- Clear structure for tracking progress
- Easy for humans to review

## 📚 Documentation Integration

This project's documentation is indexed for AI agents at:
- **`.makeflow/project/index.md`** - Entry point for all project documentation

**Purpose**: AI agents check this index to understand where to find:
- Technical architecture documentation
- API references and specifications
- Domain knowledge and business rules
- Coding standards and conventions
- Deployment and configuration guides

**For AI Agents**: If `.makeflow/project/index.md` exists, review it before starting work to understand the project context and locate relevant documentation for the feature you're building.

**Setup**: Use `.makeflow/workflows/00-setup/hook-docs.md` or `bootstrap-docs.md` to configure documentation integration.

## Using with Different AI Tools

### Codegen
```markdown
@codegen Use .makeflow/workflows/01-intake/from-ticket.md
Ticket: PROJ-123
```

### Cursor
```markdown
@Cursor Follow the workflow in .makeflow/workflows/01-intake/from-ticket.md

Ticket: PROJ-123
```

### Claude Code
```markdown
@Claude Execute .makeflow/workflows/01-intake/from-ticket.md

Context:
- Ticket: PROJ-123
- Project: [project name]
```

### Any AI Tool
Copy-paste the workflow content and provide context!

## Documentation

See the main [README.md](../README.md) for:
- Complete guide
- Design decisions
- FAQ
- Examples

## Support

- **Issues**: https://github.com/ajdurancr/makeflow/issues
- **Discussions**: https://github.com/ajdurancr/makeflow/discussions
