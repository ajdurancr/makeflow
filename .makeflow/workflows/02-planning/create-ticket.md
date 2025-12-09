# Workflow: Create Ticket from Specification

**Stage**: 02 - Planning  
**Purpose**: Generate a ticket in Linear/Jira/GitHub from spec  
**Time**: 5-10 minutes  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ You have a specification or clear requirements
- ✅ You need to track work in your ticketing system
- ✅ You want to create a formal ticket for team visibility

---

## Prerequisites

- [ ] Work folder exists with AGENTS.md
- [ ] Requirements are documented
- [ ] (Optional) spec.md or plan.md exists

---

## Instructions for AI Agent

### Step 1: Review Existing Documentation

Read from `.makeflow/work/[feature-name]/`:
- `AGENTS.md` - Overview and requirements
- `spec.md` (if exists) - Technical details
- `plan.md` (if exists) - Task breakdown

### Step 2: Generate Ticket Content

Create a ticket with:

**Title**: [Clear, concise feature name]

**Description**:
```markdown
## Problem
[What problem this solves - user perspective]

## Proposed Solution
[High-level approach]

## Acceptance Criteria
- [ ] [Specific, testable criterion 1]
- [ ] [Specific, testable criterion 2]
- [ ] [Specific, testable criterion 3]

## Technical Approach
[Brief technical summary]

**Files Affected**: ~[N files]  
**Estimated Effort**: [X hours]

## Related
- makeflow work: `.makeflow/work/[feature-name]/`
- Specification: [Link if exists]
- Design: [Link if exists]
```

**Labels/Tags**: [bug/feature/enhancement], [priority], [component]

**Estimate**: [Story points or hours]

### Step 3: Present Ticket Draft

```markdown
---

## 🎫 Ticket Draft

I've prepared a ticket based on your specification:

### Title
**[Feature Name]**

### Description
[Show the description]

### Labels
- Type: [feature/bug/task]
- Priority: [high/medium/low]
- Component: [component-name]

### Estimate
[X hours / Y story points]

---

**Options**:

1. **Create the ticket** - I'll add it to [Linear/Jira/GitHub]
2. **Modify first** - Tell me what to change
3. **Just give me the content** - You create it manually

Which do you prefer?
```

### Step 4: Create or Provide Ticket

**If user wants AI to create**:
- Use available ticket creation tools
- Create the ticket
- Get the ticket ID/URL
- Update AGENTS.md with ticket link

**If user will create manually**:
- Provide formatted content ready to copy-paste
- Show the ticket template clearly

### Step 5: Update AGENTS.md

Add to `.makeflow/work/[feature-name]/AGENTS.md`:

```markdown
## 🔗 Related Links

- **Ticket**: [TICKET-ID] - [URL]
- **PR**: [Will be added when created]
```

Add to decisions log:
```markdown
### [YYYY-MM-DD] - Ticket Created
**Ticket**: [TICKET-ID]  
**Link**: [URL]  
**Purpose**: Track work in team system
```

### Step 6: Confirm and Recommend Next Steps

```markdown
---

## ✅ Ticket Created

**Ticket**: [TICKET-ID]  
**URL**: [Link to ticket]

The ticket has been linked in `.makeflow/work/[feature-name]/AGENTS.md`

---

## 🚀 Next Steps

**Ready to start building**:

```
@ai Use .makeflow/workflows/03-execution/execute-task.md
Feature: [feature-name]
Task: [first-task]
```

Or if you have a plan:

```
@ai Use .makeflow/workflows/03-execution/execute-phase.md
Feature: [feature-name]
Phase: 1
```
```

---

## Example Ticket Content

### Example: Resource Multi-Filter

**Title**: Add multi-criteria filtering to resources table

**Description**:
```markdown
## Problem
Administrators need to filter resources by multiple criteria simultaneously (Type + Status + Location) to generate accurate reports. Currently, only single-criterion filtering is supported, forcing users to export and filter in Excel.

## Proposed Solution
Add multi-select dropdowns for each filterable column. Users can apply multiple filters with AND logic. Filtered state persists in URL params for sharing.

## Acceptance Criteria
- [ ] Can filter by multiple Types (e.g., Equipment + Tools)
- [ ] Can filter by multiple Statuses (e.g., Active + Maintenance)
- [ ] Can combine Type + Status + Location filters
- [ ] Filter results update in < 500ms with 1000+ resources
- [ ] URL params reflect active filters (shareable links)
- [ ] "Clear all filters" button resets to unfiltered view
- [ ] Filtered count shows "Showing X of Y resources"

## Technical Approach
Extend existing @tanstack/react-table filtering setup. Use existing MultiSelect component. Update Prisma queries with compound WHERE clauses. Add filter state to URL search params.

**Files Affected**: ~4 files  
**Estimated Effort**: 4-6 hours

## Related
- makeflow work: `.makeflow/work/resource-multi-filter/`
- Similar feature: `app/routes/dashboard.assignments.tsx`
- Component: `app/components/ui/multi-select.tsx`
```

**Labels**: feature, resources, priority:high  
**Estimate**: 5 story points

---

## Tips for Good Tickets

### ✅ DO:
- Write from user perspective (problem/solution)
- Make acceptance criteria specific and testable
- Include technical context
- Link to related work
- Estimate realistically

### ❌ DON'T:
- Use jargon in user-facing parts
- Skip acceptance criteria
- Be vague ("improve performance")
- Forget to link related work
- Under-estimate complexity

---

## Ticket Template for Copy-Paste

```markdown
## Problem
[What problem does this solve for users?]

## Proposed Solution
[How will we solve it?]

## Acceptance Criteria
- [ ] [Specific, testable criterion]
- [ ] [Specific, testable criterion]
- [ ] [Specific, testable criterion]

## Technical Approach
[Brief technical summary for developers]

**Files Affected**: ~[N files]  
**Estimated Effort**: [X hours]  
**Complexity**: [Simple/Medium/Complex]

## Related
- makeflow work: `.makeflow/work/[feature-name]/`
- Specification: [Link if exists]
- Design: [Link if exists]
- Similar feature: [Link to similar code]
```

---

## Validation Checklist

- [ ] Ticket title is clear and concise
- [ ] Problem statement written from user perspective
- [ ] Solution approach explained
- [ ] Acceptance criteria are specific and testable
- [ ] Technical approach summarized
- [ ] Estimate provided
- [ ] Related links included
- [ ] Labels/tags appropriate
- [ ] AGENTS.md updated with ticket link

---

## Integration with Other Workflows

**After ticket creation → Start building**:
```
.makeflow/workflows/03-execution/execute-task.md
```

or

```
.makeflow/workflows/03-execution/execute-phase.md
```

**Update ticket when complete**:
```
.makeflow/workflows/04-delivery/complete.md
```

---

**End of Workflow**

