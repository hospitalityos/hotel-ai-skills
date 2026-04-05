# HospitalityOS Hotel AI Skills Marketplace - Deployment Checklist

## Pre-Deployment Verification

### Repository Structure
- [x] marketplace.json exists at repository root
- [x] marketplace.json is valid JSON
- [x] README.md exists at repository root
- [x] MARKETPLACE_STRUCTURE.md included for reference
- [x] hotel-intelligence-suite/ directory present
- [x] .claude-plugin/plugin.json exists
- [x] plugin.json is valid JSON

### Plugin Contents
- [x] All 10 skills present and verified:
  - [x] revenue-management
  - [x] forecasting-budgeting
  - [x] pl-variance
  - [x] labor-optimization
  - [x] reputation-intelligence
  - [x] competitive-intelligence
  - [x] owner-reporting
  - [x] sop-training
  - [x] sales-pipeline
  - [x] content-engine
- [x] Each skill has SKILL.md
- [x] Each skill has {references}/ directory
- [x] CONNECTORS.md present
- [x] DATA_ACQUISITION_PROTOCOL.md present
- [x] PROPERTY_PROFILE_TEMPLATE.md present

### Documentation
- [x] Marketplace README explains purpose and installation
- [x] Installation instructions included for Claude
- [x] Website link provided (hospitalityos.tech/skills)
- [x] Contact/support info included
- [x] File sizes reasonable (252K - no model weights)
- [x] All markdown files properly formatted

## Deployment Steps

### Step 1: Create GitHub Repository
1. Create new public GitHub repo: `hospitalityos/hotel-ai-skills`
2. Clone locally
3. Copy entire contents of `/sessions/clever-awesome-fermat/hotel-ai-skills-marketplace/` to repo

### Step 2: Initial Commit
```bash
git add .
git commit -m "Initial: HospitalityOS Hotel AI Skills Marketplace"
git push -u origin main
```

### Step 3: Create Release Tag
```bash
git tag -a v1.0.0 -m "Release v1.0.0: Hotel Intelligence Suite"
git push origin v1.0.0
```

### Step 4: Configure GitHub Settings
- [ ] Repository visibility: Public
- [ ] Add description: "Enterprise-grade AI skills for hotel operations"
- [ ] Add website URL: https://hospitalityos.tech
- [ ] Add topics: `claude-plugin`, `hotel-operations`, `hospitality`, `ai-skills`
- [ ] Enable GitHub Pages (optional, for documentation site)

### Step 5: Register with Claude Marketplace
1. Visit Claude marketplace documentation
2. Register marketplace URL: `https://github.com/hospitalityos/hotel-ai-skills`
3. Verify marketplace.json is discoverable
4. Verify plugin.json is accessible

### Step 6: Installation Testing
```bash
# Test marketplace installation
claude plugin add --marketplace https://github.com/hospitalityos/hotel-ai-skills

# Verify plugins are discoverable
claude plugin list

# Verify each skill is accessible
claude skill list
```

## Post-Deployment

### Monitor & Maintain
- [ ] Monitor GitHub repository for issues
- [ ] Track installation/usage metrics
- [ ] Monitor Claude marketplace stats
- [ ] Collect user feedback

### Update Process (for future versions)
1. Make changes locally
2. Update version in plugin.json
3. Commit with message: "Update: [feature/fix description]"
4. Tag release: `git tag -a vX.Y.Z`
5. Push: `git push origin main && git push origin vX.Y.Z`
6. Claude marketplace auto-updates within 5 minutes

### Adding New Skills
For each new skill:
1. Create directory: `skills/skill-name/`
2. Create SKILL.md with full documentation
3. Create {references}/ subdirectory
4. Update plugin README.md
5. Commit and push
6. No need to modify marketplace.json

## File Locations

**Local Development:** `/sessions/clever-awesome-fermat/hotel-ai-skills-marketplace/`

**Marketplace URL:** `https://github.com/hospitalityos/hotel-ai-skills`

**Raw marketplace.json:** `https://raw.githubusercontent.com/hospitalityos/hotel-ai-skills/main/marketplace.json`

**Claude Installation Command:** `claude plugin add --marketplace https://github.com/hospitalityos/hotel-ai-skills`

## Current Statistics

- **Total Files:** 18
- **Total Directories:** 24
- **Total Size:** 252 KB
- **Skills Included:** 10
- **Plugin Version:** 1.0.0
- **License:** Proprietary (HospitalityOS)

## Marketplace Metadata

- **Marketplace Name:** HospitalityOS Hotel AI Skills
- **Plugin Name:** hotel-intelligence-suite
- **Author:** HospitalityOS
- **Homepage:** https://hospitalityos.tech
- **Keywords:** hotel, hospitality, revenue-management, forecasting, budgeting, labor-optimization, reputation-management, hotel-finance, owner-reporting, RevPAR, hotel-AI, PMS

## Success Criteria

- [x] Repository structure matches Claude marketplace specification
- [x] marketplace.json is valid and discoverable
- [x] plugin.json contains all required metadata
- [x] All 10 skills are present and documented
- [x] README instructions are clear and actionable
- [x] Installation commands work correctly
- [x] File sizes are optimized (no model weights)
- [x] Documentation is complete and professional

## Notes for Maintainers

1. **GitHub Repository Must Be Public** - Claude only reads public repos
2. **marketplace.json at Root** - Non-negotiable path requirement
3. **plugin.json in .claude-plugin/** - Must follow this exact path
4. **SKILL.md Naming** - All skills use exactly this filename
5. **Version Numbers** - Semantic versioning (MAJOR.MINOR.PATCH)
6. **Tags in GitHub** - Create annotated tags for each release
7. **Auto-Updates** - Claude checks main branch every 5-15 minutes

---

**Created:** April 4, 2026
**Marketplace Root:** `/sessions/clever-awesome-fermat/hotel-ai-skills-marketplace/`
**Status:** Ready for GitHub deployment
