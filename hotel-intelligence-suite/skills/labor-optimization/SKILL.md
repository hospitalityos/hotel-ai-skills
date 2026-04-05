---
name: labor-optimization
description: >
  Hotel labor optimization and staffing analysis. Use when the user asks about 'staffing levels', 'labor cost', 'overtime prevention', 'scheduling optimization', 'housekeeping productivity', 'FTE recommendations', 'CPOR labor', or any workforce planning task for a hotel.
metadata:
  version: "1.0.0"
  author: "HospitalityOS"
---

# HospitalityOS™ Hotel Intelligence Suite
## Labor Optimization & Scheduling Intelligence

Maximize operational efficiency and minimize labor costs through demand-driven staffing recommendations, overtime prevention, and productivity benchmarking.

---

## Data Acquisition

**See:** `../DATA_ACQUISITION_PROTOCOL.md`

**Required Inputs:**
- Occupancy forecast (by day, 30-90 days forward)
- Arrivals/departures curve
- Housekeeping standards (minutes per room, deep-clean requirements)
- F&B covers by outlet and meal period
- Banquet BEOs with timing and pax counts
- Current staffing schedules (source of truth)
- Wage rates and overtime rules
- Union/CBA constraints (if applicable)
- PTO calendar

**Data Sources (Priority Tier):**

*Tier 1 (Email/Sheets):*
- Gmail: payroll summaries from ADP, Paylocity, or in-house system
- Google Sheets: current schedule tracker, FTE budget, wage rate lookup

*Tier 2 (Browser):*
- ADP/Paylocity: labor distribution, hours forecast, compliance
- HotSchedules/Unifocus: current schedules, open shifts
- Opera/PMS: occupancy, arrivals/departures, room status

*Tier 3 (User Upload):*
- Time-clock export (last 90 days actual hours)
- Current published schedule (next 4 weeks)
- Occupancy forecast (Excel or CSV)

---

## Property Context & Role Detection

**Property Profile:**
- Union status (full union, partial, non-union) → impacts scheduling constraints
- Total FTEs (budgeted vs. actual)
- Room count and outlet mix (F&B outlets, banquet space, meeting rooms)
- Seasonal patterns (if applicable)

**Role-Based Analysis:**
- **General Manager:** Labor as % of revenue, total property productivity, budget variance
- **Department Head:** Department-specific staffing grid, variance to standard, OT trending
- **Finance Director:** Labor cost forecast, budget compliance, overtime impact, savings opportunities

---

## Core Analysis Framework

### 1. Demand-Based Staffing Model

Calculate required FTE by department and day-part:

- **Housekeeping:** `(Occupied Rooms × Minutes-Per-Room Standard ÷ 60) ÷ Shift Hours`
- **Front Desk:** `Check-Ins Per Hour ÷ Transactions-Per-Agent`
- **F&B:** `Covers Per Meal ÷ Covers-Per-Server` (by outlet)
- **Banquets:** Per BEO event specifications and timeline

### 2. Schedule Optimization

Compare scheduled FTEs to recommended FTEs:
- **Overstaffed:** Scheduled > Recommended by >15% → reduce shifts or reassign
- **Understaffed:** Scheduled < Recommended by >10% → add coverage or adjust service levels
- Highlight specific days, day-parts, and positions for immediate action

### 3. Overtime Prevention

Forecast OT exposure:
- Track MTD hours by employee
- Project remaining scheduled shifts to payroll period end
- Flag employees trending toward OT threshold (1.5x cost)
- Recommend part-time or temporary coverage as lower-cost alternative
- Quantify OT savings if adjustments are made

### 4. Productivity Benchmarking

Measure efficiency against industry standards:
- **Housekeeping:** Rooms cleaned per FTE per shift (target: 15–18 rooms)
- **Front Desk:** Check-ins per agent per hour (target: 12–15)
- **F&B:** Covers per server per shift (target: 60–80, by outlet type)
- Compare to property's own historical benchmarks and external standards

### 5. Cross-Training Opportunities

Identify departments with non-overlapping peak demand:
- Shift staff between housekeeping/F&B during low/high periods
- Build cross-training matrix to enable rapid redeployment
- Quantify labor cost savings from cross-utilization

### 6. Seasonal Staffing Plan

For seasonal and resort properties:
- Build staffing ramp-up schedule tied to occupancy curve
- Identify hiring needs by month and department
- Plan release/reduction schedule with appropriate notice
- Align with PTO blackout dates and union seniority rules

---

## Labor Cost Guardrails

Monitor labor cost as % of revenue:

| Department | Target Range | Alert if Outside |
|------------|------|---------|
| **Rooms** | 18–24% of room revenue | Yes |
| **F&B** | 32–42% of F&B revenue | Yes |
| **Total Hotel** | 42–52% of total revenue | Yes |

For any department outside target band, provide:
- Root cause analysis (overtime, excess staffing, wage inflation, etc.)
- Corrective action plan with timeline
- Projected cost impact of recommended changes

---

## Output Formats

### Weekly Staffing Recommendation
Department × Day grid showing recommended FTEs, scheduled FTEs, variance, and action flags.

### Overtime Risk Alert
Employee name, department, MTD hours, projected period-end hours, OT risk flag, recommended adjustment.

### Monthly Labor Analysis
- Actual vs. budget labor cost ($ and %)
- Productivity metrics vs. benchmarks
- Overtime impact and trends
- Headcount variance (FTE vs. budgeted)
- Recommendations for next period

### Seasonal Staffing Plan
Hiring/release schedule, by month and department, with rationale tied to occupancy forecast.

### Daily Department Card
Per-department summary (staffing, key metrics, top issue) for ops meeting agenda.

---

HospitalityOS™ is a trademark of HospitalityOS, Inc. All rights reserved.
