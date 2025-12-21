# Workflow: Update Makeflow

**Stage**: 00 - Setup  
**Purpose**: Check for and apply makeflow updates from upstream  
**Time**: 10-15 minutes  
**AI-Agnostic**: ✅ Works with any AI tool

---

## When to Use This

- ✅ Periodic maintenance (check monthly or quarterly)
- ✅ When you hear about new makeflow features
- ✅ When experiencing issues that might be fixed in newer versions
- ✅ Before starting major new features

---

## Prerequisites

- [ ] Git installed and configured
- [ ] Internet connection to access GitHub
- [ ] Active work in `.makeflow/work/` completed or at a good stopping point

---

## Instructions for AI Agent

### Step 1: Check Current Version

**Read the current version**:
```bash
cat .makeflow/VERSION
```

If file doesn't exist:
- Assume version `0.0.0` (pre-versioning)
- Create `.makeflow/VERSION` file with `0.0.0`

**Output**: "Currently running makeflow v{{CURRENT_VERSION}}"

---

### Step 2: Fetch Latest Version from Upstream

**Set up update cache directory**:
```bash
mkdir -p .makeflow/.update-cache
```

**Option A: Use GitHub CLI** (Preferred):
```bash
gh api repos/ajdurancr/makeflow/contents/VERSION --jq '.content' | base64 -d
```

**Option B: Use curl**:
```bash
curl -s https://raw.githubusercontent.com/ajdurancr/makeflow/main/VERSION
```

**Option C: Clone to update cache**:
```bash
cd .makeflow/.update-cache
rm -rf makeflow-latest
git clone --depth 1 https://github.com/ajdurancr/makeflow.git makeflow-latest
cat makeflow-latest/VERSION
cd ../../
```

**Output**: "Latest version available: v{{LATEST_VERSION}}"

---

### Step 3: Compare Versions

**Parse version numbers** using semantic versioning (MAJOR.MINOR.PATCH):
- Current: `{{CURRENT_MAJOR}}.{{CURRENT_MINOR}}.{{CURRENT_PATCH}}`
- Latest: `{{LATEST_MAJOR}}.{{LATEST_MINOR}}.{{LATEST_PATCH}}`

**Determine update type**:
- **Major update**: `LATEST_MAJOR > CURRENT_MAJOR` (Breaking changes)
- **Minor update**: `LATEST_MINOR > CURRENT_MINOR` (New features)
- **Patch update**: `LATEST_PATCH > CURRENT_PATCH` (Bug fixes)
- **No update**: Versions are equal

**If no update needed**:
- Message: "✅ You're running the latest version of makeflow (v{{CURRENT_VERSION}})"
- Ask: "Would you like to see what's new in this version from CHANGELOG?"
- Clean up: `rm -rf .makeflow/.update-cache/makeflow-latest`
- Stop here

**If update available**:
- Message: "📦 Update available: v{{CURRENT_VERSION}} → v{{LATEST_VERSION}}"
- Continue to next step

---

### Step 4: Fetch and Display CHANGELOG

**Fetch CHANGELOG.md**:
```bash
# Using update cache clone from Step 2, or:
curl -s https://raw.githubusercontent.com/ajdurancr/makeflow/main/CHANGELOG.md
```

**Parse changes between versions**:
- Extract all sections between `## [{{LATEST_VERSION}}]` and `## [{{CURRENT_VERSION}}]`
- Show all intermediate versions if jumping multiple versions

**Display to user**:
```markdown
## 📋 Changes in this Update

### What's New in v{{LATEST_VERSION}}

**Added**:
- Feature 1
- Feature 2

**Changed**:
- Change 1
- Change 2

**Fixed**:
- Fix 1

**Removed**:
- (if any)

### ⚠️ Breaking Changes (if major version bump)

- Breaking change 1: Migration steps
- Breaking change 2: Migration steps
```

**Ask user**: "Would you like to proceed with this update? (yes/no)"

**If user says no**: 
- Clean up: `rm -rf .makeflow/.update-cache/makeflow-latest`
- End workflow

---

### Step 5: Check for Active Work

**Before updating, check** `.makeflow/work/`:
```bash
ls -la .makeflow/work/
```

