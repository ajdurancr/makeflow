# Workflow: Start from Ticket

**Stage**: 01 - Intake  
**Purpose**: Validate an existing ticket and create work folder  
**Time**: 5-10 minutes  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ You have a ticket from Linear, Jira, GitHub Issues, etc.
- ✅ The ticket has some description and requirements
- ✅ You want to start working on it with AI assistance

---

## Prerequisites

- [ ] Ticket ID/number
- [ ] Access to the ticket system
- [ ] Project repository cloned locally

---

## Instructions for AI Agent

When a user invokes this workflow, follow these steps:

### Step 0: Review Project Documentation (if available)

**Before starting**, check if `.makeflow/project/index.md` exists:
- **If it exists**: Review it to understand the project's architecture, conventions, and relevant documentation
- **Purpose**: This helps you better understand the context when validating the ticket and asking clarifying questions
- **What to look for**: Architecture patterns, API references, domain knowledge that might relate to this ticket

### Step 1: Read the Ticket

**Ask the user for**:
- Ticket ID/URL
- Any additional context not in the ticket

**Then**:
1. Read the ticket details (if you have access)
2. Extract:
   - Title
   - Description
   - Acceptance criteria (if present)
   - Any technical requirements
   - Links to related tickets/docs

**If ticket is not accessible, ask user to provide**:
- Ticket summary
- Requirements
- Acceptance criteria

### Step 2: Validate Clarity

Check if the ticket is clear enough to start work:

