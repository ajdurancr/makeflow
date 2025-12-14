# Workflow: Create Specification

**Stage**: 02 - Planning  
**Purpose**: Write a detailed technical specification  
**Time**: 30-60 minutes  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ Complex feature (8+ hours of work)
- ✅ Novel solution or architecture needed
- ✅ Multiple stakeholders involved
- ✅ Need to align team before building

---

## Prerequisites

- [ ] Work folder exists (`.makeflow/work/[feature-name]/`)
- [ ] Requirements are clarified
- [ ] Basic feasibility confirmed

---

## Instructions for AI Agent

### Step 1: Gather Context

**First**, read `.makeflow/work/[feature-name]/AGENTS.md` to understand:
- Requirements
- Acceptance criteria
- Technical constraints
- Any decisions already made

**Then**, check if `.makeflow/project/index.md` exists:
- **If it exists**: Review it to find relevant technical documentation for this feature
- **Purpose**: Understand architectural patterns, existing components to reuse, API design standards, and technical constraints
- **What to look for**: Architecture docs, API references, similar features, design patterns used in the project

### Step 2: Define Technical Approach

Create `.makeflow/work/[feature-name]/spec.md`:

```markdown
# [Feature Name] - Technical Specification

**Author**: AI + [User Name]  
**Date**: [YYYY-MM-DD]  
**Status**: Draft

---

## 1. Problem Statement

### Current Situation
[Describe what exists today]

### Problems with Current Approach
- [Problem 1]
- [Problem 2]

### Impact
[Who is affected and how]

---

## 2. Proposed Solution

### High-Level Approach
[2-3 paragraphs explaining the solution]

### Why This Approach
- [Reason 1]
- [Reason 2]

### Alternatives Considered
1. **[Alternative 1]**: [Why not chosen]
2. **[Alternative 2]**: [Why not chosen]

---

## 3. Technical Design

### Architecture Overview
```
[ASCII diagram showing components and their relationships]
```

### Components

#### Component 1: [Name]
**Purpose**: [What it does]  
**Location**: `path/to/component`  
**Responsibilities**:
- [Responsibility 1]
- [Responsibility 2]

**Interface**:
```typescript
[Key functions/types]
```

#### Component 2: [Name]
[Same structure]

### Data Model

**New/Modified Tables**:
```sql
-- Or TypeScript types, depending on project
```

**Relationships**:
- [How data relates]

### API Changes

**New Endpoints**:
- `POST /api/endpoint` - [Purpose]
- `GET /api/endpoint/:id` - [Purpose]

**Modified Endpoints**:
- `PUT /api/existing` - [What changes]

---

## 4. User Experience

### User Flows

#### Flow 1: [Primary Use Case]
1. User does [action]
2. System [response]
3. User sees [result]

#### Flow 2: [Secondary Use Case]
[Same structure]

### UI Changes

**New Screens/Components**:
- [Component name] - [Purpose]

**Modified Screens**:
- [Screen name] - [What changes]

### Wireframes/Mockups
[Links to designs or ASCII mockups]

---

## 5. Testing Strategy

### Unit Tests
**Coverage Areas**:
- [What to unit test]
- [Edge cases]

### Integration Tests
**Scenarios**:
- [Integration test 1]
- [Integration test 2]

### E2E Tests
**Critical Paths**:
- [E2E flow 1]
- [E2E flow 2]

### Performance Tests
**Benchmarks**:
- [Performance requirement 1]
- [Performance requirement 2]

---

## 6. Implementation Plan

### Phase 1: [Foundation]
**Goal**: [What this phase achieves]  
**Tasks**:
- [ ] Task 1.1
- [ ] Task 1.2

**Estimated**: [X hours]

### Phase 2: [Core Features]
**Goal**: [What this phase achieves]  
**Tasks**:
- [ ] Task 2.1
- [ ] Task 2.2

**Estimated**: [X hours]

### Phase 3: [Polish & Tests]
**Goal**: [What this phase achieves]  
**Tasks**:
- [ ] Task 3.1
- [ ] Task 3.2

**Estimated**: [X hours]

---

## 7. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| [Risk 1] | High | High | [How to mitigate] |
| [Risk 2] | Medium | Low | [How to mitigate] |

---

## 8. Dependencies

**External Dependencies**:
- [Library/service 1] - [Why needed]
- [Library/service 2] - [Why needed]

**Internal Dependencies**:
- [Feature/module 1] - [Relationship]
- [Feature/module 2] - [Relationship]

**Blocked By**:
- [What needs to happen first]

---

## 9. Rollout Plan

### Deployment Strategy
[How to deploy - feature flags, gradual rollout, etc.]

### Rollback Plan
[How to rollback if issues occur]

### Monitoring
**Metrics to Watch**:
- [Metric 1]
- [Metric 2]

**Alerts**:
- [What triggers an alert]

---

## 10. Success Criteria

**Launch Criteria**:
- [ ] All acceptance criteria met
- [ ] Tests passing (coverage > X%)
- [ ] Performance benchmarks met
- [ ] Documentation updated
- [ ] Stakeholder approval

**Post-Launch Metrics**:
- [Metric 1]: Target [value]
- [Metric 2]: Target [value]

---

## 11. Open Questions

- [ ] [Question 1] - Owner: [Name]
- [ ] [Question 2] - Owner: [Name]

---

## 12. Appendix

### References
- [Link to related docs]
- [Link to design]
- [Link to research]

### Glossary
- **Term 1**: [Definition]
- **Term 2**: [Definition]
```

