# Feature Prompt Template

Copy this template when requesting a feature from an AI tool.

---

## 🎯 Basic Feature Request

```markdown
@ai Use .makeflow/workflows/01-intake/from-ticket.md

Ticket: [TICKET-ID]
Additional Context: [Anything not in the ticket]
```

---

## 🎯 Feature Without Ticket

```markdown
@ai Use .makeflow/workflows/01-intake/from-idea.md

Feature Idea: [One sentence description]

Context:
- **Who needs this**: [User type or role]
- **Why**: [Problem or pain point]
- **Where**: [Which part of the system]
- **Current behavior**: [What happens now]
- **Desired behavior**: [What should happen]

Constraints:
- [Technical constraint 1]
- [Technical constraint 2]

Reference:
- [Link to design, if available]
- [Similar feature in the system]
```

---

## 🎯 Well-Defined Feature (Direct to Planning)

```markdown
@ai Use .makeflow/workflows/02-planning/create-spec.md

Feature: [Feature name]

Description: [2-3 sentences describing what needs to be built]

Acceptance Criteria:
- [ ] [Specific, testable criterion 1]
- [ ] [Specific, testable criterion 2]
- [ ] [Specific, testable criterion 3]

Technical Approach:
- [High-level approach]
- [Technologies to use]
- [Patterns to follow]

Reference:
- Similar code: [path/to/similar-code.ts]
- Documentation: [docs/relevant-doc.md]

Constraints:
- [Constraint 1]
- [Constraint 2]
```

---

## 🎯 Quick Feature (Skip Planning)

```markdown
@ai Use .makeflow/workflows/03-execution/execute-quick.md

Quick Feature: [Description]

What to do:
1. [Step 1]
2. [Step 2]
3. [Step 3]

Files to change:
- [path/to/file.ext]

Pattern to follow:
- [path/to/similar-implementation.ext]
```

---

## Examples

### Example 1: From Linear Ticket

```markdown
@codegen Use .makeflow/workflows/01-intake/from-ticket.md

Ticket: ASG-145
Additional Context: Product team wants this for Q1 roadmap demo
```

### Example 2: Vague Idea

```markdown
@cursor Use .makeflow/workflows/01-intake/from-idea.md

Feature Idea: Users should be able to export filtered data to Excel

Context:
- **Who needs this**: Administrators generating reports
- **Why**: Currently they copy/paste data manually (time-consuming)
- **Where**: Resources table in dashboard
- **Current behavior**: No export when filters applied
- **Desired behavior**: Export button that exports visible data

Constraints:
- Should work with all filter combinations
- Export filename should include date and filter description
- Must use existing xlsx library

Reference:
- Similar export in app/routes/dashboard.assignments.tsx
```

### Example 3: Well-Defined Feature

```markdown
@claude Use .makeflow/workflows/02-planning/create-spec.md

Feature: Resource bulk assignment system

Description: Enable users to select multiple resources via checkboxes and assign them all to a location in a single operation. Reduces time for batch assignments.

Acceptance Criteria:
- [ ] Checkboxes appear in resources table
- [ ] Bulk action toolbar shows when resources selected
- [ ] Assignment dialog supports bulk mode
- [ ] All assignments happen in single transaction
- [ ] Assignment history shows bulk operation

Technical Approach:
- Add checkbox column to resources table
- Use database transaction for atomic bulk operations
- Follow existing table patterns from @tanstack/react-table
- Reuse existing assignment dialog with bulk mode

Reference:
- Similar code: app/routes/dashboard.assignments.tsx
- Documentation: docs/resource-assignment-spec.md

Constraints:
- Must work with existing database schema (no migrations)
- Should handle 100+ resources efficiently
- Needs proper error handling for partial failures
```

---

## Tips for Writing Good Feature Prompts

### ✅ DO:
- Be specific about acceptance criteria
- Reference existing code/docs when possible
- Mention technical constraints upfront
- Provide context about why the feature is needed
- Link to tickets when available

### ❌ DON'T:
- Use vague language ("make it better", "improve performance")
- Skip acceptance criteria
- Forget about test requirements
- Ignore existing patterns in the codebase
- Rush past the planning stage for complex features

---

## Choosing the Right Workflow

| **Feature Complexity** | **Recommended Workflow** | **Time** |
|------------------------|---------------------------|----------|
| Vague idea needing clarity | `from-idea.md` | 10-20 min |
| Clear ticket | `from-ticket.md` | 5 min |
| Small, simple (< 2 hours) | `execute-quick.md` | < 2 hrs |
| Medium (2-8 hours) | `create-spec.md` → `create-plan.md` | 30 min planning<br>2-8 hrs execution |
| Large/complex (8+ hours) | Full workflow from intake through delivery | 1-2 hrs planning<br>8+ hrs execution |

