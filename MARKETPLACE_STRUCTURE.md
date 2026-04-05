# Marketplace Structure Guide

This document describes the complete GitHub marketplace repository structure for HospitalityOS Hotel AI Skills.

## Repository Root

```
hotel-ai-skills-marketplace/
├── marketplace.json                    # Claude marketplace manifest (REQUIRED)
├── README.md                          # Marketplace overview and installation guide
├── MARKETPLACE_STRUCTURE.md           # This file
└── hotel-intelligence-suite/          # The actual plugin
```

## marketplace.json

This is the required manifest file that Claude's plugin system reads to understand the marketplace.

```json
{
  "name": "HospitalityOS Hotel AI Skills",
  "description": "Enterprise-grade AI skills for hotel operations teams",
  "plugins": [
    {
      "name": "hotel-intelligence-suite",
      "description": "10 purpose-built AI skills...",
      "path": "./hotel-intelligence-suite"
    }
  ]
}
```

**Key fields:**
- `name`: Display name of the marketplace
- `description`: Short description visible to users
- `plugins[]`: Array of available plugins
  - `name`: Plugin identifier (kebab-case)
  - `description`: What this plugin does
  - `path`: Relative path to plugin directory

## Hotel Intelligence Suite Plugin Structure

```
hotel-intelligence-suite/
├── .claude-plugin/
│   └── plugin.json                    # Plugin metadata and configuration
├── README.md                          # Full plugin documentation
├── CONNECTORS.md                      # Data integration guide
├── DATA_ACQUISITION_PROTOCOL.md       # How data flows into skills
├── PROPERTY_PROFILE_TEMPLATE.md       # Standard hotel data model
├── skills/                            # 10 individual skills
│   ├── revenue-management/
│   │   ├── SKILL.md                   # Skill definition and usage
│   │   └── {references}/              # Reference materials
│   ├── forecasting-budgeting/
│   │   ├── SKILL.md
│   │   └── {references}/
│   ├── pl-variance/
│   ├── labor-optimization/
│   ├── reputation-intelligence/
│   ├── competitive-intelligence/
│   ├── owner-reporting/
│   ├── sop-training/
│   ├── sales-pipeline/
│   └── content-engine/
└── [other documentation files]
```

## Plugin Configuration: plugin.json

Located at: `.claude-plugin/plugin.json`

This file contains metadata that Claude uses to understand the plugin:

```json
{
  "name": "hotel-intelligence-suite",
  "version": "1.0.0",
  "description": "Enterprise-grade AI operating system for hotel teams...",
  "author": {
    "name": "HospitalityOS",
    "homepage": "https://hospitalityos.tech"
  },
  "repository": "https://github.com/hospitalityos/hotel-ai-skills",
  "license": "proprietary",
  "keywords": [
    "hotel", "hospitality", "revenue-management", "forecasting", ...
  ]
}
```

**Key fields:**
- `name`: Unique plugin identifier
- `version`: Semantic versioning
- `description`: Full description (longer than marketplace description)
- `author`: Plugin creator info
- `repository`: GitHub repo URL
- `license`: License type
- `keywords`: Searchable tags for discovery

## Skills

Each skill is self-contained and follows this structure:

```
skill-name/
├── SKILL.md          # Skill documentation:
│                     #   - What it does
│                     #   - When to use it
│                     #   - Example usage
│                     #   - Connected data sources
│                     #   - Required inputs
│                     #   - Output format
└── {references}/     # Supporting materials
```

### The 10 Skills Included

1. **Revenue Management** - Dynamic pricing, occupancy, rate strategy
2. **Forecasting & Budgeting** - Demand forecasting, budget planning
3. **P&L Variance Analysis** - Variance reporting, margin optimization
4. **Labor Optimization** - Staffing, scheduling, cost control
5. **Reputation Intelligence** - Reviews, sentiment, benchmarking
6. **Competitive Intelligence** - Market analysis, competitor tracking
7. **Owner Reporting** - Dashboards, KPI tracking, executive analytics
8. **SOP Training** - Procedure documentation, training content
9. **Sales Pipeline** - Prospect tracking, growth pipeline
10. **Content Engine** - Marketing content generation

## Key Documentation Files

### README.md (Marketplace Root)
- Marketplace overview
- Installation instructions for Claude
- Quick start guide
- Contact/support information

### README.md (Plugin Root)
- Detailed plugin features
- Getting started guide
- Supported hotels/systems
- FAQ

### CONNECTORS.md (Plugin Root)
- List of supported data sources
- Integration setup instructions
- API authentication
- Data mapping details
- Example payloads

### DATA_ACQUISITION_PROTOCOL.md (Plugin Root)
- How data flows into the plugin
- Real-time vs batch processing
- Frequency of updates
- Data quality standards
- Error handling

### PROPERTY_PROFILE_TEMPLATE.md (Plugin Root)
- Standard hotel data model
- Required fields
- Optional fields
- Field validation rules
- Example property profile

## Installation Workflow

1. User runs: `claude plugin add --marketplace https://github.com/hospitalityos/hotel-ai-skills`
2. Claude reads marketplace.json from repo root
3. Claude displays available plugins (hotel-intelligence-suite)
4. User installs plugin
5. Claude reads plugin.json from `.claude-plugin/`
6. Claude indexes all SKILL.md files
7. Plugin is available for use

## GitHub Repository Setup

For this to work as a public Claude marketplace:

1. Repository must be public
2. Must be hosted on GitHub
3. marketplace.json must be at repository root
4. plugin.json must be at `.claude-plugin/plugin.json` relative to plugin path
5. All SKILL.md files must be discoverable

### Recommended GitHub URLs

- Marketplace: `https://github.com/hospitalityos/hotel-ai-skills`
- Raw marketplace.json: `https://raw.githubusercontent.com/hospitalityos/hotel-ai-skills/main/marketplace.json`

## File Naming Conventions

- Directory names: kebab-case (e.g., `revenue-management`)
- SKILL.md: Always named exactly `SKILL.md`
- plugin.json: Always in `.claude-plugin/` directory
- marketplace.json: Always at repository root

## Size & Performance

Current marketplace:
- Total files: 10+ skills with full documentation
- Total size: ~2-5 MB (documentation only, no model weights)
- Git clone time: < 1 second
- Installation time: < 5 seconds

## Versioning

- Plugin version: 1.0.0 (semantic versioning)
- Git tags recommended: v1.0.0, v1.1.0, etc.
- Marketplace updates automatically from main branch
- Latest commit = latest version

## Future Expansion

To add new skills:

1. Create new directory under `skills/`
2. Add SKILL.md with full documentation
3. Update plugin README with new skill
4. No need to update marketplace.json (auto-detected)
5. Commit and push to GitHub
6. Claude marketplace auto-refreshes

---

**Created:** April 4, 2026
**Marketplace Root:** `/sessions/clever-awesome-fermat/hotel-ai-skills-marketplace/`
**Repository:** github.com/hospitalityos/hotel-ai-skills
