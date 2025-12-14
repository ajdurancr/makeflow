# Workflow: Update Documentation

**Stage**: 04 - Delivery  
**Purpose**: Update project documentation for changes  
**Time**: 15-30 minutes  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ Feature adds new APIs or components
- ✅ Feature changes existing behavior
- ✅ User guide needs updates
- ✅ README or technical docs affected

---

## Prerequisites

- [ ] Feature is implemented
- [ ] You understand what needs documenting
- [ ] You know where docs are located

---

## Instructions for AI Agent


### Step 0: Review Project Documentation Index (if available)

**Before identifying documentation needs**, check if `.makeflow/project/index.md` exists:
- **If it exists**: Review it to understand what documentation exists in this project and where it lives
- **Purpose**: This helps you identify which documentation files need to be updated based on the project's documentation structure
- **What to look for**: Documentation locations, existing guides, API reference locations, update procedures
### Step 1: Identify Documentation Needs

**Determine what needs updating**:

```markdown
## 📚 Documentation Assessment

**Feature**: [feature-name]

**Documentation Needed**:
- [ ] **README** - High-level project docs
- [ ] **API Documentation** - New/changed endpoints
- [ ] **Component Docs** - New components
- [ ] **User Guide** - End-user instructions
- [ ] **Setup/Install** - Installation changes
- [ ] **Examples** - Usage examples
- [ ] **Migration Guide** - Breaking changes
- [ ] **Changelog** - Version history
```

### Step 2: Update Each Documentation Type

#### README Updates

**What to add**:
- New features in features list
- Usage examples
- New dependencies
- Breaking changes

**Example**:
```markdown
## Features

- ✅ Multi-select filtering
- ✅ URL-based filter persistence
- ✅ [NEW] Multi-criteria resource filtering
```

#### API Documentation

**For new endpoints**:
```markdown
### POST /api/resources/filter

Filter resources by multiple criteria.

**Request**:
```json
{
  "types": ["Equipment", "Tools"],
  "statuses": ["Active"],
  "locations": ["Building A"]
}
```

**Response**:
```json
{
  "resources": [...],
  "count": 42,
  "total": 156
}
```

**Example**:
```bash
curl -X POST /api/resources/filter \
  -H "Content-Type: application/json" \
  -d '{"types": ["Equipment"]}'
```
```

#### Component Documentation

**For new components**:
```markdown
## ResourceFilters

Multi-select filter component for resources table.

**Props**:
```typescript
interface ResourceFiltersProps {
  types: string[];
  statuses: string[];
  locations: string[];
  onFilterChange: (filters: FilterState) => void;
}
```

**Usage**:
```tsx
<ResourceFilters
  types={selectedTypes}
  statuses={selectedStatuses}
  locations={selectedLocations}
  onFilterChange={handleFilterChange}
/>
```

**Example**:
[Link to Storybook or live example]
```

#### User Guide

**For end users**:
```markdown
## Filtering Resources

### Multi-Criteria Filtering

You can now filter resources by multiple criteria simultaneously:

1. Click the **Type** filter dropdown
2. Select one or more types (e.g., Equipment, Tools)
3. Click the **Status** filter dropdown
4. Select one or more statuses (e.g., Active, Maintenance)
5. Resources update automatically

**Tips**:
- All selected filters must match (AND logic)
- Share filtered views by copying the URL
- Click "Clear all filters" to reset
- The count shows "Showing X of Y resources"

**Screenshot**: [Add screenshot showing filters]
```

#### Changelog

**Add entry**:
```markdown
## [Version X.Y.Z] - YYYY-MM-DD

### Added
- Multi-criteria filtering for resources table (#234)
- URL parameter persistence for filters
- Clear all filters button

### Changed
- Resources table now supports compound filters

### Performance
- Filter updates optimized for datasets > 1000 items
```

### Step 3: Add Examples

**Create or update examples**:

```markdown
## Examples

### Filtering Resources by Multiple Criteria

```typescript
// Example: Filter by equipment that is active
const filters = {
  types: ['Equipment'],
  statuses: ['Active']
};

const filteredResources = await filterResources(filters);
// Returns only Equipment that is Active
```

### Sharing Filtered Views

```
# Share this URL with your team
https://app.com/resources?types=Equipment,Tools&status=Active

# Anyone opening this link will see the filtered view
```
```

### Step 4: Check for Broken Links

**Verify**:
- [ ] All internal links work
- [ ] External links valid
- [ ] Code examples are accurate
- [ ] Screenshots up-to-date

### Step 5: Update makeflow Work Folder

Update `.makeflow/work/[feature-name]/AGENTS.md`:

```markdown
## 📚 Documentation

**Updated**:
- [x] README.md - Added to features list
- [x] docs/api.md - Documented new endpoint
- [x] docs/components.md - Added ResourceFilters docs
- [x] docs/user-guide.md - Added filtering section
- [x] CHANGELOG.md - Added v1.2.0 entry

**Locations**:
- [List paths to updated docs]
```

