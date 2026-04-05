---
name: pl-variance
description: >
  Hotel P&L variance analysis and financial reporting. Use when the user asks about 'P&L variance', 'budget variance', 'flash report', 'CPOR analysis', 'flow-through', 'departmental P&L', 'labor cost analysis', or any hotel financial performance reporting.
metadata:
  version: "1.0.0"
  author: "HospitalityOS"
---

# HospitalityOS™ Hotel Intelligence Suite — P&L Variance Analysis & Financial Reporting

This skill delivers comprehensive monthly P&L variance analysis, budget-to-actual reconciliation, and role-specific financial narratives rooted in variance decomposition, flow-through analysis, and departmental performance tracking. Use this skill whenever you need to:

- Break down revenue and expense variances into root causes and quantified drivers
- Analyze GOP (Gross Operating Profit) flow-through and identify where incremental revenue went
- Calculate CPOR (Cost Per Occupied Room) by department to track efficiency independent of occupancy
- Provide role-specific financial commentary (GM executive narrative, Finance deep-dive, Department head scorecards)
- Deliver owner-ready financial packages with talking points and forward guidance

---

## Data Acquisition

**Read the shared DATA_ACQUISITION_PROTOCOL.md** (`../DATA_ACQUISITION_PROTOCOL.md`) to understand the three-tier acquisition framework.

### Data Requirements for This Skill

This skill requires the following data inputs. Follow the tiers in order; use the best available method:

**Tier 1 — MCP Direct Integration:**
- Gmail MCP: Daily flash report emails from PMS (arrival count, revenue, occupancy), monthly accounting close summary email
- Google Drive MCP: Monthly P&L file (Excel or PDF export), budget file with departmental detail, prior-year actuals

**Tier 2 — Browser-Assisted Pull:**
- **M3 (RealPage)**: Financial Reports → Income Statement → select month → department-level detail → Export Excel
- **Opera PMS**: Reports → Financial → Manager's Report → select date range → Flash Report (daily revenue, occupancy, ADR)
- **Sage Intacct**: Reports → Income Statement → departmental detail → Export
- **ProfitSword**: Dashboard → Monthly Close → P&L by department → Compare to Budget → Export

**Tier 3 — Manual Upload:**
- If Tier 1 and Tier 2 fail, ask the user to provide:
  1. **Monthly P&L (Excel):** Columns needed: Account Code, Account Name, Actual YTD, Budget YTD, Actual MTD, Budget MTD, Prior Year YTD. Rows: revenue by center, all operating expenses by department, fixed costs (admin, utilities, insurance).
  2. **Daily Flash Report (CSV):** Current month YTD occupancy %, ADR, RevPAR, rooms sold, room revenue. Include same-day occupancy and MTD pace vs. budget.
  3. **Labor Report (Excel):** By department: hours worked (salaried, hourly, management), labor cost YTD, labor % of revenue, overtime hours.
  4. **Budget File (Excel):** Mirror P&L structure with annual budget, monthly budget, priors-year actual for comparison.
  5. **AP Aging (Excel):** Invoice date, vendor, amount, days outstanding — to assess cash timing and payables position.
  6. **Capital Expenditure Tracker (Excel):** Project name, budgeted amount, YTD spend, status — to reconcile capex P&L impact.

---

## Property Context

**Read the shared PROPERTY_PROFILE_TEMPLATE.md** (`../PROPERTY_PROFILE_TEMPLATE.md`) and ensure the property profile is complete.

Before analyzing any P&L data, load the property's:
- **Department Structure**: Which revenue centers (Rooms, F&B, Spa, Golf, Parking, etc.)? Which cost centers (Rooms, F&B, Admin, Utilities, Marketing, etc.)?
- **Ownership Reporting Requirements**: Does the owner need monthly reporting? What format (one-pager, full P&L with narrative)? What KPIs matter most (NOI, GOP, cash position)?
- **Fiscal Calendar**: Month-end date, consolidation timeline, audit schedule
- **Budgeted vs. Actual Seasonality**: Peak months vary — budget should reflect this. Compare monthlies, not just YTD, to avoid seasonal distortion.
- **Labor Model**: Staffing by department, typical labor % of revenue, known seasonal ramp-ups (summer F&B, winter housekeeping)
- **Fixed Cost Commitments**: Annual management fee, property taxes, insurance, mortgage — compare to budget

---

## Role Detection

