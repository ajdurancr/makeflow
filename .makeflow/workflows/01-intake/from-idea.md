# Workflow: Start from Idea

**Stage**: 01 - Intake  
**Purpose**: Transform a vague idea into clear requirements  
**Time**: 15-30 minutes  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ You have a vague idea or concept
- ✅ No formal ticket exists yet
- ✅ Requirements need clarification
- ✅ You want to explore if the idea is feasible

---

## Prerequisites

- [ ] General idea of what you want to build
- [ ] Understanding of the problem being solved
- [ ] Access to project codebase (for context)

---

## Instructions for AI Agent

When a user invokes this workflow, follow these steps:

### Step 1: Capture the Initial Idea

**Ask the user for**:
```markdown
Please provide:

1. **Feature Idea** (1-2 sentences)
2. **Problem/Pain Point** (What problem does this solve?)
3. **Target Users** (Who will use this?)
4. **Current Situation** (What happens today without this?)
5. **Desired Outcome** (What should happen with this feature?)
```

**If user provides minimal info**, prompt for more details with specific questions.

### Step 2: Clarifying Questions

Based on the initial idea, ask targeted questions:

**About Scope**:
- How big should this be? (MVP vs full-featured)
- What's in scope? What's explicitly out of scope?
- Are there phases or can this be built incrementally?

**About Users**:
- Who exactly will use this? (Roles, personas)
- How often will they use it?
- What's their technical skill level?

**About Implementation**:
- Are there similar features in the system we can reference?
- Are there existing patterns or libraries to use?
- Any technical constraints? (Performance, compatibility, etc.)

**About Success**:
- How will we know this is successful?
- What metrics matter?
- How will we test this?

**Present questions to user**:
```markdown
## 🤔 Clarifying Questions

To transform this idea into a clear specification, I need to understand:

**Scope & Size**:
1. [Question about scope]
2. [Question about MVP vs full version]

**Users & Usage**:
3. [Question about who uses this]
4. [Question about how often]

**Implementation**:
5. [Question about technical approach]
6. [Question about constraints]

**Success Criteria**:
7. [Question about how to measure success]
8. [Question about testing]

Please answer these questions, and I'll create a clear specification.
```

**Wait for user responses** before proceeding.

### Step 3: Research Existing Patterns

**Search the codebase for**:
- Similar features
- Related components
- Applicable patterns
- Potential conflicts

**Present findings**:
```markdown
## 📚 Codebase Research

**Similar Features Found**:
- `path/to/similar-feature.ext` - [What's similar]
- `path/to/related-component.ext` - [How it relates]

**Patterns to Follow**:
- [Pattern 1 from docs or existing code]
- [Pattern 2]

**Potential Integration Points**:
- [Where this feature fits in]
- [What it might affect]

**Technical Considerations**:
- [Library/framework consideration]
- [Performance consideration]
- [Compatibility consideration]
```

### Step 4: Draft Requirements

Transform the idea into structured requirements:

```markdown
## 📋 Draft Requirements

### Feature Overview
**What**: [Clear 1-2 sentence description]

**Why**: [Problem being solved]

**Who**: [Target users]

### Functional Requirements
1. [Requirement 1 - specific and actionable]
2. [Requirement 2 - specific and actionable]
3. [Requirement 3 - specific and actionable]

### Non-Functional Requirements
- **Performance**: [Performance expectation]
- **Usability**: [Usability expectation]
- **Compatibility**: [Compatibility needs]

### Acceptance Criteria
- [ ] [Testable criterion 1]
- [ ] [Testable criterion 2]
- [ ] [Testable criterion 3]

### Out of Scope
- [What we're NOT building]
- [Future enhancements for later]
```

**Show to user**:
```markdown
---

## 📝 Requirements Draft

[Show the draft requirements]

**Does this capture your idea correctly?**

Options:
1. ✅ Yes, looks good → I'll create the work folder
2. 🔄 Needs adjustments → Tell me what to change
3. 🤔 Still unclear → Let's discuss more
```

**Wait for user approval** before proceeding.

### Step 5: Assess Complexity & Create Work Folder

**Assess complexity**:
- **Simple** (< 2 hours): Single component, clear pattern
- **Medium** (2-8 hours): Multiple files, some new patterns
- **Complex** (8+ hours): New architecture, extensive changes