**If active work exists**:
```markdown
⚠️ **Warning**: Active work detected in `.makeflow/work/`:
- {{feature-name-1}}/
- {{feature-name-2}}/

**Recommendation**: Complete or pause current work before updating to avoid conflicts.

Would you like to:
1. **Stop** and complete current work first (Recommended)
2. **Continue** with update anyway (Advanced)
3. **Cancel** the update
```

**If user chooses "Stop"**: 
- Clean up: `rm -rf .makeflow/.update-cache/makeflow-latest`
- End workflow gracefully

**If user chooses "Cancel"**: 
- Clean up: `rm -rf .makeflow/.update-cache/makeflow-latest`
- End workflow

**If user chooses "Continue"**: Show warning and proceed

---

### Step 6: Backup Current Configuration

**Create backup**:
```bash
# Backup .makeflow/ folder
mkdir -p .makeflow-backups/
cp -r .makeflow/ ".makeflow-backups/backup-v{{CURRENT_VERSION}}-$(date +%Y%m%d-%H%M%S)/"
```

**Output**: "✅ Backup created at `.makeflow-backups/backup-v{{CURRENT_VERSION}}-{{TIMESTAMP}}/`"

---

### Step 7: Download Latest Makeflow

**Use update cache clone** from Step 2 or clone fresh:
```bash
cd .makeflow/.update-cache
rm -rf makeflow-latest
git clone https://github.com/ajdurancr/makeflow.git makeflow-latest
cd makeflow-latest
git checkout v{{LATEST_VERSION}}  # Use tagged version
cd ../../../
```

---

### Step 8: Selective Update

**Update ONLY framework files, preserve project-specific files**:

#### **Files to UPDATE** (overwrite):
```bash
# Framework workflows
cp -r .makeflow/.update-cache/makeflow-latest/.makeflow/workflows/* .makeflow/workflows/

# Framework documentation
rm -rf .makeflow/framework/
cp -r .makeflow/.update-cache/makeflow-latest/.makeflow/framework/ .makeflow/framework/

# Framework templates
cp -r .makeflow/.update-cache/makeflow-latest/.makeflow/templates/* .makeflow/templates/

# Core README
cp .makeflow/.update-cache/makeflow-latest/.makeflow/README.md .makeflow/README.md

# Version file
cp .makeflow/.update-cache/makeflow-latest/VERSION .makeflow/VERSION
```

#### **Files to PRESERVE** (do not touch):
- `.makeflow/project/` (project-specific docs index)
- `.makeflow/work/` (active work)
- `.makeflow/history/` (completed work)
- Custom workflows in `.makeflow/workflows/custom/` (if they exist)

---

### Step 9: Handle Conflicts (Smart Merge)

**Check for custom workflows**:
```bash
# If user has custom workflows, detect them
find .makeflow/workflows -name "*.custom.md" -o -path "*/custom/*"
```

**For each custom workflow**:
- Preserve it
- Check if there's a new official version of similar workflow
- Suggest review if conflicts detected

**Output conflicts** (if any):
```markdown
⚠️ **Potential Conflicts Detected**:

1. Custom workflow `.makeflow/workflows/custom/my-workflow.md` 
   - Similar to new official workflow `01-intake/from-custom.md`
   - **Action**: Review both and decide if you want to keep custom or migrate to official

2. Template customizations detected
   - You have modified `.makeflow/templates/agents-template.md`
   - **Action**: Your version preserved as `.makeflow/templates/agents-template.custom.md`
   - New version at `.makeflow/templates/agents-template.md`
```

---

### Step 10: Validate Installation

**Run validation checks**:

1. **Version file updated**:
   ```bash
   cat .makeflow/VERSION  # Should show {{LATEST_VERSION}}
   ```

2. **Required workflow files exist**:
   ```bash
   ls .makeflow/workflows/01-intake/from-ticket.md
   ls .makeflow/workflows/02-planning/create-spec.md
   ls .makeflow/workflows/03-execution/execute-task.md
   ls .makeflow/workflows/04-delivery/create-pr.md
   ```

3. **Framework docs exist**:
   ```bash
   ls .makeflow/framework/
   ```

4. **Project files preserved**:
   ```bash
   ls .makeflow/project/index.md  # Should still exist
   ls .makeflow/work/              # Should be unchanged
   ls .makeflow/history/           # Should be unchanged
   ```

