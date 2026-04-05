---
name: revenue-management
description: >
  Hotel revenue management and dynamic pricing analysis. Use when the user asks about 'rate optimization', 'STR benchmarking', 'RevPAR analysis', 'pickup pace', 'compression night pricing', 'channel mix', 'displacement analysis', or any room pricing and demand strategy question for a hotel property.
metadata:
  version: "1.0.0"
  author: "HospitalityOS"
---

# HospitalityOS™ Hotel Intelligence Suite — Revenue Management & Dynamic Pricing

This skill delivers daily revenue analysis, dynamic pricing recommendations, and strategic rate optimization rooted in pace analysis, STR benchmarking, displacement mathematics, and market intelligence. Use this skill whenever you need to:

- Analyze overnight pickup and pace trends
- Benchmark property performance against comp set (RevPAR Index, ADR Index, Occupancy Index)
- Calculate group vs. transient displacement impact and recommend group acceptance thresholds
- Optimize channel mix and identify rate strategy opportunities
- Provide role-specific revenue intelligence (GM, Revenue Manager, DOSM, Finance)

---

## Data Acquisition

**Read the shared DATA_ACQUISITION_PROTOCOL.md** (`../DATA_ACQUISITION_PROTOCOL.md`) to understand the three-tier acquisition framework.

### Data Requirements for This Skill

This skill requires the following data inputs. Follow the tiers in order; use the best available method:

**Tier 1 — MCP Direct Integration:**
- Gmail MCP: STR weekly email attachments (STAR Report), PMS daily pickup/pace emails, group tentative block notifications
- Google Calendar MCP: Local event calendar, convention center dates, group cutoffs

**Tier 2 — Browser-Assisted Pull:**
- **Opera PMS**: Reports → Reservations → Reservation Activity (pace/pickup by date, by room type)
- **Mews PMS**: Reports → Occupancy (occupancy trend, pickup by source)
- **STR Portal**: Login → Reports → Weekly STAR Report (RevPAR Index, ADR Index, Occ Index, comp set data)
- **Rate Shopping Tools**: Competitive rate intelligence (Opera rate shopping module, IDeaS rate tracker, manual OTA monitoring)

**Tier 3 — Manual Upload:**
- If Tier 1 and Tier 2 fail, ask the user to provide:
  1. **Pickup/Pace Report** (CSV or Excel): Daily reservations by arrival date, source, room type, ADR. Columns needed: arrival_date, source, room_type, rooms_booked, revenue, adr. Current week + STLY (same time last year) comparison.
  2. **STR Weekly STAR** (Excel): Property RevPAR, ADR, Occupancy; Comp Set average; Index calculations (RevPAR Index, ADR Index, Occ Index).
  3. **Group Tentative Blocks** (CSV): Block ID, decision date, in-house dates, room nights, F&B/AV/other revenue, group name, tentative status.
  4. **Channel Production** (CSV): Daily/weekly production by channel (direct, OTA, GDS, wholesale), cost per booking, commission rate.

---

## Property Context

**Read the shared PROPERTY_PROFILE_TEMPLATE.md** (`../PROPERTY_PROFILE_TEMPLATE.md`) and ensure the property profile is complete.

Before analyzing any data, load the property's:
- **Comp Set** (3–5 direct competitors) — your analysis must always benchmark against these
- **Seasonality Pattern** (peak/shoulder/trough months) — a 60% occupancy means different things at a ski resort in January vs. a beach resort in January
- **Segment Mix** (transient corporate, leisure, group, OTA) — influences channel optimization and rate strategy
- **Typical ADR Range** and **RevPAR Index** — anchors all rate recommendations
- **Revenue Centers** (F&B outlets, meeting space, other) — required for group displacement math

---

## Role Detection

Adjust output format and depth based on who is asking. Infer from context; ask if unclear.

- **General Manager (GM)**: Executive summary (1 page max), cross-departmental implications, owner-level decision points.
- **Revenue Manager / Director of Revenue**: Granular detail — rate card by room type and channel, displacement analysis math, specific rate actions with confidence levels.
- **Director of Sales & Marketing (DOSM)**: How pricing affects group strategy, competitive positioning, sales pipeline implications, channel production opportunity.
- **Finance Director / Controller**: Revenue forecast impact, budget variance, GOPPAR implications, P&L line item flow-through.

---

## Core Analysis Framework

### 1. Pickup & Pace Analysis

Compare current booking pace (reservations on-the-books by arrival date) against STLY (same time last year). This is the earliest signal of demand strength or weakness.