**Create work folder**:

Create `.makeflow/work/[feature-slug]/` with the following files:

#### 1. AGENTS.md
Use template from `.makeflow/templates/agents-template.md` and populate with:
- Overview from requirements
- All clarified requirements
- Acceptance criteria
- Technical approach from research
- Complexity assessment
- Next recommended workflow

#### 2. spec.md (for Medium/Complex features)
```markdown
# [Feature Name] Specification

## Problem Statement
[Detailed problem description]

## Proposed Solution
[Detailed solution description]

## User Experience
[How users will interact with this]

## Technical Design
[Architecture and implementation details]

## Testing Strategy
[How to test this]

## Rollout Plan
[How to deploy and release]
```

#### 3. questions.md (if any open questions remain)
```markdown
# Open Questions

## Resolved
- [Question] → [Answer] ([Date])

## Unresolved
- [Question that needs stakeholder input]
```

### Step 6: Present to User

```markdown
---

## ✅ Work Folder Created

**Feature**: `[feature-slug]`  
**Location**: `.makeflow/work/[feature-slug]/`  
**Entry Point**: `.makeflow/work/[feature-slug]/AGENTS.md`

**Complexity**: [Simple/Medium/Complex]  
**Estimated Time**: [X hours]  
**Files Likely Affected**: ~[N files]

---

## 📊 What We Clarified

**From Your Idea**:
> [Original idea in user's words]

**To Clear Requirements**:
- ✅ Defined scope and MVP
- ✅ Identified target users
- ✅ Established success criteria
- ✅ Found similar patterns to follow
- ✅ Assessed technical feasibility

**Open Questions** (if any):
- [Question requiring stakeholder input]

---

## 🚀 Recommended Next Steps

**For Simple Features**:
```
@ai Use .makeflow/workflows/02-planning/create-plan.md
Feature: [feature-slug]
```

**For Medium/Complex Features**:
```
@ai Use .makeflow/workflows/02-planning/create-spec.md
Feature: [feature-slug]
```

**If you want to create a ticket first**:
```
@ai Use .makeflow/workflows/02-planning/create-ticket.md
Feature: [feature-slug]
```

---

Which path would you like to take?
```

---

## Example Usage

### Example: Vague Idea to Clear Requirements

**User**:
```markdown
@codegen Use .makeflow/workflows/01-intake/from-idea.md

Feature Idea: Make filtering better
```

**AI Response**:
```markdown
## 🤔 Clarifying Questions

I'd love to help improve filtering! To create a clear specification, I need to understand:

**Scope & Size**:
1. Which filtering are you referring to? (Resources, users, assignments, or all tables?)
2. What specific problems exist with current filtering?
3. What would "better" look like? (Faster? More options? Easier to use?)

**Users & Usage**:
4. Who uses filtering most often? (Admins, end users, both?)
5. How often do they need to apply multiple filters?
6. What combinations of filters are most common?

**Implementation**:
7. I found filtering in resources table (app/routes/dashboard.resources.tsx). Should we follow that pattern or change it?
8. Any performance concerns with large datasets?

**Success Criteria**:
9. How will we know the new filtering is "better"? (User feedback? Speed benchmarks? Feature adoption?)

Please answer what you can, and I'll create a clear specification!
```

**User Responds**:
```markdown
1. Resources table specifically
2. Users can't filter by multiple criteria at once (e.g., Type=Equipment AND Status=Active)
3. Need multi-select dropdowns for each column
4. Mostly admins, generating reports
5. Very often - almost every session
6. Type+Status is most common, Type+Location second most
7. Follow existing pattern but extend it
8. Yes - we have 1000+ resources
9. Users should be able to apply 2-3 filters quickly (< 3 clicks)
```

