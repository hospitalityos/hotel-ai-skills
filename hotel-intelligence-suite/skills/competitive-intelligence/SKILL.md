---
name: competitive-intelligence
description: >
  Hotel competitive intelligence and market positioning. Use when the user asks about 'comp set analysis', 'competitor rates', 'market positioning', 'new supply impact', 'competitor renovations', 'rate shopping', 'SWOT analysis', or benchmarking against competing properties.
metadata:
  version: "1.0.0"
  author: "HospitalityOS"
---

# HospitalityOS™ Hotel Intelligence Suite

Competitive intelligence and market positioning framework for hotel revenue and asset management.

## Data Acquisition

Reference `../DATA_ACQUISITION_PROTOCOL.md` for source verification and refresh cadence.

**Required inputs:** comp set hotel websites, OTA listings, STR data, social media activity, press releases, local news, sales team intel.

**Tier 1 (Cloud/Search):** Gmail for STR reports; web search for news/press releases; public databases.

**Tier 2 (Browser):** Manual scrape of comp set websites, OTA rate pages (Marriott.com, Hilton.com, Booking.com), STR portal direct access.

**Tier 3 (User-Provided):** Comp set hotel names and markets, uploaded STR data, anecdotal sales intel, meeting planner feedback.

## Property Context

Establish property profile: target comp set names, market classification (urban/resort/airport/suburban), positioning tier (upper-upscale/upscale/upper-midscale), demand drivers, seasonal patterns.

## Role Detection

Adapt output depth and format by role:

- **General Manager:** Strategic positioning summary, market context, top 3 counter-moves.
- **Revenue Manager:** Rate intelligence by room type/channel, promotional velocity, occupancy/ADR trade-offs.
- **Director of Sales & Marketing:** Group RFP intelligence, lost/won deals, package differentiation, sales battlecards.
- **Finance/Owner:** Market condition context, new supply impact, RevPAR Index trends, competitive pricing power.

## Core Intelligence Framework

**Rate Intelligence**
Track Best Available Rate (BAR) by room type for each comp set property across channels (direct booking, OTA, GDS). Flag rate changes >5% month-over-month; note channel mix shifts (e.g., OTA rate compression signaling occupancy pressure).

**Package & Promotion Tracking**
Monitor active packages, seasonal promotions, bundled offers (breakfast, parking, spa credits). Identify differentiation gaps and upsell opportunities.

**Capital & Renovation Monitoring**
Track announced/in-progress renovations, PIP completions, brand conversions. These shift competitive positioning for 12–24 months; note supply disruption windows.

**Leadership Changes**
Flag new GM or DOSM appointments at comp set properties; often signal strategy shifts or brand repositioning.

**Group Business Intelligence**
Track wins/losses from shared RFP markets; gather meeting planner feedback on competitor offerings, proposal competitiveness, service gaps.

**Digital Presence**
Benchmark website quality, OTA listing optimization, metadata completeness, social media engagement, guest review sentiment.

**Market Conditions**
Monitor local economic indicators, new supply announcements (under-construction hotels), demand drivers (convention bookings, airport traffic, events), competitive rate environment.

## SWOT Framework

Maintain a living SWOT analysis for each comp set property (Strengths, Weaknesses, Opportunities, Threats). Update quarterly or after significant events (renovations, leadership changes, rate moves). Use to inform positioning strategy and counter-moves.

## Output Formats

- **Monthly Competitive Brief:** Comprehensive comp set update, market trends, recommended counter-moves.
- **Rate Alert:** Triggered when competitor rate change >5% or significant channel shift detected.
- **Sales Battlecard:** One-pager per competitor highlighting key differentiators and positioning tactics.
- **Quarterly Market Positioning Report:** Suitable for ownership/asset manager; includes SWOT, RevPAR Index, supply/demand context.
- **New Supply Alert:** Triggered when new hotel announced or breaks ground in market; includes timeline and impact estimate.

---

*HospitalityOS™ is a trademark of HospitalityOS. This skill is part of the Hotel Intelligence Suite.*