**Output**: "✅ Validation passed: All essential files present and project data preserved"

---

### Step 11: Clean Up

**Remove update cache**:
```bash
rm -rf .makeflow/.update-cache/makeflow-latest
```

**Output**: "✅ Update cache cleaned up"

---

### Step 12: Commit Changes

**Stage and commit**:
```bash
git add .makeflow/
git commit -m "chore: Update makeflow framework to v{{LATEST_VERSION}}

Updated components:
- Framework workflows
- Framework documentation
- Template system
- Core README

Preserved:
- Project documentation index (.makeflow/project/)
- Active work (.makeflow/work/)
- History (.makeflow/history/)
- Custom workflows

See CHANGELOG: https://github.com/ajdurancr/makeflow/blob/main/CHANGELOG.md#{{LATEST_VERSION}}"
```

---

### Step 13: Post-Update Recommendations

**Show user**:
```markdown
## ✅ Makeflow Updated Successfully!

**Previous version**: v{{CURRENT_VERSION}}
**New version**: v{{LATEST_VERSION}}

### 🎉 What's New:

[Summarize key new features from CHANGELOG]

### 📚 Next Steps:

1. **Review new workflows**: Check `.makeflow/workflows/` for new workflow options
2. **Read framework docs**: See `.makeflow/framework/` for updated documentation
3. **Try new features**: [Specific recommendations based on version changes]
4. **Update project docs**: Run `@ai Use .makeflow/workflows/04-delivery/update-docs.md` if needed

### 🔗 Resources:

- [Full CHANGELOG](https://github.com/ajdurancr/makeflow/blob/main/CHANGELOG.md)
- [Documentation](https://github.com/ajdurancr/makeflow/blob/main/README.md)

### 💾 Backup Location:

Your previous configuration is backed up at:
`.makeflow-backups/backup-v{{CURRENT_VERSION}}-{{TIMESTAMP}}/`

You can restore it if needed:
\`\`\`bash
rm -rf .makeflow/
cp -r .makeflow-backups/backup-v{{CURRENT_VERSION}}-{{TIMESTAMP}}/ .makeflow/
\`\`\`
```

---

## Success Criteria

- [ ] Latest version fetched and compared
- [ ] CHANGELOG displayed to user
- [ ] User approved update
- [ ] Active work checked and handled
- [ ] Backup created
- [ ] Framework files updated
- [ ] Project files preserved
- [ ] Conflicts identified and handled
- [ ] Validation checks passed
- [ ] Update cache cleaned up
- [ ] Changes committed
- [ ] Post-update recommendations shown

---

## Rollback Procedure

**If something goes wrong**:

1. **Restore from backup**:
   ```bash
   # Find your backup
   ls -la .makeflow-backups/
   
   # Restore it
   rm -rf .makeflow/
   cp -r .makeflow-backups/backup-v{{CURRENT_VERSION}}-{{TIMESTAMP}}/ .makeflow/
   
   # Commit rollback
   git add .makeflow/
   git commit -m "chore: Rollback makeflow to v{{CURRENT_VERSION}}"
   ```

2. **Report issue**: https://github.com/ajdurancr/makeflow/issues

---

## Troubleshooting

### Issue: Cannot fetch latest version

**Problem**: Network error or API rate limit  
**Solution**: 
1. Check internet connection
2. Try alternative fetch method (gh CLI → curl → git clone)
3. Wait a few minutes if rate limited

### Issue: Merge conflicts in custom workflows

**Problem**: You've customized workflows that were updated  
**Solution**:
1. Review both versions (backup vs new)
2. Manually merge changes or choose one version
3. Rename custom version with `.custom.md` suffix

### Issue: Validation fails

**Problem**: Essential files missing after update  
**Solution**:
1. Check backup integrity
2. Restore from backup
3. Try update again with verbose logging
4. Report issue if persistent

### Issue: Update cache not cleaned up

**Problem**: `.makeflow/.update-cache/` still exists after update  
**Solution**:
```bash
# Manually remove it
rm -rf .makeflow/.update-cache/
```

---

**Last Updated**: 2025-12-21  
**Workflow Version**: 1.1.0
