---
name: forecasting-budgeting
description: >
  Hotel forecasting and budget modeling. Use when the user asks to 'build a forecast', 'create a hotel budget', 'reforecast revenue', 'project GOP', 'model occupancy scenarios', 'forecast F&B revenue', 'labor forecast', or any forward-looking financial projection for a hotel.
metadata:
  version: "1.0.0"
  author: "HospitalityOS"
---

# HospitalityOS™ Hotel Intelligence Suite
## Forecasting & Budgeting Skill

**Professional hotel revenue and expense forecasting — combining historical performance, market assumptions, and booking pace to deliver monthly reforecasts, rolling 90-day projections, and annual budgets with full variance decomposition.**

---

## Data Acquisition

Reference `../DATA_ACQUISITION_PROTOCOL.md` for the complete tiered approach. This skill needs:

**Essential Data:**
- 12–24 months historical P&L by department (Rooms, F&B, Other)
- Group pace report (definite + tentative blocks, decision dates, lead time)
- Transient booking curve (week-by-week pickup from previous years)
- Confirmed room disruptions (renovations, closure dates) and planned events
- Payroll / labor hour allocation by department
- Current-year budget assumptions (market ADR, mix, occupancy targets)
- Seasonal patterns and outlier events (e.g., natural disaster, brand conversion)

**Tier 1 (Direct API):**
- **Gmail** → Pull accounting emails with P&L attachments, budget uploads, variance reports
- **Google Drive** → Access shared budget models, departmental templates, seasonal assumptions
- **Google Sheets** → Live labor trackers, booking curve data, event calendars

**Tier 2 (Browser Pull):**
- **M3 / ProfitSword** → Income Statement, Budget vs Actual, department-level P&L
- **Delphi / Amadeus** → Group pace report, pipeline by decision date, tentative blocks
- **Opera / Mews PMS** → Forecast report, booking pickup, room type distribution
- **STR Portal** → Historical RevPAR, occupancy, rate benchmarks (if available)

**Tier 3 (Manual Upload):**
- Excel file: 24-month P&L (rows: months, columns: departments and line items)
- Excel file: group pace and transient booking curve (rows: future dates, columns: rooms, rate, segment)
- CSV: room disruption calendar (date, reason, rooms out of service, anticipated impact)

---

## Property Context

Before forecasting, **read the property profile** for:
- Seasonality patterns (which months are peak, shoulder, trough)
- Revenue center mix (% Rooms vs F&B vs other)
- Primary guest segments (corporate transient %, group %, leisure %)
- Room type distribution (king/double/suite split)
- Special events or seasonal drivers (convention season, ski resort winter, beach summer)
- Known constraints (union labor, franchise restrictions, market comp set)

---

## Role Detection & Output Customization

The forecast output adapts based on the user's role:

- **General Manager (GM):** High-level 1-page narrative with key numbers, occupancy/ADR trends, profit impact, and 3–5 strategic recommendations
- **Revenue Manager (RM):** Detailed rooms forecast by segment, booking curve variance, rate strategy impact, and segment mix decomposition
- **Finance Director / Controller:** Full P&L reforecast, budget variance with rate/volume/mix drivers, cash flow implications, and departmental variance
- **Director of Sales & Marketing (DOSM):** Group pace detail, conversion assumptions, tentative block risk, and occupancy/revenue impact by sales vector

---

## Core Forecasting Framework

### Rooms Forecast

1. **By Segment** (build separately, then sum):
   - **Transient:** Apply same-year-ago (STYA) booking curve pickup to current pace. Adjust for known rate changes, market softness, or new demand drivers.
   - **Group:** Definite blocks at contracted rate; tentative blocks at high-risk % (default 70% conversion, adjustable). Add in pace of new proposals as they confirm.
   - **Contract / Other:** Extrapolate from historical agreement terms and renewal timing.

2. **Adjust for Disruptions:**
   - Subtract rooms out of service for renovations, maintenance, or natural disasters.
   - Add temporary inventory (overflow partner, pop-up rooms, if applicable).

3. **Check Against Capacity:** Never exceed available rooms. Flag if forecast overbooking.

**Why:** Segment-level forecasting captures different booking behaviors (group books months in advance; transient books days ahead). STYA booking curves are the most reliable anchor for transient demand absent external shocks.

---

### ADR Forecast