### Step 3: Review with User

Present the spec:

```markdown
---

## 📋 Specification Draft Created

**Location**: `.makeflow/work/[feature-name]/spec.md`

### Key Decisions:
1. **Architecture**: [High-level approach]
2. **Technology**: [Key technologies chosen]
3. **Scope**: [Phases and timeline]

### 📊 Complexity Assessment:
- **Total Effort**: [X hours]
- **Phases**: [N phases]
- **Risk Level**: [Low/Medium/High]

### Open Questions:
- [Question requiring stakeholder input]

---

**Review the specification and let me know**:
1. ✅ Approved → Move to task breakdown
2. 🔄 Needs changes → Tell me what to adjust
3. 🤔 Questions → Let's discuss concerns
```

### Step 4: Update AGENTS.md

Update `.makeflow/work/[feature-name]/AGENTS.md`:
- Change status to "📐 Spec Complete"
- Add link to spec.md
- Add decision log entry
- Update next steps

### Step 5: Recommend Next Workflow

```markdown
---

## ✅ Specification Complete

**Next Step**: Break specification into executable tasks

```
@ai Use .makeflow/workflows/02-planning/create-plan.md
Feature: [feature-name]
```

This will create a phase-by-phase task breakdown.
```

---

## Tips for Writing Good Specs

### ✅ DO:
- Be specific and concrete
- Include diagrams/examples
- Consider edge cases
- Document alternatives
- Define success metrics
- Plan for testing

### ❌ DON'T:
- Be vague or ambiguous
- Skip the "why"
- Ignore risks
- Forget about rollback
- Omit performance considerations
- Write without stakeholder input

---

## Example Spec Outline

For a "Resource Bulk Assignment" feature:

**1. Problem**: Assigning 50+ resources one-by-one is tedious  
**2. Solution**: Select multiple resources, assign all in one action  
**3. Design**:
   - Add checkboxes to resource table
   - Bulk action toolbar when > 0 selected
   - Modified assignment dialog for bulk mode
   - Database transaction for atomicity
**4. Testing**: Unit tests for state, integration for transaction, E2E for flow  
**5. Plan**: Phase 1 (UI), Phase 2 (Backend), Phase 3 (Tests)  
**6. Risks**: Large bulk operations might timeout  
**7. Success**: Admins can assign 50+ resources in < 30 seconds  

---

## Validation Checklist

- [ ] Problem statement clear
- [ ] Solution approach defined
- [ ] Technical design detailed
- [ ] User experience described
- [ ] Testing strategy outlined
- [ ] Implementation phases planned
- [ ] Risks identified with mitigations
- [ ] Success criteria defined
- [ ] Open questions documented
- [ ] Spec reviewed with user

---

**End of Workflow**