Adjust output format and depth based on who is asking. Infer from context; ask if unclear.

- **General Manager (GM)**: Executive narrative (1 page max), headline variances, talking points for ownership conversations, forward outlook, confidence in next month.
- **Finance Director / Controller**: Detailed variance decomposition by line item (dollar and %), audit trail of assumptions, cash flow implications, close calendar status.
- **Revenue Manager**: Room revenue variance decomposition (occupancy, ADR, mix), flow-through impact on GOP, rate strategy contribution to variance.
- **Department Head (Food & Beverage, Housekeeping, etc.)**: Their department P&L only, comparison to budget and prior year, variance drivers in their control, peer benchmarking (CPOR, labor %).

---

## Core Analysis Framework

### 1. Revenue Variance Decomposition (Rooms Segment)

Break room revenue variance into three quantified components. Never just say "room revenue is down." Say *why*.

**Formula:**
```
Total Room Revenue Variance = Occupancy Variance + ADR Variance + Mix Variance

Occupancy Variance = (Actual Occupancy% − Budget Occupancy%) × Budget Occupancy × Avg Budget ADR
ADR Variance = (Actual ADR − Budget ADR) × Actual Rooms Sold
Mix Variance = Revenue shift between room types or segments (e.g., more suites sold @ higher ADR)
```

**Example:**
- Budget: 75% occupancy, 200 rooms, $120 ADR = $18,000 room revenue
- Actual: 73% occupancy (146 rooms), $128 ADR = $18,688 room revenue
- Variance: +$688 (favorable despite lower occupancy)
  - Occupancy Variance: (73% − 75%) × 75% × 200 × $120 = −$3,600 (unfavorable)
  - ADR Variance: ($128 − $120) × 146 = +$1,168 (favorable)
  - Mix Variance: +$3,120 (booking higher-ADR segments)
  - **Net: +$688** — rate strategy and segment mix offset occupancy softness

**Why it matters:** Identifies which lever (volume, rate, mix) is driving performance. Occupancy down but ADR up? Rate strategy is working. Occupancy down and ADR down? Demand problem, not pricing.

---

### 2. GOP Flow-Through Analysis

Calculate what percentage of incremental revenue reached the bottom line (Gross Operating Profit).

**Formula:**
```
Flow-Through % = (Actual GOP − Budget GOP) ÷ (Actual Revenue − Budget Revenue) × 100
```

**Example:**
- Budget: $100K revenue, $30K GOP
- Actual: $105K revenue, $31.5K GOP
- Incremental revenue: $5K
- Incremental GOP: $1.5K
- Flow-Through: $1.5K ÷ $5K = **30%** (poor; expected 40%+)
- **Investigation:** Where did the other $2K go? Check labor (is the property over-staffed on incremental occupancy?), F&B COGS, utilities, commissions.

**Interpretation:**
- 50%+ flow-through: Healthy — incremental revenue drops mostly to GOP
- 30–50%: Acceptable but investigate specific cost drivers
- <30%: Poor — labor, commissions, or COGS are consuming the incremental revenue

**Why it matters:** Shows operational leverage. If you can't convert incremental revenue to profit, occupancy growth doesn't help the bottom line.

---

### 3. CPOR (Cost Per Occupied Room) Analysis

Track operational efficiency independent of occupancy swings.

**Formula:**
```
CPOR = Departmental Operating Expense ÷ Occupied Rooms
```

**By Department:**
- **Rooms CPOR:** Housekeeping + laundry + amenities + maintenance ÷ occupied rooms. Typical: $20–$40/room. Trend this month-over-month and vs. prior year.
- **F&B CPOR:** F&B labor + COGS ÷ covers (or covers per occupied room for hotel properties). Flags inefficiency (labor per cover too high) or COGS creep.
- **Admin CPOR:** Admin salary + utilities + insurance ÷ occupied rooms. Lower is better but constrained by fixed costs.

**Why it matters:** Two hotels at 70% occupancy can have very different unit economics. CPOR isolates operational efficiency from demand.

**Example:**
- Property A: $15K housekeeping spend, 600 occupied rooms = $25/room
- Property B: $15K housekeeping spend, 750 occupied rooms = $20/room
- Property B is more efficient (lower CPOR) despite same cost, because of higher occupancy and labor productivity.

---

### 4. Department-Level Variance Analysis

For each revenue center and cost center, compare actuals to budget and prior year. Flag variances >5% or >$5K (whichever is larger).

