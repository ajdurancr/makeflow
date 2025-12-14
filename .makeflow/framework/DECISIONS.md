# Design Decisions & FAQ

Why makeflow is designed the way it is.

---

## Table of Contents

1. [Design Decisions](#design-decisions)
2. [FAQ](#faq)
3. [Philosophy](#philosophy)

---

## Design Decisions

### Decision 1: Work Folders Are Committed

**Decision**: Work folders (`.makeflow/work/`) are committed to the repository

**Rationale**:
- Cloud AI tools (Codegen, Claude, etc.) need to read work folder to understand current state
- AGENTS.md provides essential context for AI continuation
- Team members can see active work
- Enables collaboration on features

**Alternative Considered**:
- Gitignore work folders (keep them local only)
- **Why not**: Cloud AI tools couldn't access context

**Impact**:
- Repository contains more "work-in-progress" data
- But this is cleaned up when work moves to history

---

### Decision 2: No Dates in Work Folder Names

**Decision**: Work folders use feature names only (`resource-export`, not `2025-12-09-resource-export`)

**Rationale**:
- Dated folders get stale and confusing ("this is 2 weeks old and still unfinished?")
- Feature names remain relevant throughout development
- Encourages one feature per branch (best practice)
- Dates are added in history folder when work is complete

**Alternative Considered**:
- Include dates in work folder names
- **Why not**: Creates confusion with long-running features

**Impact**:
- Work folder names stay relevant
- Naturally enforces one-feature-per-branch workflow

---

### Decision 3: Tests by Default (Opt-Out, Not Opt-In)

**Decision**: All execution workflows include test coverage by default; `-without-tests` variants available for rare exceptions

**Rationale**:
- Tests should be the default expectation (quality-first mindset)
- Junior developers learn that testing is normal
- Opt-out requires conscious decision

**Alternative Considered**:
- Opt-in testing (tests only if explicitly requested)
- **Why not**: Leads to insufficient test coverage

**Impact**:
- Encourages consistent test coverage across codebase
- Technical debt is exception, not the rule

---

### Decision 4: Specification-Driven for All Changes

**Decision**: Every change (even small ones) starts with some form of specification

**Rationale**:
- Prevents wasted effort building the wrong thing
- Creates permanent record of intent
- Easier code review and understanding
- AI tools work better with clear requirements

**Varies by Complexity**:
- **Simple**: Quick AGENTS.md entry
- **Medium**: Full task plan
- **Complex**: Detailed specification document

**Alternative Considered**:
- Allow ad-hoc changes without specification
- **Why not**: Leads to unclear requirements and wasted work

**Impact**:
- Slight upfront time investment
- Significant time saved avoiding rework

---

### Decision 5: AI-Agnostic via Pure Markdown

**Decision**: All workflows written in plain markdown, work with any AI tool

**Rationale**:
- No vendor lock-in
- Tool preferences can change without system obsolescence
- Copy-paste friendly across all AI platforms
- Future-proof as new AI tools emerge

**Alternative Considered**:
- Custom commands for each platform (Codegen commands, Cursor commands, etc.)
- **Why not**: Adds complexity; doesn't work across tools

**Impact**:
- Universal compatibility
- Simple to understand and use
- Works with future AI tools

---

### Decision 6: Work/History Separation with Cleanup

**Decision**: Active work in temporary work folder; summarized to history; work folder deleted after completion

**Rationale**:
- **During development**: Need detailed tracking (work folder)
- **After completion**: Only need summary (history folder)
- **Keeps repository clean**: Work folders don't accumulate
- **Permanent record maintained**: History folder prevents information loss

**Alternative Considered**:
- Keep all work folders forever
- **Why not**: Repository becomes cluttered with old work

**Impact**:
- Clean, organized repository
- Complete historical record
- Easy to find current vs completed work

---

### Decision 7: Bidirectional Ticket Creation

**Decision**: Support both directions - ticket → work AND work → ticket creation

**Rationale**:
- **Ticket → Work**: Most common workflow (existing ticket)
- **Work → Ticket**: Sometimes you define a spec first, then need a ticket for tracking

**Alternative Considered**:
- One direction only (ticket → work)
- **Why not**: Doesn't handle all real-world scenarios

**Impact**:
- Flexibility for different team workflows
- Supports both top-down and bottom-up processes

---

### Decision 8: Four-Stage Workflow (Not Linear)

**Decision**: Organize workflows into 4 clear stages (Intake → Planning → Execution → Delivery)

**Rationale**:
- Mirrors how humans naturally develop software
- Each stage has clear entry/exit criteria
- Stages can be sized appropriately (skip planning for simple changes)
- Progressive complexity

**Alternative Considered**:
- Linear workflow (one path for all changes)
- **Why not**: Different complexity levels need different processes

**Impact**:
- Flexible workflow that scales with complexity
- Clear mental model for developers
- Easy to know "where you are" in the process

---

### Decision 9: AGENTS.md as Single Entry Point

**Decision**: Every work folder has AGENTS.md as the primary file AI agents read

**Rationale**:
- Single source of truth for feature context
- AI agents know exactly what to read
- Consistent structure across all features
- Always up-to-date with current state

**Alternative Considered**:
- Multiple files without clear entry point
- **Why not**: AI agents wouldn't know what to read first

**Impact**:
- Easy for AI to understand feature state
- Consistent experience across features
- Clear structure for humans too

---

### Decision 10: Zero Dependencies (Pure Markdown)

**Decision**: System requires no installation, no dependencies, no CLI tools

**Rationale**:
- Copy `.makeflow/` folder to any project and it works
- No setup friction
- No version conflicts
- No maintenance burden
- Universal compatibility

**Alternative Considered**:
- npm package with CLI tools
- **Why not**: Adds setup friction, dependencies, maintenance

**Impact**:
- Maximum portability
- Immediate usability
- Zero maintenance overhead

---

## FAQ

### General Questions

**Q: Do I need to use all 12 workflows?**  
A: No! Use what you need:
- Simple fix: `from-bug.md` → `execute-quick.md` → `complete.md`
- Medium feature: `from-ticket.md` → `create-plan.md` → `execute-task.md` × N → `create-pr.md` → `complete.md`
- Complex feature: Use all stages

**Q: Can I customize workflows for my team?**  
A: Absolutely! Edit the workflows to match your team's needs. makeflow is a starting point.

**Q: Do I have to delete work folders after completion?**  
A: **YES - it's mandatory!** The `complete.md` workflow includes explicit deletion requirements with a checklist. Work folders are committed during development for AI access, but MUST be deleted after summarizing to history. This keeps the repository clean and enforces the work/history separation design.

**Q: What if I'm not using AI tools?**  
A: Workflows still work as documentation! Follow the steps manually. The structure helps even without AI.

**Q: How do I handle multiple people working on same feature?**  
A: Two approaches:
1. One person "owns" the work folder, others reference it
2. Use branches per developer, merge work folder updates carefully

---

### Technical Questions

**Q: Why are work folders committed if they're temporary?**  
A: Cloud AI tools need to read them to understand context. They're temporary but need to be accessible during development.

**Q: What if work folder names conflict?**  
A: Add a unique suffix:
```bash
resource-export-v2
resource-export-2025-attempt
resource-export-simplified
```

**Q: Can I have multiple work folders?**  
A: Yes! One per feature/branch:
```
.makeflow/work/
├── feature-export/
├── bug-login-fix/
└── refactor-api/
```

**Q: How do I handle work that spans weeks/months?**  
A: Keep the work folder! Update AGENTS.md regularly. Break into smaller pieces if possible. The work folder stays until feature is merged and summarized.

**Q: What if I forget to summarize before deleting work folder?**  
A: Check git history:
```bash
git log -- .makeflow/work/feature-name/
git show <commit>:.makeflow/work/feature-name/AGENTS.md
```

---

### Workflow Questions

**Q: When should I use `execute-quick.md` vs `execute-task.md`?**  
A:
- `execute-quick.md`: < 1 hour, following exact pattern, no ambiguity
- `execute-task.md`: Defined task from plan, needs tests, more complex

**Q: Can I skip planning for all features?**  
A: Not recommended. Planning prevents rework. Exception: Very simple changes (< 1 hour).

**Q: When do I need a full specification?**  
A: Complex features (8+ hours), novel solutions, multiple stakeholders, unclear requirements.

**Q: How do I handle bugs discovered during development?**  
A: Two options:
1. Fix immediately if small (document in AGENTS.md)
2. Create separate work folder if significant (use `from-bug.md`)

**Q: What if requirements change mid-development?**  
A: Update AGENTS.md, add decision log entry explaining the change, adjust plan if needed.

---

### Tool-Specific Questions

**Q: Does makeflow only work with Codegen?**  
A: No! Works with Codegen, Cursor, Claude, ChatGPT, Copilot, any AI tool. See [MULTI-TOOL.md](MULTI-TOOL.md).

**Q: Can I use makeflow without AI?**  
A: Yes! Follow workflows manually. They provide structure even without AI assistance.

**Q: Which AI tool is best for makeflow?**  
A: Depends on your needs:
- **Codegen**: Full workflows, async work
- **Cursor**: Interactive development
- **Claude**: Design and planning
- See [MULTI-TOOL.md](MULTI-TOOL.md) for detailed comparison

**Q: Can I switch AI tools mid-feature?**  
A: Yes! AGENTS.md provides context for any tool. Example: Plan with Claude, implement with Cursor.

---

### Process Questions

**Q: How do I onboard my team to makeflow?**  
A:
1. Copy `.makeflow/` to your repo
2. Do one feature together as a team
3. Share this guide
4. Let people adapt workflows to their style

**Q: What if team members don't want to use it?**  
A: makeflow is optional tooling. Some can use it, others don't have to. Work folders being committed means everyone can see the tracking even if they don't use workflows.

**Q: How do I measure if makeflow is helping?**  
A: Track:
- Time from idea to shipped code
- Rework due to unclear requirements
- Code review time
- Onboarding time for new developers
- Test coverage

**Q: Can I use makeflow for non-code work?**  
A: Yes! Works for documentation, design, research, any work that needs tracking.

---

### History Questions

**Q: How long should I keep history?**  
A: Forever! It's a permanent record. Archive old history if it gets large:
```bash
mkdir .makeflow/history/archive/2024
mv .makeflow/history/2024-* .makeflow/history/archive/2024/
```

**Q: What if history INDEX gets too long?**  
A: Break by year:
```
.makeflow/history/
├── INDEX.md (current year)
├── INDEX-2024.md
├── INDEX-2023.md
```

**Q: Can I search history?**  
A: Yes!
```bash
# Search all summaries
grep -r "search term" .makeflow/history/

# Search INDEX
grep "feature name" .makeflow/history/INDEX.md
```

---

## Philosophy

### Why Specification-Driven?

**Problem**: #1 source of wasted developer time is building the wrong thing.

**Solution**: Spend time upfront clarifying requirements:
- Reduces ambiguity
- Prevents rework  
- Creates permanent record
- Enables better AI assistance
- Facilitates code review

### Why Four Stages?

**Natural developer workflow**:
1. **Intake**: "What am I building?"
2. **Planning**: "How will I build it?"
3. **Execution**: "Building it"
4. **Delivery**: "Shipping it"

Each stage has clear purpose and deliverable.

### Why Work/History Split?

**Development is messy**: Work folder captures the real, iterative process

**History is clean**: Only final results matter for long-term record

This split enables both without cluttering the repository.

### Why AI-Agnostic?

**Tools change**: Today's preferred AI might not be tomorrow's

**Teams vary**: Different developers prefer different tools

**Future-proof**: Works with AI tools that don't exist yet

**Simple**: Markdown works everywhere

### Why Zero Dependencies?

**Maximum portability**: Copy to any project, works immediately

**No maintenance**: No packages to update, no breaking changes

**Universal**: Works regardless of project tech stack

**Simple**: Easier to understand and customize

---

## Contributing to These Decisions

Have feedback on these design decisions? 

**Found a better approach?** Open an issue or PR!

**Disagree with a decision?** Start a discussion!

**Want to share your experience?** We'd love to hear it!

makeflow is designed to evolve based on real-world usage. Your input shapes its future.

---

**Next**: See [EXAMPLES.md](EXAMPLES.md) for real-world usage examples.
