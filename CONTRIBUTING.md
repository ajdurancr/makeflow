# Contributing to makeflow

Thank you for your interest in contributing to makeflow! 🎉

---

## 🔄 Using Makeflow Workflows (Eat Our Own Dog Food!)

**makeflow contributions should use makeflow workflows** - we practice what we preach!

### For Non-Trivial Changes

Use the workflow system for any change that's more than a simple typo or formatting fix:

```markdown
# 1. Create a work folder
mkdir .makeflow/work/NNN-your-feature-name

# 2. Create AGENTS.md to track your work
# (See .makeflow/templates/agents-template.md)

# 3. Follow the appropriate workflow
# For new workflow: Use .makeflow/workflows/01-intake/from-idea.md
# For bug fix: Use .makeflow/workflows/01-intake/from-bug.md
# For improvement: Use .makeflow/workflows/02-planning/create-plan.md
```

**Why?**
- ✅ **Validates the system** - Using makeflow improves makeflow
- ✅ **Creates examples** - Your work becomes a reference for others
- ✅ **Improves quality** - Structured process catches issues early
- ✅ **Builds confidence** - You'll understand the system better

**Example**: See `.makeflow/history/2025-12-09-001-dogfooding-implementation/` for the first work folder that established this practice!

### For Trivial Changes

**Skip workflows for**:
- Typo fixes
- Formatting/whitespace
- Broken links
- Simple documentation corrections

**Just**:
1. Make the change
2. Commit with clear message
3. Create PR

### Quick Reference

**Adding a new workflow**:
```markdown
@ai Use .makeflow/workflows/01-intake/from-idea.md

Feature Idea: Add workflow for [use case]
Context: [Why it's needed]
```

**Fixing a bug in existing workflow**:
```markdown
@ai Use .makeflow/workflows/01-intake/from-bug.md

Bug: [workflow-name] has [issue]
Impact: [Who's affected]
```

**Improving documentation**:
```markdown
@ai Use .makeflow/workflows/02-planning/create-plan.md

Improvement: Update [doc] with [enhancement]
```

---

## Ways to Contribute

### 1. Report Bugs or Issues
Found something that doesn't work? Let us know!

**Create an issue** with:
- Clear description of the problem
- Steps to reproduce
- Expected vs actual behavior
- Your environment (AI tool used, project type, etc.)

### 2. Suggest Workflow Improvements
Have ideas for better workflows?

**Open a discussion** or issue with:
- Which workflow you want to improve
- What problem it would solve
- Your proposed solution
- Example usage

### 3. Share Usage Examples
Using makeflow in interesting ways?

**Share your experience**:
- Open a discussion
- Show how you adapted makeflow for your team
- Share lessons learned
- Include before/after metrics if available

### 4. Submit Workflow Customizations
Created custom workflows for your team?

**Consider sharing** as a pull request:
- Add to `.makeflow/workflows/community/`
- Include documentation
- Explain the use case

### 5. Improve Documentation
Documentation can always be better!

**Help by**:
- Fixing typos or unclear sections
- Adding more examples
- Translating to other languages
- Creating video tutorials

---

## How to Contribute Code

### Setup

```bash
# 1. Fork the repository on GitHub

# 2. Clone your fork
git clone https://github.com/YOUR-USERNAME/makeflow.git
cd makeflow

# 3. Create a branch
git checkout -b feature/your-feature-name

# 4. Make your changes

# 5. Commit with clear messages
git add .
git commit -m "feat: Add community workflow for X"

# 6. Push to your fork
git push origin feature/your-feature-name

# 7. Create a Pull Request on GitHub
```

### Commit Message Format

Use conventional commits:

```
feat: Add new workflow for X
fix: Correct typo in workflow Y
docs: Update GUIDE.md with example Z
refactor: Simplify workflow instructions
```

Types:
- `feat`: New feature or workflow
- `fix`: Bug fix
- `docs`: Documentation changes
- `refactor`: Code/workflow improvements
- `test`: Test additions or changes
- `chore`: Maintenance tasks

---

## Guidelines

### For Workflow Contributions

**Keep workflows**:
- ✅ Clear and actionable
- ✅ AI-agnostic (work with any tool)
- ✅ Well-documented with examples
- ✅ Focused on a specific use case

**Avoid**:
- ❌ Tool-specific commands
- ❌ Overly complex instructions
- ❌ Vague or ambiguous steps

### For Documentation Contributions

**Make documentation**:
- ✅ Easy to scan (use headers, lists)
- ✅ Example-rich (show, don't just tell)
- ✅ Beginner-friendly (explain jargon)
- ✅ Accurate (test examples)

---

## Pull Request Process

1. **Create PR** with clear description
2. **Reference issues** if applicable
3. **Wait for review** (we'll respond within a few days)
4. **Address feedback** if requested
5. **Merge** once approved!

---

## Community Guidelines

**Be respectful**: Treat everyone with kindness and respect

**Be constructive**: Offer solutions, not just criticism

**Be patient**: Maintainers volunteer their time

**Be collaborative**: We're building this together!

---

## Questions?

- **General questions**: Open a discussion
- **Bug reports**: Create an issue
- **Feature ideas**: Start a discussion or create an issue

---

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

**Thank you for helping make makeflow better!** 🚀
