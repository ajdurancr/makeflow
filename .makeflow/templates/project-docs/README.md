# Project Documentation Templates

This directory contains templates for bootstrapping documentation in projects using makeflow.

## 📋 Templates Available

### Entry Point Template
- **`index.md.template`** - Template for `.makeflow/project/index.md` (documentation index for AI agents)

### Documentation Structure Templates
- **`docs/README.md.template`** - Main documentation hub
- **`docs/patterns/pattern-template.md`** - Development pattern documentation
- **`docs/specs/spec-template.md`** - Feature specification template
- **`docs/workflows/documentation/guidelines.md.template`** - Documentation guidelines
- **`docs/workflows/documentation/templates.md.template`** - Template reference guide
- **`docs/decisions/adr-template.md`** - Architecture Decision Record template
- **`docs/faq.md.template`** - FAQ template

## 🎯 Template Variables

All templates use standardized placeholder variables:

```
{{PROJECT_NAME}}          # e.g., "MyApp", "API Service"
{{PROJECT_DESCRIPTION}}   # Brief tagline (1-2 sentences)
{{REPO_URL}}              # GitHub repository URL
{{REPO_OWNER}}            # GitHub username or organization
{{REPO_NAME}}             # Repository name
{{TECH_STACK_SUMMARY}}    # Brief tech stack description
{{PRIMARY_LANGUAGE}}      # Main programming language
{{FRAMEWORK}}             # Main framework (if applicable)
{{CURRENT_DATE}}          # YYYY-MM-DD format
```

## 🚀 How to Use Templates

### Automatic (Recommended)

Use the makeflow workflows to automatically set up documentation:

**For existing documentation**:
```markdown
@ai Use .makeflow/workflows/00-setup/hook-docs.md
```

**For new documentation**:
```markdown
@ai Use .makeflow/workflows/00-setup/bootstrap-docs.md
```

These workflows will:
1. Prompt for necessary information
2. Replace template variables automatically
3. Create appropriate documentation structure
4. Set up makeflow integration

### Manual

If you prefer to manually use templates:

1. **Copy template files** to your project
2. **Replace all `{{VARIABLE}}` placeholders** with actual values
3. **Remove `.template` extension** from filenames
4. **Customize content** to fit your project

**Example**:
```bash
# Copy index template
cp .makeflow/templates/project-docs/index.md.template .makeflow/project/index.md

# Replace variables
sed -i 's/{{PROJECT_NAME}}/MyApp/g' .makeflow/project/index.md
sed -i 's/{{CURRENT_DATE}}/2025-12-14/g' .makeflow/project/index.md

# Customize content as needed
vim .makeflow/project/index.md
```

## 📚 Template Structure

### `index.md.template`
**Purpose**: Entry point for AI agents to understand documentation structure  
**Location**: Copy to `.makeflow/project/index.md`  
**Key Sections**:
- Main documentation hub location
- Documentation structure map
- AI agent quick reference
- Maintenance notes

### `docs/README.md.template`
**Purpose**: Main documentation hub for the project  
**Location**: Copy to `docs/README.md`  
**Key Sections**:
- Project overview and mission
- Quick links and navigation
- Core concepts
- Technology stack
- Documentation sections index

### `docs/patterns/pattern-template.md`
**Purpose**: Template for documenting development patterns  
**Location**: Copy to `docs/patterns/[pattern-name].md`  
**Key Sections**:
- Problem and context
- Solution and implementation
- Benefits and trade-offs
- Examples and usage

### `docs/specs/spec-template.md`
**Purpose**: Template for feature specifications  
**Location**: Copy to `docs/specs/[feature-name].md`  
**Key Sections**:
- Overview and goals
- Requirements (functional and non-functional)
- Architecture and components
- Implementation notes
- Testing strategy

### `docs/workflows/documentation/guidelines.md.template`
**Purpose**: Guidelines for adding documentation  
**Location**: Copy to `docs/workflows/documentation/guidelines.md`  
**Key Sections**:
- When and where to add documentation
- Documentation structure guidelines
- Best practices

### `docs/workflows/documentation/templates.md.template`
**Purpose**: Reference for available templates  
**Location**: Copy to `docs/workflows/documentation/templates.md`  
**Key Sections**:
- Available template list
- Usage tips
- Customization guidelines

### `docs/decisions/adr-template.md`
**Purpose**: Architecture Decision Record template  
**Location**: Copy to `docs/decisions/NNNN-[title].md`  
**Key Sections**:
- Status and context
- Decision details
- Consequences and alternatives
- Implementation notes

### `docs/faq.md.template`
**Purpose**: Frequently Asked Questions template  
**Location**: Copy to `docs/faq.md`  
**Key Sections**:
- Common questions organized by topic
- Clear, actionable answers
- Links to related documentation

## 🎨 Customization Tips

### Adding Sections
Templates are guidelines, not requirements:
- **Add sections** that make sense for your project
- **Remove sections** that don't apply
- **Adapt structure** to fit your needs

### Keeping Consistency
When customizing:
- Maintain similar structure across similar document types
- Use consistent formatting and style
- Link liberally to related documentation
- Keep "Last Updated" dates current

### Progressive Documentation
Start simple and grow organically:
- Begin with just README and guidelines
- Add patterns as you identify them
- Create specs as you plan features
- Record decisions as you make them

## 🔄 Updating Templates

Templates in makeflow may be updated in new versions. To get updates:

```markdown
@ai Use .makeflow/workflows/00-setup/update-makeflow.md
```

This will update framework templates while preserving your project-specific documentation.

## 📖 Examples

### Example 1: Bootstrap New Project

```bash
# Run bootstrap workflow
@ai Use .makeflow/workflows/00-setup/bootstrap-docs.md

# AI will:
# 1. Scan your codebase
# 2. Generate initial documentation
# 3. Set up structure with these templates
# 4. Create makeflow index
```

### Example 2: Add New Pattern

```bash
# Copy pattern template
cp .makeflow/templates/project-docs/docs/patterns/pattern-template.md \
   docs/patterns/my-pattern.md

# Edit with your pattern details
vim docs/patterns/my-pattern.md

# Link from main README
# Add to docs/README.md under Patterns section
```

### Example 3: Create Specification

```bash
# Copy spec template
cp .makeflow/templates/project-docs/docs/specs/spec-template.md \
   docs/specs/new-feature.md

# Fill in specification details
vim docs/specs/new-feature.md

# Update index if needed
vim .makeflow/project/index.md
```

## 🤝 Contributing

Found a way to improve these templates? Contributions welcome!

1. Test your improvements on real projects
2. Submit PR to makeflow repository
3. Include rationale and examples

## 📞 Getting Help

- **Template usage questions**: See `.makeflow/framework/GUIDE.md`
- **Workflow questions**: See `.makeflow/workflows/` README files
- **Issues or bugs**: https://github.com/ajdurancr/makeflow/issues

---

**Last Updated**: 2025-12-14  
**Templates Version**: 1.0.0