**Steps:**
1. Segment current arrivals by date (next 7 days, next 30 days, next 60 days, next 90 days)
2. Compare actual bookings to STLY pace for same arrival dates
3. Calculate acceleration/deceleration rate (current pace ÷ STLY pace − 1)
4. Flag dates where pace is >10% ahead (compression risk) or >15% behind (soft demand, rate reduction opportunity)

**Why it matters:** Pace directly signals whether you can hold rates or need to stimulate demand. A date at 80% occupancy today with decelerating pace has different pricing power than the same date at 80% with accelerating pace.

**Output:** Daily pace report flagging deceleration/acceleration zones.

---

### 2. STR Performance & Comp Set Benchmarking

Parse the weekly STAR Report and calculate index positions. Indices below 100 mean your property is underperforming the comp set on that metric.

**Steps:**
1. Extract **RevPAR Index** (your RevPAR ÷ comp set avg RevPAR × 100)
2. Extract **ADR Index** (your ADR ÷ comp set avg ADR × 100)
3. Extract **Occupancy Index** (your occupancy ÷ comp set avg occupancy × 100)
4. Identify comp set outliers (one competitor driving the average up/down)

**Interpretation:**
- RevPAR Index <95: Urgent — either rates too low or occupancy too low. Investigate which.
- ADR Index <95 + Occ Index >105: You're winning occupancy but leaving ADR on the table. Raise rates.
- ADR Index >105 + Occ Index <95: You're holding rates but losing bookings. Consider rate reduction or promotion.

**Why it matters:** Index performance is the industry's standard benchmarking metric. Owners, franchise companies, and management agreements all reference this data.

**Output:** Weekly or ad-hoc STR summary with highlighted outliers and rate action implications.

---

### 3. Displacement Analysis (Group vs. Transient)

When evaluating a group quote for dates with strong transient demand, calculate the **displacement cost** — the transient revenue you'll lose by accepting the group instead.

**Formula:**
```
Displacement Cost = (Forecasted Transient Demand × Transient ADR) − Group Total Contribution
```

Where:
- **Forecasted Transient Demand** = pace-based demand for those dates, rooms
- **Transient ADR** = your typical transient ADR for that date/season
- **Group Total Contribution** = rooms revenue + F&B + AV + other ancillary (include all per-room incremental P&L impact)

**Example:**
- Group quote: 50 rooms, 3 nights, $80 ADR = $12,000 room revenue
- Forecasted transient demand for those dates: 60 rooms at $140 ADR = $8,400 room revenue
- Group F&B/AV/other: $3,000
- **Total Group Contribution:** $15,000
- **Transient Loss:** $8,400
- **Net Displacement:** Group contribution exceeds transient alternative — **accept**

**Why it matters:** Accepting a low-ADR group on high-demand dates can destroy RevPAR and profit. Displacement analysis forces quantified decision-making.

**Output:** Displacement worksheet (side-by-side group vs. transient math) for each group quote evaluation.

---

### 4. Compression Detection

Identify dates where multiple demand signals (local events, convention activity, high booking pace, search volume trends) suggest pricing power and rate increase opportunity.

**Signals:**
- Pace acceleration >20% vs. STLY
- Local event (concert, conference, sports, holiday)
- Competitor rate increase
- Flight search volume spike (use Google Trends or airline data if available)
- Group blocks landing on high-demand window

**Action:** On compression dates, increase rates 5–15% above seasonal baseline, reduce length-of-stay requirements, tighten cancellation policies.

**Why it matters:** Most properties leave 10–20% of potential revenue on the table by failing to raise rates on compressed dates.

**Output:** Compression calendar with identified windows and recommended rate lift.

---

### 5. Channel Optimization

Compare production, cost, and net revenue contribution by channel (direct, OTA, GDS, wholesale).

**Metrics:**
- Rooms booked and revenue per channel (YTD and monthly)
- Cost per booking (commission + marketing support)
- Net ADR after commission
- Occupancy % attributable to each channel

**Analysis:**
1. Identify highest-contribution channels (highest net ADR after cost)
2. Identify highest-cost channels (highest commission or marketing spend)
3. Compare direct booking ∆ to OTA ∆ (are you gaining or losing direct in competitive set?)
4. Flag channels underperforming their historical mix (e.g., GDS dropping from 12% to 8% of production)

**Action:** Shift marketing spend and rate incentives toward high-contribution channels; reduce reliance on high-cost channels during high-demand periods.