**Ask yourself**:
- [ ] Is the goal clear? (What needs to be built/fixed)
- [ ] Are acceptance criteria present? (How to verify it's done)
- [ ] Are there any ambiguities?
- [ ] Is the scope reasonable? (Not too large)
- [ ] Are there technical constraints mentioned?

**If any answers are NO**, proceed to Step 2a.  
**If all answers are YES**, skip to Step 3.

#### Step 2a: Clarify Ambiguities

**Present to user**:
```markdown
## 🔍 Ticket Validation: [TICKET-ID]

**Ticket Title**: [title]

**What I Understand**:
- Goal: [summarize goal]
- Acceptance Criteria: [list criteria if present, or "Not specified"]
- Scope: [size estimate]

**Ambiguities/Questions**:
1. [Question 1 about unclear aspect]
2. [Question 2 about missing detail]
3. [Question 3 about technical constraint]

**Recommendation**:
- Option 1: Answer these questions, then I'll create the work folder
- Option 2: Use `.makeflow/workflows/01-intake/from-idea.md` for deeper clarification

Which do you prefer?
```

**Wait for user response** before proceeding.

### Step 3: Determine Complexity

Estimate the complexity to recommend the right workflow:

**Complexity Factors**:
- [ ] Number of files affected (1-2 files = simple, 3-5 = medium, 6+ = complex)
- [ ] New patterns vs existing patterns (existing = simple, new = complex)
- [ ] Testing requirements (unit only = simple, integration = medium, e2e = complex)
- [ ] Multiple systems involved? (single system = simple, multiple = complex)

**Complexity Assessment**:
- **Simple** (< 2 hours): Quick fix or small feature
- **Medium** (2-8 hours): Feature with multiple components
- **Complex** (8+ hours): Large feature or architectural change

### Step 4: Create Work Folder

Create the following structure in `.makeflow/work/[feature-slug]/`:

```
.makeflow/work/[feature-slug]/
├── AGENTS.md           # Entry point (create this file)
├── spec.md             # Specification (if needed for medium/complex)
└── plan.md             # Task plan (if needed for medium/complex)
```

**Feature slug naming**:
- Lowercase
- Hyphen-separated
- Descriptive but concise
- Example: `user-bulk-export`, `fix-special-chars`, `add-filtering`

#### AGENTS.md Template

Create `.makeflow/work/[feature-slug]/AGENTS.md` with this content:

```markdown
# [Feature Name]

> **Ticket**: [TICKET-ID]  
> **Created**: [YYYY-MM-DD]  
> **Status**: 📝 Planning  
> **AI Tool**: [Codegen/Cursor/Claude/Other]

---

## 📋 Overview

**What**: [One sentence description]

**Why**: [Business/user value]

**Ticket Link**: [URL to ticket]

---

## 🎯 Requirements

**From Ticket**:
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]

**Additional Context**:
- [Any context not in ticket]

---

## ✅ Acceptance Criteria

- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

---

## 📐 Complexity Assessment

**Size**: [Simple/Medium/Complex]  
**Estimated Time**: [X hours]  
**Files Affected**: ~[N files]

---

## 🗺️ Next Steps

**Recommended Workflow**:

[Choose based on complexity]

**For Simple**:
```markdown
@ai Use .makeflow/workflows/03-execution/execute-quick.md
Feature: [feature-slug]
```

**For Medium**:
```markdown
@ai Use .makeflow/workflows/02-planning/create-plan.md
Feature: [feature-slug]
```

**For Complex**:
```markdown
@ai Use .makeflow/workflows/02-planning/create-spec.md
Feature: [feature-slug]
```

---

## 📝 Progress Log

### [YYYY-MM-DD]
- Created work folder from ticket [TICKET-ID]
- Assessed complexity: [size]
- Ready for [next workflow]
```

### Step 5: Present to User

**Show summary**:
```markdown
---

## ✅ Work Folder Created

**Feature**: `[feature-slug]`  
**Location**: `.makeflow/work/[feature-slug]/`  
**Entry Point**: `.makeflow/work/[feature-slug]/AGENTS.md`

**Ticket**: [TICKET-ID] - [Title]  
**Complexity**: [Simple/Medium/Complex]  
**Estimated Time**: [X hours]

---

## 📊 What I Found

**Clear Requirements**: [Yes/No]  
**Acceptance Criteria**: [Yes/No]  
**Files Likely Affected**: ~[N files]

**Ambiguities** (if any):
- [List any remaining unclear points]

---

## 🚀 Next Steps

**Recommended**: [Workflow based on complexity]

[Show the specific command with feature slug]

**Alternative Options**:
1. Review `AGENTS.md` and provide additional context
2. Adjust complexity assessment if needed
3. Clarify ambiguities before proceeding

---

Ready to proceed? Let me know!
```

---

## Example Usage

### Example 1: Clear Ticket (Simple)

**User**:
```markdown
@codegen Use .makeflow/workflows/01-intake/from-ticket.md

Ticket: PROJ-145
```

**AI Response**:
```markdown
## ✅ Work Folder Created

**Feature**: `resource-export`
**Location**: `.makeflow/work/resource-export/`
**Entry Point**: `.makeflow/work/resource-export/AGENTS.md`

**Ticket**: PROJ-145 - Add Excel Export to Resources

**What I Found**:
- ✅ Clear goal: Add export button to resources table
- ✅ Acceptance criteria provided
- ✅ Similar feature exists (assignments export)
- ✅ Technical approach clear

**Complexity**: Simple  
**Estimated Time**: 2-3 hours  
**Files Affected**: ~3 files

---

## 🚀 Recommended Next Step

Since this is a **simple** feature with clear requirements:

```
@codegen Use .makeflow/workflows/02-planning/create-plan.md
Feature: resource-export
```

This will create a task plan and you can start building immediately!

Ready to proceed?
```

---

### Example 2: Unclear Ticket

**User**:
```markdown
@cursor Use .makeflow/workflows/01-intake/from-ticket.md

Ticket: PROJ-200
```

**AI Response**:
```markdown
## 🔍 Ticket Validation: PROJ-200

**Ticket Title**: Improve filtering

**What I Understand**:
- Goal: Make filtering "better" somehow
- Acceptance Criteria: Not specified
- Scope: Unknown

**Ambiguities/Questions**:
1. Which filtering? (Resources, assignments, users, all of them?)
2. What's wrong with current filtering? (Too slow? Missing features? Confusing UI?)
3. What does "improved" mean? (Performance? More options? Better UX?)
4. Are there specific filter types needed? (Date ranges? Multi-select? Search?)

**Recommendation**:
This ticket needs clarification before we can start.

**Option 1**: Answer the questions above  
**Option 2**: Use `.makeflow/workflows/01-intake/from-idea.md` for deeper discovery

Which do you prefer?
```

---

## Tips for AI Agents

### Creating Good Feature Slugs
- ✅ `user-bulk-export` (clear, descriptive)
- ✅ `fix-excel-special-chars` (includes fix type)
- ✅ `add-multi-filter` (includes add action)
- ❌ `proj-145` (ticket ID, not descriptive)
- ❌ `new-feature` (too vague)
- ❌ `updates` (not specific)

### Assessing Complexity
**Simple** (< 2 hours):
- Single file or component
- Following existing patterns
- Clear requirements
- Example: Add button, fix bug, update text

**Medium** (2-8 hours):
- Multiple files/components
- Some new patterns needed
- Moderate testing
- Example: New feature, refactor component, API integration

**Complex** (8+ hours):
- Multiple systems/files
- New architecture/patterns
- Extensive testing needed
- Example: Large feature, system redesign, new module

### When to Recommend Each Planning Workflow

**Skip planning** (`execute-quick.md`):
- Very small changes (< 1 hour)
- Following exact pattern
- No ambiguity

**Create plan** (`create-plan.md`):
- Simple to medium features
- Requirements are clear
- Standard approach

**Create spec** (`create-spec.md`):
- Complex features
- Ambiguous requirements
- Novel solutions needed
- Multiple stakeholders

---

## Integration with Other Workflows

**Next Workflows** (based on complexity):

**Simple → Quick Execution**:
```
.makeflow/workflows/03-execution/execute-quick.md
```

**Medium → Create Plan**:
```
.makeflow/workflows/02-planning/create-plan.md
```

**Complex → Create Spec**:
```
.makeflow/workflows/02-planning/create-spec.md
```

---

## Validation Checklist

Before completing this workflow, verify:

- [ ] Work folder created in `.makeflow/work/[feature-slug]/`
- [ ] `AGENTS.md` file created with all required sections
- [ ] Ticket requirements extracted and documented
- [ ] Ambiguities identified (if any)
- [ ] Complexity assessed
- [ ] Next workflow recommended
- [ ] User has clear next steps

---

## Notes

- This workflow is AI-agnostic - works with any AI tool
- The AGENTS.md file serves as the entry point for all subsequent work
- Work folder will be deleted after feature completion (summarized to history)
- Keep the feature slug simple and descriptive

---

**End of Workflow**
