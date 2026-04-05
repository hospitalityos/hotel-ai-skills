---
name: sales-pipeline
description: >
  Hotel sales pipeline and group business management. Use when the user asks about 'group pipeline', 'RFP response', 'displacement analysis', 'catering proposal', 'sales production report', 'total revenue contribution', 'tentative blocks', or any hotel sales and events management task.
metadata:
  version: "1.0.0"
  author: "HospitalityOS"
---

# HospitalityOS™ Hotel Intelligence Suite
## Sales Pipeline & Group Business Analysis

---

## Data Acquisition Protocol

**Reference:** ../DATA_ACQUISITION_PROTOCOL.md

**Required Data Inputs:**
- CRM/sales system export: group name, arrival/departure dates, room nights, rate, space needs, F&B minimums, status, decision date
- Transient demand forecast for the property
- Historical group production by segment (corporate, association, SMERF, wedding, government)
- Catering BEOs (banquet event orders) and F&B contracted amounts

**Tier 1 - Direct Integrations:**
- HubSpot MCP: pipeline data, deal stages, contact history
- Gmail MCP: RFP emails, inquiry tracking
- Google Calendar MCP: cutoff dates, decision dates, follow-ups

**Tier 2 - Browser-Based Research:**
- Delphi/Salesforce: booking activity exports, historical deal data
- Cvent: RFP platform details, group requirements
- Property management system: room availability, rate calendars

**Tier 3 - User Provided:**
- Direct exports from sales system (CSV/Excel)
- Pasted RFP details or email content
- Uploaded group sales spreadsheets

---

## Property Context Requirements

- Meeting space inventory: square footage, ceiling height, configurations
- Food & beverage outlets: banquet capacity, catering menu pricing
- Segment mix: historical percentage by corporate/association/SMERF/wedding/government
- Seasonality: peak/shoulder/trough periods for group demand

---

## Role Detection & Customization

**General Manager:** Pipeline health metrics, displacement implications, top priorities
**Director of Sales/Marketing:** Deal prioritization, RFP strategy, competitive positioning
**Revenue Manager:** Displacement analysis, rate optimization, ADR impact
**Finance/Controller:** Group revenue forecasts, variance tracking, budget implications

---

## Core Analysis Framework

### Pipeline Health Assessment
- **Value by Stage:** Total revenue (not just room revenue) at each pipeline stage
- **Conversion Rates:** Historical close rates by stage, segment, source
- **Aging Analysis:** Flag tentatives without updates for >30 days as "stale"
- **Decision Date Tracking:** Calendar view of upcoming cutoff dates and decision points
- **Velocity Metrics:** Average days from inquiry to booking, stage-to-stage cycle time

### Total Revenue Contribution (TRC)
Calculate and rank every group by *total contribution*, not room revenue alone:
- Room revenue = room nights × rate
- F&B revenue = contracted catering minimum + estimated à la carte spend
- AV/A/V rentals = audio/visual package revenue
- Parking revenue = if chargeable to group
- Resort fees = if applicable

**Example:** A 200-room-night group at $179/night with $50K F&B minimum (TRC = $85,800) outranks a 300-room-night group at $199/night with no F&B (TRC = $59,700).

### Displacement Analysis
For every pending group, calculate:
1. **Displaced Transient Revenue:** transient ADR × room nights on those dates
2. **Group Total Contribution:** all revenue streams from group
3. **Displacement Threshold:** Accept groups only if TRC > displaced transient revenue + 15% margin
4. **Opportunity Cost:** quantify what we're giving up if dates decline

### Segment Mix Optimization
- Track production by segment (corporate, association, SMERF, wedding, government)
- Flag over-reliance (>50% of annual revenue from one segment)
- Identify seasonal gaps (e.g., weddings peak spring/fall, corporate peaks Q1/Q4)
- Recommend segment diversification to smooth cash flow and reduce risk

### RFP Response & Proposal Development
When an RFP arrives:
1. Analyze the opportunity (size, dates, segment, complexity)
2. Draft a compelling proposal using property fact sheet
3. Price based on historical win rates and current demand
4. Recommend concessions (comp breakfast, free parking, room upgrades) within margin
5. Include differentiators (meeting space, culinary excellence, service reputation)
6. Set decision deadline aligned with group procurement process

### Win/Loss Tracking
- Log all closed deals: rate negotiated, concessions offered, final outcome
- Capture losses: reason (price, property, alternative selected, meeting relocated)
- Analyze patterns: are we losing to price, venue, or service expectations?
- Refine future strategy based on win/loss insights

### Cutoff Date Management
- Flag upcoming cutoff dates (typically 30-60 days pre-arrival)
- Recommend release vs. extension based on pickup pace vs. historical curve
- Calculate release penalty (forfeited deposit, rate guarantee, room allotment)
- Trigger follow-up calls before cutoff to confirm status

---

## Output Formats

**Weekly Pipeline Dashboard**
- Health snapshot: tentative value, definite bookings, stale deals
- Top 10 priority groups by TRC
- Upcoming decisions/cutoff dates (next 30 days)
- Stage-to-stage conversion metrics

**Displacement Analysis Worksheet**
- Side-by-side comparison: group TRC vs. displaced transient revenue per pending group
- Accept/decline recommendation with ROI calculation
- Margin impact if accepted at proposed rate

**RFP Response Draft**
- Branded proposal template with rate, concessions, and property differentiators
- Rationale for pricing based on demand and historical win data
- Decision deadline and escalation contact

**Monthly Sales Production Report**
- Bookings by segment: room nights, rate, F&B, total revenue
- Pace vs. prior year (PY same month)
- Booking source attribution (direct, meeting planner, OTA, etc.)

**Group Revenue Forecast**
- Monthly room night projection (definite + tentative weighted by close probability)
- Transient revenue forecast comparison
- Group revenue contribution to annual budget

---

## Footer

*HospitalityOS™ is a trademark of Hospitality Operating Systems, Inc. This skill provides strategic analysis and recommendations for group sales management. All pricing and displacement analysis should be validated with your property's historical data and current market conditions. Revenue and pricing decisions remain the responsibility of property management and revenue leadership.*