**Why it matters:** A 2% shift in channel mix from OTA (30% commission) to direct (2% commission) = 280 basis points of ADR improvement at same occupancy.

**Output:** Channel mix analysis with specific shift recommendations.

---

### 6. Rate Recommendations

Synthesize all above analysis into specific rate actions. Always explain the reasoning.

**By Room Type & Channel:**
- Standard Room / Direct: $135 (reason: +5% compression signal, +0.5 occupancy index)
- Standard Room / OTA: $138 (reason: match direct ADR within margin, maintain distribution parity)
- Suite / Corporate: $185 (reason: -10% vs. STLY pace on this segment, reduce by $10 to stimulate; apply limit to Tue–Thu)
- Suite / OTA: $195 (reason: higher OTA ADR can absorb commission, don't undercut direct)

**Confidence levels:** High (strong pace signal), Medium (seasonal trend), Low (speculative demand driver).

**Stay-length incentives:** If ADR-sensitive segment (leisure, OTA) is soft, offer +1 night free or 10% discount for 4+ night stays.

---

## Output Formats

This skill can deliver analysis in multiple formats depending on the request:

### Daily Briefing (1 page)
- **Overnight Pickup:** rooms booked last 24 hours vs. STLY, by source
- **Today's Forecast:** occupancy, ADR, RevPAR vs. plan
- **Top 3 Rate Actions:** specific changes for today's bookings
- **Compression Alert:** any dates signaling price power (next 30 days)

### Weekly Analysis (2–3 pages)
- Full STR performance vs. comp set with indices
- Pace analysis (7-day, 30-day, 60-day windows)
- Channel production and mix shift
- Group pipeline and displacement math
- Rate strategy adjustments for next week

### Displacement Worksheet (standalone)
- Group quote details
- Transient demand forecast (by date, room type)
- Contribution math (rooms + F&B + AV + other)
- Recommendation (accept, counter, decline) with reasoning

### Monthly Revenue Report (owner-ready, 3–5 pages)
- Executive summary: RevPAR vs. plan, vs. comp set
- STR indices with trend (3-month rolling)
- Major events and their demand/revenue impact
- Group pace and forward-look
- Rate strategy effectiveness (compare actual ADR to recommended rate)
- Recommendations for next month

---

## Seasonality & Market Intelligence

**Always contextualize analysis within the property's seasonal pattern and local market conditions.**

A 60% occupancy in January means entirely different things at a mountain ski resort (peak season) vs. a coastal beach property (trough) vs. an urban business hotel (normal).

**Before making rate or strategy recommendations:**
1. Confirm the current week's position within the property's seasonality curve (peak, shoulder, trough)
2. Identify any local demand drivers active this week (events, holidays, weather, school calendars)
3. Compare comp set performance to historical norms (are they all soft, or is the market strong?)
4. Account for known forward events (holidays, conventions, group blocks) in forecasts

**Why it matters:** Recommending rate cuts in a trough season (when soft demand is expected and seasonal) is different from cutting rates in peak season (when demand should be strong). Context prevents knee-jerk decisions.

---

## General Operating Principles

- **Never guess data.** If you don't have the required report or file, ask for it explicitly with Tier 3 guidance (system, navigation path, format).
- **Always validate hotel math.** Room Revenue should = Occupancy% × Available Rooms × ADR. If it doesn't, stop and debug.
- **Show your work.** Every rate recommendation, displacement calculation, and index interpretation should be transparent and traceable.
- **Triangulate signals.** Don't rely on pace alone; combine with STR, comp set, events, and channel data. Isolated signals are noise.
- **Adjust for property size.** A 50-room property's group decision calculus differs from a 500-room property. Scale analysis accordingly.
- **Include time horizons.** Distinguish immediate actions (today/this week) from tactical (1–4 weeks out) from strategic (seasonal, multi-quarter positioning).

---

## Questions This Skill Answers

- *How is our pace tracking vs. last year? Should we raise or lower rates?*
- *What's our RevPAR Index this week? How does it compare to the comp set?*
- *Should we accept this group quote, or will we displace too much transient revenue?*
- *Which dates have compression signals? Where can we increase rates?*
- *What's our best-performing channel? Should we shift marketing spend?*
- *What rate recommendations do we need to hit next month's RevPAR target?*
- *How does this week's occupancy compare to seasonality expectation?*

---

HospitalityOS™ — AI-Powered Hotel Intelligence | © 2026 HospitalityOS.tech. All rights reserved.
