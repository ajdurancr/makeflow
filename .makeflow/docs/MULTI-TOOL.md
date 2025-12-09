# Multi-Tool Integration Guide

How to use makeflow with different AI tools.

---

## Overview

**makeflow is AI-agnostic** - it works with any AI tool because:
- All workflows are plain markdown
- No special syntax or commands
- Copy-paste friendly
- Tool-independent instructions

---

## Codegen

### Setup

Codegen works natively with makeflow. No setup needed!

### Usage

```markdown
@codegen Use .makeflow/workflows/01-intake/from-ticket.md

Ticket: ASG-145
```

### Features

✅ **Reads work folders automatically** - Codegen can access `.makeflow/work/` to understand context  
✅ **Native GitHub integration** - Creates PRs, commits, etc.  
✅ **Async execution** - Codegen works while you do other things  

### Tips

- Codegen automatically reads AGENTS.md for context
- You can reference work folders: "Check `.makeflow/work/feature-name/` for context"
- Use threading to continue conversations

---

## Cursor IDE

### Setup

1. Open your project in Cursor
2. makeflow workflows are ready to use!

### Usage

**Method 1: Reference workflow file**
```markdown
@Cursor Follow .makeflow/workflows/01-intake/from-ticket.md

Ticket: ASG-145

Read the workflow file and execute each step.
```

**Method 2: Copy-paste workflow**
1. Open `.makeflow/workflows/01-intake/from-ticket.md`
2. Copy the "Instructions for AI Agent" section
3. Paste into Cursor with your context

### Features

✅ **IDE integration** - Works directly in your editor  
✅ **File access** - Can read/write files naturally  
✅ **Real-time** - Interactive development  

### Tips

- Use `Cmd/Ctrl + K` to reference workflow files
- Cursor can see your entire codebase
- Include file paths in your prompts
- Use "Composer" for multi-file changes

### Example Session

```markdown
# Step 1: Start feature
@Cursor Follow .makeflow/workflows/01-intake/from-ticket.md

Ticket: ASG-145 (Add multi-select filters)

# Step 2: Continue (later)
@Cursor I'm continuing work on ASG-145.

Read `.makeflow/work/resource-multi-filter/AGENTS.md` and let's implement Task 1.1.

# Step 3: Create PR
@Cursor Follow .makeflow/workflows/04-delivery/create-pr.md

Feature: resource-multi-filter
```

---

## Claude Code

### Setup

Use Claude via web or API with makeflow.

### Usage

**Method: Provide full context**
```markdown
@Claude Execute workflow: .makeflow/workflows/01-intake/from-ticket.md

Project Context:
- Repository: resource-management-system
- Tech Stack: React, TypeScript, Prisma
- My Role: Full-stack developer

Ticket: ASG-145 - Add multi-select filtering

Please follow the workflow steps precisely.
```

### Features

✅ **Long context** - Can process entire workflows  
✅ **Detailed responses** - Thorough explanations  
✅ **Multi-step planning** - Good at breaking down work  

### Tips