1. **By Segment & Room Type:**
   - Extract STYA ADR by segment (transient corp, transient leisure, group, etc.).
   - Factor in **rate strategy changes** (rate fence removals, corporate contract renegotiations, seasonal adjustments).
   - Apply **inflation factor** if market is moving (typically 2–4% YoY in stable markets).
   - Account for **mix shift**: if group is replacing lower-ADR transient, blended ADR may rise or fall even if segment ADR is flat.

2. **Validate Against Comp Set:**
   - If STR or other competitive data is available, check that rate assumptions are reasonable vs. market.

**Why:** ADR is the second lever after occupancy. Separating rate from volume drivers clarifies whether margin pressure comes from losing transient occupancy or from forced rate concessions.

---

### F&B Forecast

1. **Tie to Rooms Occupancy:**
   - Restaurant outlet covers = Occupied Rooms × Avg Covers per Occupied Room (outlet-specific; e.g., 30% breakfast capture, 20% lunch, 35% dinner)
   - Banquet revenue from group blocks: definite covers × contracted rate; tentative blocks at risk-adjusted cover estimates.

2. **Variable Costs:**
   - Food cost % tied to volume (typically 28–35% of F&B revenue); factor in inflation on COGS.
   - Labor (typically 35–45% of F&B revenue) partly variable with volume, partly fixed (kitchen skeleton crew).

3. **Handle Events:**
   - Pull banquet definites from booking system; add separate line for each catered event if needed.

**Why:** F&B is the most correlation-dependent expense; it drives cash and operational leverage. Occupancy swings directly affect restaurant traffic and banquet demand.

---

### Departmental Expense Forecast

1. **Fixed vs. Variable Split:**
   - **Fixed:** Management salaries, rent/lease, insurance, franchise fees, certain utilities (baseline).
   - **Variable:** Housekeeping labor/supplies, food cost, credit card fees, commissions.
   - **Semi-Variable:** Utilities (baseline + variable usage), labor (minimum crew + variable overtime/casual).

2. **Labor Forecast:**
   - Extract actual hours by department from payroll system (Tier 2/3 data).
   - Estimate hours-per-occupied-room (HPR) by department from historical data.
   - Multiply forecasted rooms × HPR × average wage = departmental labor cost.
   - Account for seasonal labor (extra housekeeping in peak, layoff in trough).

3. **Non-Labor:**
   - Supplies: typically 3–6% of department revenue, scale with volume.
   - Utilities: split fixed base + variable per occupied room.
   - Other: depreciation (fixed), repairs & maintenance (fixed baseline + variable emergency spend).

**Why:** Labor is 30–45% of hotel operating costs and is often misforecasted. Tying it to occupancy and HPR metrics prevents naive linear scaling of headcount.

---

### GOP / NOI Projection

- **Gross Operating Profit (GOP)** = Total Revenue − Operating Expenses
- **Flow-Through Model:** Forecast assumes that each incremental $1 of revenue flows through at the current GOP margin (e.g., if GOP margin is 40%, +$100 rooms revenue → +$40 GOP).
- **NOI (Net Operating Income)** = GOP − Debt Service − Reserves. Include capital reserve assumptions (if required by lender or ownership).

**Why:** Flow-through is a simple approximation; actual flow-through varies by segment (group with high F&B mix flows differently than transient). Separately modeling revenue and expense is more accurate than applying a single margin.

---

### Variance Decomposition

**When comparing forecast to budget, always decompose into:**

- **Rate Variance** = (Actual ADR − Budgeted ADR) × Actual Rooms
- **Volume Variance** = (Actual Rooms − Budgeted Rooms) × Budgeted ADR
- **Mix Variance** = (Actual Mix % − Budgeted Mix %) × Room Revenue (if comparing segment-level)

**Example:** Rooms revenue miss of −$50K
- Rate variance: −$10K (ADR came in $5 lower)
- Volume variance: −$30K (missed 2 rooms per night)
- Mix variance: −$10K (higher % of group vs. higher-ADR corporate)

This decomposition tells the revenue manager what to action (rate strategy? occupancy chase? segment rebalance?).

---

## Output Formats

### 1. Rolling 90-Day Forecast
- **Weekly granularity** for the next 12 weeks
- **Columns:** Week, Occ%, ADR, Rooms Revenue, F&B Revenue, Total Revenue, Rooms Cost of Sales, F&B Labor, Total Op Exp, GOP
- **Includes:** Actual YTD vs. forecast for weeks that have closed; forward forecast for open weeks
- **Use Case:** Weekly operations review, cash flow projection, labor scheduling

