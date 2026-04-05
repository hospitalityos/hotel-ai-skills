# Connectors

## How tool references work

Plugin files use `~~category` as a placeholder for whatever tool the user connects in that category. Plugins are tool-agnostic — they describe workflows in terms of categories rather than specific products.

## Connectors for this plugin

| Category | Placeholder | Options |
| --- | --- | --- |
| Property Management System | `~~PMS` | Opera PMS, Mews, Cloudbeds, StayNTouch, OPERA Cloud |
| Revenue Management System | `~~RMS` | Duetto, IDeaS, Atomize, OTA Insight |
| Accounting / Back Office | `~~accounting` | M3, ProfitSword, Aptech PVNG, Sage Intacct |
| Sales & Catering | `~~sales catering` | Delphi, Event Temple, MeetingBroker, Tripleseat |
| Reputation Platform | `~~reputation` | Revinate, TrustYou, ReviewPro, GuestRevu |
| STR Benchmarking | `~~STR` | STR (CoStar), Transparent, OTA Insight |
| Payroll / Scheduling | `~~payroll` | ADP, Paychex, HotSchedules, Unifocus, Legion |
| CRM | `~~CRM` | HubSpot, Salesforce, Cendyn |
| Channel Manager | `~~channel manager` | SiteMinder, Cloudbeds, RateGain |
| Spreadsheets | `~~spreadsheets` | Google Sheets, Microsoft Excel |
| Email | `~~email` | Gmail, Outlook |
| File Storage | `~~file storage` | Google Drive, Box, Dropbox |

## Data Acquisition

This plugin uses a 3-tier data acquisition model:

1. **Tier 1 — Direct API/MCP**: If a connector is available for the system, the skill pulls data directly
2. **Tier 2 — Browser-Assisted**: Claude navigates the system in a browser to extract data
3. **Tier 3 — Manual Upload**: User exports files (Excel, CSV, PDF) with guided instructions

Skills always attempt Tier 1 first, then fall back through the tiers automatically.