- Provide more context upfront (Claude doesn't see your files)
- Copy workflow content for complex workflows
- Ask Claude to confirm understanding before proceeding
- Use artifacts for code generation

### Example Session

```markdown
# Initial request
@Claude I'm using the makeflow workflow system for development.

Execute: .makeflow/workflows/01-intake/from-idea.md

Feature Idea: Users should be able to export filtered data to Excel

Context:
- Target users: Administrators generating reports
- Current situation: No export when filters applied
- Tech stack: React, Remix, Prisma
- Similar feature exists for assignments

Please follow the workflow and ask clarifying questions.

# Claude will ask questions, you answer, then...

# Continue
Great answers! Now please create the work folder and AGENTS.md.

# Later
I'm continuing work on resource-export.

Here's the current AGENTS.md content:
[paste AGENTS.md]

Let's implement Task 1.1: Add export button component.
```

---

## GitHub Copilot

### Setup

Copilot works inline - use makeflow workflows as guidance.

### Usage

1. **Open workflow file** in editor
2. **Read the steps** to understand approach
3. **Code with Copilot** using workflow as guide
4. **Update AGENTS.md** manually as you progress

### Features

✅ **Inline suggestions** - Code completion  
✅ **Fast** - Real-time assistance  
✅ **Context-aware** - Understands your files  

### Tips

- Keep workflow file open in split view
- Add comments describing next step (Copilot suggests based on comments)
- Update AGENTS.md checklist as you complete tasks

### Example

```typescript
// Following makeflow task 1.1: Add multi-select filter component
// Copilot will suggest based on this comment

export function TypeMultiSelect() {
  // Copilot suggests component implementation
}
```

---

## ChatGPT

### Setup

Use ChatGPT web or API with makeflow.

### Usage

**Copy workflow content and provide context**:

```markdown
I'm using a workflow system for development. Here's the workflow:

[Copy .makeflow/workflows/01-intake/from-ticket.md content]

Please execute this workflow for:
- Ticket: ASG-145
- Project: Resource Management System
- Tech: React, TypeScript, Prisma

Follow each step precisely.
```

### Features

✅ **Accessible** - Available via web  
✅ **Conversational** - Natural interaction  
✅ **Flexible** - Works with any workflow  

### Tips

- Paste workflow content in first message
- Provide codebase context
- Save important responses for reference
- Continue conversations with "Read my previous messages for context"

---

## Combining Tools

You can use different tools for different stages!

### Example: Codegen + Cursor

**Planning (Codegen)**:
```markdown
@codegen Use .makeflow/workflows/02-planning/create-spec.md
Feature: resource-export
```

**Implementation (Cursor)**:
```markdown
@Cursor Follow .makeflow/workflows/03-execution/execute-task.md

Feature: resource-export
Task: Task 1.1

[Cursor has IDE access for faster coding]
```

**PR Creation (Codegen)**:
```markdown
@codegen Use .makeflow/workflows/04-delivery/create-pr.md
Feature: resource-export
```

### Example: Claude + GitHub Copilot

**Design (Claude)**:
```markdown
@Claude Help me design the architecture for ASG-145

[Claude provides detailed design]
```

**Implementation (Copilot)**:
```typescript
// Use Claude's design + Copilot's inline suggestions
```

**PR Description (Claude)**:
```markdown
@Claude Create PR description for ASG-145

[Claude writes comprehensive PR description]
```

---

## Tool Comparison

| Feature | Codegen | Cursor | Claude | ChatGPT | Copilot |
|---------|---------|--------|--------|---------|---------|
| **File Access** | ✅ Yes | ✅ Yes | ❌ No | ❌ No | ✅ Yes |
| **Async Work** | ✅ Yes | ❌ No | ❌ No | ❌ No | ❌ No |
| **IDE Integration** | ❌ No | ✅ Yes | ❌ No | ❌ No | ✅ Yes |
| **Long Context** | ✅ Yes | ✅ Yes | ✅ Yes | ⚠️ Limited | ⚠️ Limited |
| **makeflow Native** | ✅ Yes | ⚠️ Manual | ⚠️ Manual | ⚠️ Manual | ⚠️ Manual |
| **Best For** | Full workflows | Interactive dev | Design/planning | General help | Code completion |

---

## Best Practices Across Tools

### 1. Always Reference AGENTS.md

**Codegen**:
```markdown
@codegen Continue work on feature-name
[Automatically reads AGENTS.md]
```

**Other tools**:
```markdown
@tool I'm working on feature-name.

Here's the current state from AGENTS.md:
[paste AGENTS.md content]

Let's continue with [next task].
```

### 2. Keep Work Folders Updated

All tools benefit from updated AGENTS.md:
- Current progress
- Decisions made
- Next steps

Update it regardless of which tool you use.

### 3. Use Tools for Their Strengths

**Codegen**: Full workflows, PR creation, async work  
**Cursor**: Interactive development, quick iterations  
**Claude**: Architecture, design decisions, documentation  
**ChatGPT**: General help, learning, brainstorming  
**Copilot**: Fast coding, autocomplete, refactoring  

### 4. Maintain Consistency

Regardless of tool:
- Follow makeflow workflows
- Update work folder
- Write tests
- Document decisions
- Complete the full cycle

---

## Troubleshooting

### Tool doesn't follow workflow

**Solution**: Be more explicit:
```markdown
You MUST follow this workflow step-by-step:

Step 1: [describe]
Step 2: [describe]
...

Do not skip steps. Confirm you understand before proceeding.
```

### Tool can't access files

**Solution**: Copy content to the tool:
```markdown
Here's the current AGENTS.md:
[paste content]

Here's the relevant code:
[paste code]

Now follow the workflow...
```

### Tool loses context

**Solution**: Summarize periodically:
```markdown
Summary of our progress:
- Feature: resource-export
- Current phase: Execution
- Completed: Tasks 1.1, 1.2
- Next: Task 1.3 - Add tests
- Location: .makeflow/work/resource-export/

Let's continue with Task 1.3.
```

---

## Your Preferred Setup?

Mix and match tools as you prefer:
- ✅ All Codegen
- ✅ All Cursor
- ✅ Planning with Claude, coding with Cursor
- ✅ Design with ChatGPT, implementation with Copilot
- ✅ Any combination!

**makeflow works with all of them** because it's just markdown. 🎉

---

**Questions?** Open an issue or discussion on GitHub!