### 2. Monthly Reforecast
- **Full P&L** for the next 6–12 months in same layout as actual monthly results
- **Variance columns:** Budget vs. Forecast, $ var, % var (by line item)
- **Rate/volume/mix decomposition** for rooms revenue variance
- **Footnotes:** Key assumptions (macro changes, group conversions, labor actions)
- **Use Case:** Monthly board reporting, flash forecasting, departmental accountability

### 3. Annual Budget Model
- **Excel workbook** with tabs:
  1. **Assumptions:** Market ADR range, occupancy targets by segment, group pipeline, labor cost inflation, capital projects
  2. **Monthly Detail:** 12 months of P&L with all departments
  3. **Department Breakdown:** Labor hours by role, supply costs, controllable expenses
  4. **Sensitivity:** Tables showing GOP impact of ±2% ADR, ±3% occ, ±5% labor cost
- **Use Case:** Board approval, annual operating plan, strategic planning

### 4. Executive Summary
- **1-page narrative** for GM/ownership with:
  - Year-over-year and YTD performance vs. budget
  - Key drivers of variance (segment mix, rate actions, cost inflation)
  - Occupancy and ADR outlook for next quarter
  - GOP projection vs. budget; implied profit variance
  - Top 3 risks and mitigation plan
  - Recommended actions (rate adjustment, cost control, revenue initiatives)

---

## Budget Season Workflow

**Step 1: Market Assumptions & Macro**
- Comp set STR data (RevPAR growth, occupancy trend)
- Brand guidance on inflation, franchise fee escalation
- Economic outlook (recession risk, tourism trends)
- Consensus occupancy and ADR targets for the market

**Step 2: Segment Build**
- Transient corporate: historical mix %, ADR sensitivity to market, new corporate clients, travel policy changes
- Transient leisure: OTA dependency, rate elasticity, seasonal swings
- Group: pipeline (converted, committed, tentative), pace assumptions, group ADR (typically discount to transient)
- Contract: renewals, escalations, any expirations

**Step 3: Revenue Centers**
- Rooms: segment build × room count × ADR
- F&B: outlet-by-outlet capture rates, banquet catering pipeline, event calendar
- Other: ancillary (parking, resort fee, spa, golf, etc.)

**Step 4: Expense Build**
- Labor: by department and cost center, headcount plan (hires, attrition), wage inflation, benefits
- Fixed costs: management salaries, rent, utilities baseline, insurance, franchise fees
- Variable: food cost %, supplies, commissions, credit card fees, STR subscriptions

**Step 5: Capital & Reserves**
- Planned capital projects (cost, timing, rooms impact, expected ROI)
- Maintenance reserves (% of revenue or absolute $)
- Working capital assumptions

**Step 6: Consolidation & Approval**
- Sum all segments and departments into consolidated P&L
- Calculate GOP, NOI, EBITDA, EBITDAE
- Run sensitivity on key variables (occupancy, ADR, labor cost)
- Present to ownership for sign-off; document approvals

---

## Key Forecasting Principles

1. **Anchor to History:** Start from STYA and adjust for known changes, not wishes.
2. **Segment Separately:** Transient and group have different booking curves and drivers.
3. **Labor Discipline:** Use HPR and occupancy, not headcount intuition.
4. **Variance Transparency:** Always decompose variance into rate, volume, mix, and cost drivers.
5. **Document Assumptions:** Future you (and finance review) will want to know why you forecasted 65% occ vs. 70%.
6. **Stress Test:** Run upside and downside scenarios; understand breakeven occupancy.
7. **Update Frequently:** Monthly reforecasts (not annual budgets only) keep operations aligned.

---

## Operational Guardrails

- **Never forecast occupancy >100%** or negative revenue/costs.
- **Cross-check occupancy formula:** (Rooms Sold ÷ Available Rooms) × 100 = Occ%. Flag if STYA doesn't explain current pace.
- **Validate ADR:** If ADR is rising but transient rooms are falling, mix is shifting (group is rising). Document explicitly.
- **Labor sanity check:** CPOR (cost per occupied room) should be directionally stable unless staffing model changed. Flag anomalies.
- **Flow-through reality:** If GOP margin is 40% and rooms revenue is up 5%, expect GOP to grow ~6–7% (volume + deflation mix). If it's growing 2%, cost inflation is eating flow-through.

---

HospitalityOS™ — AI-Powered Hotel Intelligence Suite

Forecasting & Budgeting Skill v1.0 | 2026

© HospitalityOS™. All rights reserved.