### Step 6: Present Documentation Updates

```markdown
---

## ✅ Documentation Updated

**Feature**: [feature-name]

### Files Updated:
- `README.md` - [What was added]
- `docs/api.md` - [What was added]
- `docs/user-guide.md` - [What was added]
- `CHANGELOG.md` - [Version entry]

### What Was Documented:
- ✅ API endpoints
- ✅ Component usage
- ✅ User instructions
- ✅ Code examples
- ✅ Changelog entry

---

## 📝 Documentation Summary

**For Developers**:
- API documentation in `docs/api.md`
- Component docs in `docs/components.md`
- Examples in `docs/examples.md`

**For End Users**:
- User guide in `docs/user-guide.md`
- Screenshots added

**Changelog**:
- Version X.Y.Z entry added

---

## 🚀 Next Steps

**If PR not created yet**:
```
@ai Use .makeflow/workflows/04-delivery/create-pr.md
Feature: [feature-name]
```

**If PR exists**:
Push documentation updates to same branch

**If ready to complete**:
```
@ai Use .makeflow/workflows/04-delivery/complete.md
Feature: [feature-name]
```

---

Ready to proceed?
```

---

## Documentation Best Practices

### ✅ DO:
- Write for your audience (devs vs users)
- Include code examples
- Add screenshots for UI features
- Keep examples simple and focused
- Update changelog
- Link related docs

### ❌ DON'T:
- Use jargon without explanation
- Skip examples
- Write overly long docs
- Forget to update changelog
- Leave broken links
- Document implementation details users don't need

---

## Documentation Types Guide

### README.md
**Audience**: New developers, users  
**Content**: Overview, features, quick start, installation  
**Tone**: Friendly, concise

### API Documentation
**Audience**: Developers integrating with your code  
**Content**: Endpoints, parameters, responses, examples  
**Tone**: Technical, precise

### User Guide
**Audience**: End users  
**Content**: How to use features, step-by-step instructions  
**Tone**: Simple, clear, no technical jargon

### Component Documentation
**Audience**: Developers using your components  
**Content**: Props, usage, examples, edge cases  
**Tone**: Technical but helpful

### Changelog
**Audience**: All stakeholders  
**Content**: What changed, when, why (if breaking)  
**Tone**: Factual, concise

---

## Example Documentation Set

### README.md Addition
```markdown
## Features

- ✅ Resource management
- ✅ Assignment tracking
- ✅ Multi-criteria filtering (NEW)
  - Filter by type, status, and location simultaneously
  - Share filtered views via URL
  - Fast performance (< 500ms with 1000+ items)
```

### API Docs (docs/api.md)
```markdown
### Filter Resources

`POST /api/resources/filter`

Apply multiple filter criteria to resources.

**Request Body**:
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| types | string[] | No | Resource types to include |
| statuses | string[] | No | Resource statuses to include |
| locations | string[] | No | Location IDs to include |

**Response**:
```json
{
  "resources": [{ Resource object }],
  "count": 42,
  "total": 156,
  "filters": { Applied filters }
}
```

**Example**:
```bash
curl -X POST /api/resources/filter \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TOKEN" \
  -d '{
    "types": ["Equipment", "Tools"],
    "statuses": ["Active"]
  }'
```

**Errors**:
- `400` - Invalid filter parameters
- `401` - Unauthorized
- `500` - Server error
```

### User Guide (docs/user-guide.md)
```markdown
## Filtering Resources

### How to Use Multi-Criteria Filters

1. **Open the Resources page**
   
2. **Select filters**:
   - Click **Type** dropdown → select one or more types
   - Click **Status** dropdown → select one or more statuses
   - Click **Location** dropdown → select one or more locations
   
3. **View results**:
   - Results update automatically as you select filters
   - See "Showing X of Y resources" at the top
   
4. **Clear filters**:
   - Click "Clear all filters" button to reset

### Tips

- **Share filtered views**: Copy the URL and share with your team
- **Bookmark common filters**: Browser bookmarks work with filtered URLs
- **Combine any filters**: All selected filters work together (AND logic)

[Screenshot: Filters in action]
```

---

## Validation Checklist

- [ ] All relevant docs identified
- [ ] README updated (if needed)
- [ ] API docs updated (if applicable)
- [ ] User guide updated (if applicable)
- [ ] Component docs updated (if applicable)
- [ ] Examples added
- [ ] Changelog updated
- [ ] Screenshots added (for UI changes)
- [ ] Links verified
- [ ] Code examples tested
- [ ] Docs committed to feature branch
- [ ] AGENTS.md updated

---

## Integration with Other Workflows

**After docs updated**:
```
.makeflow/workflows/04-delivery/create-pr.md
```

or

```
.makeflow/workflows/04-delivery/complete.md
```

---

**End of Workflow**