**Steps:**
1. **Rooms Revenue**: Compare total, by segment if available (transient, group, etc.). Tie to occupancy %, ADR, mix.
2. **F&B Revenue**: Compare by outlet (restaurant, bar, room service, catering). Investigate covers (traffic) vs. check average.
3. **Operating Expenses** (Rooms, F&B, Spa, Admin, Sales, Utilities, etc.):
   - Actual YTD vs. Budget YTD
   - Actual YTD vs. Prior Year YTD
   - Trend this month alone vs. budget month and prior year month
4. **Flag & Comment**: If variance >5% or >$5K, write a one-sentence root cause (e.g., "Labor up 8% due to holiday week staffing").

---

### 5. Labor Analysis

Labor is typically 25–35% of revenue at hotels. Drill into it.

**Metrics:**
- Labor cost as % of revenue (YTD, MTD, by department)
- Overtime hours and cost (flag if >5% of total hours)
- Productivity metrics:
  - Housekeeping: rooms cleaned per FTE per shift (target: 16–20 rooms/shift)
  - F&B: covers per server or per labor hour (target: 15–20 covers/hour)
  - Bell desk: arrivals per FTE (target: 40–60 arrivals/shift)

**Compare:**
- Actual labor % vs. budget labor %
- Actual overtime vs. budget overtime
- Actual productivity (rooms/housekeeper, covers/server) vs. budget and prior year

**Why it matters:** Labor variance is usually the biggest controllable cost variance. A 2% labor variance on a $1M hotel is $20K.

---

## Output Formats

This skill can deliver analysis in multiple formats depending on the request:

### Daily Flash Report (1 page)
- **Yesterday's Results**: Rooms sold, occupancy %, ADR, revenue vs. plan
- **MTD Pace**: Occupancy %, ADR, revenue vs. budget and prior year (% complete)
- **Occupancy Forecast**: Expected week-end occupancy vs. budget
- **One Sentence Outlook**: "On pace for 71% occupancy; ADR flat to budget; expect to hit GOP target."
- Delivered by 8 AM

### Monthly Variance Report (3–5 pages)
- Full P&L (revenue by center, expenses by department, GOP, NOI) with variance columns ($ and %)
- Revenue variance decomposition (occupancy, ADR, mix for rooms; covers, check average for F&B)
- GOP flow-through analysis (incremental revenue → incremental GOP)
- CPOR trends by department
- Department-level commentary (one sentence per material variance)
- Labor analysis with overtime and productivity flags
- Forward outlook (confidence in next month, any headwinds or tailwinds)

### Executive Summary (1 page)
- Headline P&L (room revenue, F&B, other revenue, total operating expenses, GOP, NOI)
- Top 3 variances (bullet format, with root cause and action item)
- Confidence statement ("On track for annual budget" or "At risk if labor costs don't moderate")
- Suitable for owner/asset manager email

### Department Performance Cards (per department)
- Single-page card for each department head
- Their P&L (revenue, expenses, contribution), vs. budget and prior year
- CPOR and productivity metrics relevant to their department
- Variance narrative (what's driving their number, and what they control)

---

## Narrative Commentary Guidelines

**Every material variance requires a root cause and action item.**

### Poor narrative:
"F&B revenue is $12K below budget."

### Useful narrative:
"F&B revenue is $12K below budget (−$4K in April YTD). Driven by 8% lower breakfast covers due to the pool deck renovation, which closed outdoor dining April 1–30. Covers are expected to recover 100% May 15 when renovation completes. No action needed; seasonal impact."

---

## General Operating Principles

- **Never guess data.** If you don't have a trial balance or P&L export, ask for it explicitly with Tier 3 guidance.
- **Always validate hotel math.** Revenue should = Rooms + F&B + Other. GOP should = Revenue − Operating Expenses. If it doesn't, stop and debug.
- **Show your work.** Every variance decomposition, flow-through calculation, and CPOR metric should be transparent and traceable to source data.
- **Adjust for seasonality.** A 10% revenue variance in January vs. December means different things. Always compare like months (Jan vs. Jan, not Jan vs. Dec).
- **Include materiality thresholds.** Flag variances >5% or >$5K (whichever is larger). Below that, they're noise.

---

HospitalityOS™ — AI-Powered Hotel Intelligence | © 2026 HospitalityOS.tech. All rights reserved.
