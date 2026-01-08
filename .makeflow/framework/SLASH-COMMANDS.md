# Makeflow Slash Commands Guide

**Quick access to makeflow workflows in Claude Code and Cursor**

---

## Table of Contents

1. [Overview](#overview)
2. [Setup](#setup)
3. [Available Commands by Stage](#available-commands-by-stage)
4. [Quick Usage Examples](#quick-usage-examples)
5. [End-to-End Workflow Examples](#end-to-end-workflow-examples)
6. [Tips and Best Practices](#tips-and-best-practices)

---

## Overview

Slash commands provide quick access to makeflow workflows directly from your IDE. Instead of typing long paths like `.makeflow/workflows/01-intake/from-ticket.md`, you can simply use `/01-from-ticket`.

### Key Features

- **Stage-Prefixed**: Commands are numbered `00-04` to show workflow progression
- **Centralized Storage**: All commands in `.agents/commands/`
- **Symlinked Access**: Available in both Claude Code (`.claude/commands/`) and Cursor (`.cursor/commands/`)
- **AI-Agnostic**: Same commands work across different AI tools

### Directory Structure

```
.agents/commands/           # Central command storage
├── 00-bootstrap-docs.md
├── 00-hook-docs.md
├── 00-update-makeflow.md
├── 01-from-bug.md
├── 01-from-idea.md
├── 01-from-ticket.md
├── 02-create-plan.md
├── 02-create-spec.md
├── 02-create-ticket.md
├── 03-execute-all-phases.md
├── 03-execute-phase.md
├── 03-execute-quick.md
├── 03-execute-task.md
├── 03-execute-task-without-tests.md
├── 04-complete.md
├── 04-create-pr.md
└── 04-update-docs.md

.claude/commands/  -> ../.agents/commands/   # Symlink for Claude Code
.cursor/commands/  -> ../.agents/commands/   # Symlink for Cursor
```

---

## Setup

The slash commands are already set up in this project. If you're setting up makeflow in a new project:

```bash
# From project root
mkdir -p .agents/commands .claude .cursor

# Create symlinks
ln -sf ../.agents/commands .claude/commands
ln -sf ../.agents/commands .cursor/commands
```

The command files are automatically created when you copy makeflow to your project.

---

## Available Commands by Stage

### Stage 00: Setup (Run Once Per Project)

These workflows set up your project's integration with makeflow.

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/00-bootstrap-docs` | Create documentation from scratch | New projects without docs |
| `/00-hook-docs` | Connect to existing documentation | Projects with existing docs |
| `/00-update-makeflow` | Update makeflow framework | Monthly/quarterly maintenance |

**Workflow Details**: [.makeflow/workflows/00-setup/](.makeflow/workflows/00-setup/)

---

### Stage 01: Intake (Clarify Requirements)

Transform vague ideas into clear, actionable requirements.

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/01-from-ticket` | Start from existing ticket/issue | Ticket already exists |
| `/01-from-idea` | Start from vague concept | Raw idea or feature request |
| `/01-from-bug` | Handle bug reports | Fixing a bug |

**Output**: Creates work folder with initial AGENTS.md

**Workflow Details**: [.makeflow/workflows/01-intake/](.makeflow/workflows/01-intake/)

---

### Stage 02: Planning (Create Specifications)

Break down requirements into executable specifications.

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/02-create-spec` | Full technical specification | Complex features (1-5 days) |
| `/02-create-plan` | Break into tasks and phases | Medium features (4-8 hours) |
| `/02-create-ticket` | Create ticket from spec | Delegating to others |

**Output**: Updates AGENTS.md with spec/plan, creates spec.md or plan.md

**Workflow Details**: [.makeflow/workflows/02-planning/](.makeflow/workflows/02-planning/)

---

### Stage 03: Execution (Build & Validate)

Implement with built-in validation and testing.

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/03-execute-quick` | Fast implementation (< 1 hour) | Simple changes, bug fixes |
| `/03-execute-task` | Build one task with tests | Single task from plan |
| `/03-execute-task-without-tests` | Build one task, skip tests | Prototyping, non-critical code |
| `/03-execute-phase` | Complete one phase (2-4 hours) | One phase from plan |
| `/03-execute-all-phases` | Complete entire feature (4-8 hours) | Execute full plan at once |

**Output**: Working code, passing tests, updated AGENTS.md

**Workflow Details**: [.makeflow/workflows/03-execution/](.makeflow/workflows/03-execution/)

---

### Stage 04: Delivery (Ship & Document)

Create PRs, update docs, and archive completed work.

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/04-update-docs` | Update project documentation | Major features, API changes |
| `/04-create-pr` | Create production-ready PR | Ready to ship |
| `/04-complete` | Summarize and archive | After PR merged |

**Output**: PR created, docs updated, work summarized to history

**Workflow Details**: [.makeflow/workflows/04-delivery/](.makeflow/workflows/04-delivery/)

---

## Quick Usage Examples

### Using Commands in Claude Code

```markdown
/01-from-ticket
Ticket: ASG-145
```

### Using Commands in Cursor

```markdown
/01-from-ticket
Ticket: ASG-145
```

### Providing Context

All commands accept context after invocation:

```markdown
/01-from-idea
Feature Idea: Add bulk resource assignment to reduce manual work

Users need to assign multiple resources to a job at once instead of
clicking through the UI for each resource individually.
```

### Chaining Commands

Execute multiple stages in sequence:

```markdown
# First, clarify requirements
/01-from-ticket
Ticket: ASG-145

# [AI completes intake]

# Then create a plan
/02-create-plan

# [AI creates plan]

# Execute the plan
/03-execute-all-phases

# [AI builds feature]

# Ship it
/04-create-pr
/04-complete
```

---

## End-to-End Workflow Examples

### Example 1: Simple Bug Fix (30 minutes)

**Scenario**: Excel export fails with special characters

```markdown
# 1. Clarify the bug
/01-from-bug
Bug: Excel export crashes when filename contains special characters like / or \

Steps to reproduce:
1. Create report named "Q4/2024 Sales"
2. Click "Export to Excel"
3. Application crashes

Expected: Should sanitize filename or show error
Actual: Unhandled exception

# [AI investigates, updates AGENTS.md with findings]

# 2. Quick fix (< 1 hour)
/03-execute-quick

# [AI implements fix with tests]

# 3. Create PR and complete
/04-create-pr
/04-complete
```

**Time**: 30 minutes
**Stages Used**: Intake → Execution → Delivery

---

### Example 2: Medium Feature (4-8 hours)

**Scenario**: Add filtering to resource list

```markdown
# 1. Start from ticket
/01-from-ticket
Ticket: ASG-145

# [AI reads ticket, clarifies requirements in AGENTS.md]

# 2. Create execution plan
/02-create-plan

# [AI creates plan with phases and tasks]

# 3. Execute phase by phase
/03-execute-phase
Phase: 1

# [AI completes Phase 1]

/03-execute-phase
Phase: 2

# [AI completes Phase 2]

# Alternative: Execute all at once
# /03-execute-all-phases

# 4. Ship it
/04-create-pr
/04-complete
```

**Time**: 4-8 hours
**Stages Used**: Intake → Planning → Execution → Delivery

---

### Example 3: Complex Feature (1-5 days)

**Scenario**: New bulk assignment system

```markdown
# 1. Start from vague idea
/01-from-idea
Feature Idea: Bulk resource assignment

Users need to assign multiple resources to multiple jobs at once.
Should support filtering, validation, and conflict detection.

# [AI clarifies requirements, asks questions, updates AGENTS.md]

# 2. Create detailed specification
/02-create-spec

# [AI creates full technical spec in spec.md]

# 3. Break into execution plan
/02-create-plan

# [AI creates multi-phase plan from spec]

# 4. Execute phase by phase
/03-execute-phase
Phase: 1

# [Complete Phase 1]

/03-execute-phase
Phase: 2

# [Complete Phase 2... continue for all phases]

# 5. Update documentation
/04-update-docs

# [AI updates project docs]

# 6. Ship it
/04-create-pr
/04-complete
```

**Time**: 1-5 days
**Stages Used**: Intake → Planning (spec + plan) → Execution → Delivery

---

### Example 4: Prototype Without Tests

**Scenario**: Experimenting with new approach

```markdown
# 1. Clarify the experiment
/01-from-idea
Experiment: Try using Web Workers for heavy calculations

Want to see if offloading to Web Workers improves UI responsiveness
when processing large datasets.

# [AI clarifies scope]

# 2. Quick plan (optional for experiments)
/02-create-plan

# [AI creates lightweight plan]

# 3. Prototype without tests
/03-execute-task-without-tests
Task: Implement Web Worker for calculation offloading

# [AI builds prototype, skips tests]

# 4. If successful, add tests and ship
# /03-execute-task
# Task: Add tests for Web Worker implementation
#
# /04-create-pr
# /04-complete
```

**Time**: 2-4 hours
**Stages Used**: Intake → Planning → Execution (no tests) → (Optionally add tests and deliver)

---

## Tips and Best Practices

### Choosing the Right Command

**Start of work**:
- Have a ticket? → `/01-from-ticket`
- Have a vague idea? → `/01-from-idea`
- Fixing a bug? → `/01-from-bug`

**Planning**:
- Complex feature (1-5 days)? → `/02-create-spec` then `/02-create-plan`
- Medium feature (4-8 hours)? → `/02-create-plan`
- Simple change (< 1 hour)? → Skip planning, go to `/03-execute-quick`

**Execution**:
- Quick fix (< 1 hour)? → `/03-execute-quick`
- Want to execute entire plan? → `/03-execute-all-phases`
- Prefer incremental progress? → `/03-execute-phase` or `/03-execute-task`
- Prototyping? → `/03-execute-task-without-tests`

**Delivery**:
- Major feature with API changes? → `/04-update-docs` first
- Always → `/04-create-pr`
- Always after PR merged → `/04-complete`

### Command Workflow Patterns

**Pattern 1: Bug Fix**
```
/01-from-bug → /03-execute-quick → /04-create-pr → /04-complete
```

**Pattern 2: Simple Feature**
```
/01-from-ticket → /03-execute-quick → /04-create-pr → /04-complete
```

**Pattern 3: Medium Feature**
```
/01-from-ticket → /02-create-plan → /03-execute-all-phases → /04-create-pr → /04-complete
```

**Pattern 4: Complex Feature**
```
/01-from-idea → /02-create-spec → /02-create-plan → /03-execute-phase (multiple) → /04-update-docs → /04-create-pr → /04-complete
```

### Providing Good Context

When invoking commands, provide:

1. **Clear identifiers** (ticket IDs, bug numbers)
2. **Expected behavior** (what should happen)
3. **Current behavior** (what actually happens)
4. **Business value** (why this matters)
5. **Constraints** (technical limitations, deadlines)

**Good example**:
```markdown
/01-from-ticket
Ticket: ASG-145
Title: Add bulk resource assignment

Business value: Reduce time spent on manual assignments by 80%
Current: Users must click through 5 screens per resource
Desired: Select multiple resources, assign to multiple jobs at once
Constraints: Must maintain existing security checks
```

**Poor example**:
```markdown
/01-from-ticket
ASG-145
```

### Checking Progress

At any point, you can ask the AI:
- "What's the current status?"
- "Show me the AGENTS.md"
- "What's next?"
- "What phase are we on?"

The AI will read `.makeflow/work/[feature-name]/AGENTS.md` to answer.

### Workflow Flexibility

You don't have to use all stages:

**Skip planning** for simple changes:
```
/01-from-bug → /03-execute-quick → /04-create-pr → /04-complete
```

**Skip spec, just plan** for medium features:
```
/01-from-ticket → /02-create-plan → /03-execute-phase → /04-create-pr → /04-complete
```

**Use everything** for complex features:
```
/01-from-idea → /02-create-spec → /02-create-plan → /03-execute-phase → /04-update-docs → /04-create-pr → /04-complete
```

### Version Control Best Practices

**Work folders are committed**:
- AI tools need to read them
- Provides context across sessions
- Cleaned up after completion

**Commit frequently during execution**:
```markdown
/03-execute-task
Task: Implement bulk selection UI

# [AI implements, run tests]

# Good practice: Commit after each task
```

**Use feature branches**:
- Create branch at intake stage
- Push regularly
- PR created automatically by `/04-create-pr`

### Multi-Session Work

Slash commands work across sessions:

**Day 1**:
```markdown
/01-from-ticket
Ticket: ASG-145

/02-create-plan
/03-execute-phase
Phase: 1
```

**Day 2** (new session):
```markdown
# AI remembers context from AGENTS.md
/03-execute-phase
Phase: 2

/04-create-pr
/04-complete
```

### Working with Multiple Features

Work on one feature at a time:

**Current feature in work folder**:
```
.makeflow/work/bulk-assignment/
```

**Want to switch?** Complete current feature first:
```markdown
/04-create-pr
/04-complete

# Now start new feature
/01-from-ticket
Ticket: ASG-146
```

**Emergency fix needed?**
1. Stash current work folder manually
2. Use `/01-from-bug` for quick fix
3. Use `/03-execute-quick`
4. Use `/04-create-pr` and `/04-complete`
5. Restore previous work folder

---

## Troubleshooting

### "Command not found"

**Cause**: Symlinks not created or broken

**Fix**:
```bash
# Recreate symlinks
rm -f .claude/commands .cursor/commands
ln -sf ../.agents/commands .claude/commands
ln -sf ../.agents/commands .cursor/commands
```

### "Multiple work folders exist"

**Cause**: Previous feature not completed

**Fix**: Complete old feature first:
```markdown
# Check what's in work/
ls .makeflow/work/

# Complete the old feature
/04-complete

# Or manually move to history if abandoned
```

### "AI doesn't remember context"

**Cause**: AGENTS.md not updated or work folder missing

**Fix**: Check AGENTS.md exists:
```bash
cat .makeflow/work/[feature-name]/AGENTS.md
```

If missing, provide context manually:
```markdown
Current feature: bulk-assignment
Status: Phase 1 complete, starting Phase 2
Context: [describe what's been done]

/03-execute-phase
Phase: 2
```

### "Tests are failing"

**Cause**: Implementation issue

**Fix**: Let the workflow handle it:
- Execution workflows include test validation
- AI will fix failing tests before marking task complete
- If tests keep failing, ask AI to investigate

### "Want to skip a stage"

**Cause**: Stage not needed for this type of work

**Fix**: That's fine! Workflows are flexible:
- Simple bug? Skip planning, go straight to `/03-execute-quick`
- Have existing spec? Skip `/02-create-spec`, go to `/02-create-plan`
- Small change? Skip `/04-update-docs`

Use what makes sense for your specific situation.

---

## Advanced: Creating Custom Commands

You can add custom commands to `.agents/commands/`:

```bash
# Create custom command
cat > .agents/commands/99-custom-review.md << 'EOF'
# Custom Code Review (Command)

## Instructions

1. You will receive a prompt or context for this workflow.

2. Perform a thorough code review focusing on:
   - Security vulnerabilities
   - Performance issues
   - Code style consistency
   - Test coverage

---

**Input Context:**
EOF
```

Now use `/99-custom-review` in Claude Code or Cursor.

---

## Next Steps

1. **Try a simple workflow**: Start with `/01-from-bug` on a known issue
2. **Experiment with planning**: Use `/02-create-plan` on a medium feature
3. **Build something**: Execute a full workflow from intake to delivery
4. **Customize**: Add your own commands for team-specific workflows

---

## Related Documentation

- **[Complete Guide](.makeflow/framework/GUIDE.md)** - Full makeflow documentation
- **[Workflows](.makeflow/workflows/)** - Detailed workflow implementations
- **[Multi-Tool Integration](.makeflow/framework/MULTI-TOOL.md)** - Using different AI tools
- **[Examples](.makeflow/framework/EXAMPLES.md)** - Real-world examples
- **[README](../../README.md)** - Quick start and overview

---

**Questions or issues?** Check the [FAQ](.makeflow/framework/DECISIONS.md#faq) or [open an issue](https://github.com/ajdurancr/makeflow/issues).

Happy building with makeflow slash commands! 🚀
