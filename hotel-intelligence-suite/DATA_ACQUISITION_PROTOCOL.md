# Data Acquisition Protocol — HospitalityOS™ Skills Suite

Every HospitalityOS™ skill uses this three-tier protocol to get the data it needs. The goal is maximum automation with zero broken workflows — if the best method isn't available, gracefully fall to the next tier.

---

## Tier 1: Direct API / MCP Connection (Best Case)

Check for native integrations first. These are fast, reliable, and fully schedulable.

**Available MCPs to check:**
- Gmail MCP → STR email attachments, PMS daily summaries, review alerts, payroll reports
- Google Drive MCP → Budget files, SOPs, shared trackers, brand standards
- Google Sheets MCP → Live operational spreadsheets, labor trackers
- HubSpot MCP → Sales pipeline, contacts, deals, group business
- Google Calendar MCP → BEO dates, group cutoffs, event calendars

**If a direct integration exists for the required data → use it.**
Log: "Pulling [data type] via [MCP name] — Tier 1 acquisition."

---

## Tier 2: Browser-Assisted Data Pull (Intermediate)

If no MCP exists for the source system, attempt to pull data through the browser before asking the user to upload manually.

### Step 1 — Identify the System
Check the property profile for the system name and URL. If unknown, ask once and store in the property profile for future runs.

### Step 2 — Check Login State
Take a screenshot of the browser. Is the user already logged into the target system?

### Step 3 — Handle Authentication
**Claude never stores, types, or manages passwords or MFA codes.**

- If logged in → proceed to Step 4
- If not logged in → ask: "I need to pull [specific report name] from [system name]. Can you log in to [system] in Chrome? I'll navigate from there and pull the data."
- If session expired on a scheduled run → notify: "Your [system] session expired. Log in when you get a chance and I'll grab the [report name], or you can upload it directly."

### Step 4 — Navigate and Extract
Use Chrome browser tools to:
1. Navigate to the reporting section using the system-specific playbook
2. Set the correct parameters (date range, department filters, etc.)
3. Generate or export the report
4. Download or scrape the data

### Step 5 — Validate Before Processing
Before passing data to the processing layer:
- Confirm the date range matches what was requested
- Check for expected columns/fields
- Verify row counts are reasonable (not empty, not suspiciously large)
- Sanity-check totals (occupancy not >100%, no negative room revenue, etc.)

### Failure Handling
If any browser navigation step fails (element not found, unexpected page layout, timeout >30 seconds):
1. Stop the browser pull immediately — do not click randomly or retry blindly
2. Log the failure point and reason
3. Fall through to Tier 3 with a clear message to the user
4. If the same failure occurs 2+ times across sessions, note it in memory so the playbook can be updated

---

## Tier 3: Manual Feed (Fallback)

Tell the user exactly what to provide. Be specific — don't say "upload your data." Say:

1. **System name and navigation path**: "In Opera, go to Reports → Financial → Manager's Report"
2. **Date range needed**: "Pull March 1-31, 2026"
3. **Export format preferred**: CSV > Excel > PDF (in order of preference)
4. **What the file should contain**: "Should have columns for date, room type, rooms sold, revenue, and ADR"
5. **Template (if format matters)**: Provide a sample file or column layout

Accept the upload, validate the structure, and proceed to processing.

---

## System-Specific Browser Playbooks

These are navigation guides for common hotel systems. Each skill references the relevant playbook for its data needs.

### Opera PMS (Oracle Hospitality)
- **Pickup/Pace Report**: Reports → Reservations → Reservation Activity → set date range → Export to CSV
- **Manager's Daily Report**: Reports → Financial → Manager's Report → select date → Export
- **Group Blocks**: Blocks → Block Overview → filter Status: Active → Export
- **Forecast**: Reports → Reservations → Forecast → set date range → Export

### Mews PMS
- **Commander Report**: Dashboard → Reports → Commander Report → select dates → Download CSV
- **Occupancy Report**: Reports → Occupancy → set parameters → Export
- **Revenue Report**: Reports → Revenue → by segment → Export

### M3 Accounting (RealPage)
- **P&L Statement**: Financial Reports → Income Statement → select period → department level → Export Excel
- **Budget vs Actual**: Same path → toggle "Budget Comparison" → Export
- **Trial Balance**: Financial Reports → Trial Balance → select period → Export
- **Flash Report**: Dashboard → Daily Flash → Export

### Delphi / Amadeus Sales & Catering
- **Pipeline / Booking Activity**: Reports → Booking Activity → set status filters → Export
- **Tentative Blocks**: Blocks → Status = Tentative → sort by Decision Date → Export
- **Lost Business**: Reports → Lost Business → set date range → Export
- **BEO Report**: Events → BEO → select event → Print/Export

### STR (Smith Travel Research)
- **Via Email**: Gmail MCP handles this (Tier 1)
- **Via Portal**: Login → Reports → Weekly STAR Report → select property → Download Excel
- **Monthly P&L Benchmarking**: Reports → HOST → select period → Download

### Revinate / ReviewPro / TrustYou
- **Review Export**: Dashboard → Reports → select date range → Download CSV
- **Sentiment Summary**: Analytics → Sentiment → select period → Export
- **Competitive Reputation**: Benchmarking → Comp Set → Export

### ADP / Paylocity / Paycom (Payroll)
- **Labor Distribution**: Reports → Labor Distribution → select pay period → Export Excel
- **Hours by Department**: Time & Attendance → Department Summary → Export
- **Overtime Report**: Reports → Overtime → select period → Export

### HotSchedules / Unifocus (Scheduling)
- **Schedule Export**: Schedules → select week → Department → Export
- **Labor Forecast**: Forecasting → select week → Export
- **Productivity Report**: Reports → Productivity → by department → Export

---

## Universal Data Quality Checks

Run these before processing any data, regardless of acquisition tier:

1. **Missing dates** — flag gaps in time series data
2. **Duplicate entries** — check for repeated rows
3. **Impossible values** — occupancy >100%, negative revenue, $0 ADR with rooms sold
4. **Test data** — rates of $1 or $99,999, guest names like "TEST GUEST"
5. **Stale data** — date ranges that don't match the requested period
6. **Empty exports** — file exists but contains no data rows

If issues are found: flag them clearly, clean what can be cleaned, and proceed with a note about data quality limitations.

---

## Hotel Math Validation

Always cross-check these relationships:

- **Room Revenue** = Occupancy% × Available Rooms × ADR
- **RevPAR** = Room Revenue ÷ Available Rooms = Occupancy% × ADR
- **GOPPAR** = Gross Operating Profit ÷ Available Rooms
- **GOP Flow-Through** = (ΔRevenue − ΔExpense) ÷ ΔRevenue
- **RevPAR Index** = Property RevPAR ÷ Comp Set RevPAR × 100
- **Labor Cost %** = Total Labor Cost ÷ Total Revenue
- **Cost Per Occupied Room (CPOR)** = Department Cost ÷ Occupied Rooms

If calculations don't balance, stop and debug before presenting results.

---

*HospitalityOS™ — AI-Powered Hotel Intelligence*
*© 2026 HospitalityOS.tech. All rights reserved.*