**AI Continues**:
```markdown
## 📚 Codebase Research

**Similar Features Found**:
- `app/routes/dashboard.resources.tsx` - Current single-filter implementation
- `app/components/ui/multi-select.tsx` - Multi-select component we can use

**Patterns to Follow**:
- Table filtering follows React Table v8 patterns
- Filter state managed in URL params (good for shareability)

**Technical Considerations**:
- Database queries use Prisma with compound WHERE clauses
- Need to test with 1000+ records for performance

---

## 📋 Draft Requirements

### Feature Overview
**What**: Add multi-criteria filtering to resources table with multi-select dropdowns

**Why**: Admins need to filter by multiple criteria simultaneously (Type + Status + Location) to generate reports efficiently

**Who**: Administrators generating resource reports

### Functional Requirements
1. Each filterable column (Type, Status, Location) has a multi-select dropdown
2. Multiple filters can be active simultaneously with AND logic
3. Filters persist in URL params for sharing filtered views
4. "Clear all filters" button resets to unfiltered state
5. Filtered count shows "Showing X of Y resources"

### Non-Functional Requirements
- **Performance**: Filter application < 500ms with 1000+ resources
- **Usability**: Maximum 3 clicks to apply 2-3 filters
- **Compatibility**: Works with existing table sorting and pagination

### Acceptance Criteria
- [ ] Can select multiple types (e.g., Equipment, Tools)
- [ ] Can select multiple statuses (e.g., Active, Maintenance)
- [ ] Can combine Type + Status + Location filters
- [ ] Filtered results update immediately
- [ ] URL params reflect active filters
- [ ] Clear filters button works
- [ ] Performance tested with 1000+ resources

### Out of Scope
- Custom filter logic (e.g., OR conditions)
- Saved filter presets (future enhancement)
- Advanced search/text filtering (different feature)

---

**Does this capture your idea correctly?**

Options:
1. ✅ Yes, looks good → I'll create the work folder
2. 🔄 Needs adjustments → Tell me what to change
3. 🤔 Still unclear → Let's discuss more
```

**User**:
```markdown
Yes, perfect!
```

**AI Creates Work Folder**:
```markdown
## ✅ Work Folder Created

**Feature**: `resource-multi-filter`  
**Location**: `.makeflow/work/resource-multi-filter/`  
**Entry Point**: `.makeflow/work/resource-multi-filter/AGENTS.md`

**Complexity**: Medium  
**Estimated Time**: 4-6 hours  
**Files Likely Affected**: ~4 files

---

## 📊 What We Clarified

**From Your Idea**:
> Make filtering better

**To Clear Requirements**:
- ✅ Scope: Resources table multi-criteria filtering
- ✅ Users: Administrators generating reports
- ✅ Success: 2-3 filters in < 3 clicks, < 500ms performance
- ✅ Pattern: Extend existing filtering, use multi-select components
- ✅ Technical: Prisma compound WHERE, URL param state

---

## 🚀 Recommended Next Steps

Since this is a **medium** complexity feature:

```
@codegen Use .makeflow/workflows/02-planning/create-plan.md
Feature: resource-multi-filter
```

This will break the work into phases and tasks.

Ready to proceed?
```

---

## Tips for AI Agents

### Getting Good Answers from Users
- Ask specific, targeted questions
- Give examples or options when possible
- Acknowledge what you understand so far
- Break complex questions into smaller ones
- Don't ask everything at once (max 8 questions per round)

### Judging Complexity
**Simple** indicators:
- "Like X but for Y"
- Following exact existing pattern
- Single file change
- Clear implementation path

**Complex** indicators:
- "Something like..." (vague)
- No existing pattern
- Multiple systems involved
- Novel user experience

### Creating Good Feature Slugs
- Descriptive: `resource-multi-filter` not `filtering-improvements`
- Specific: `user-bulk-export` not `export-feature`
- Action-oriented: `add-dark-mode` not `dark-mode-feature`

---

## Validation Checklist

Before completing this workflow:

- [ ] Initial idea captured in user's words
- [ ] Clarifying questions asked and answered
- [ ] Codebase research performed
- [ ] Requirements drafted and approved by user
- [ ] Work folder created with AGENTS.md
- [ ] Complexity assessed
- [ ] Next workflow recommended
- [ ] User has clear path forward

---

## Integration with Other Workflows

**Typical Next Workflows**:

**Simple → Direct to Planning**:
```
.makeflow/workflows/02-planning/create-plan.md
```

**Medium/Complex → Full Specification**:
```
.makeflow/workflows/02-planning/create-spec.md
```

**Create Ticket First** (for tracking):
```
.makeflow/workflows/02-planning/create-ticket.md
```

---

**End of Workflow**

