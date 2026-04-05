---
name: reputation-intelligence
description: >
  Guest review analysis and reputation management for hotels. Use when the user asks to 'analyze reviews', 'check our ratings', 'draft a management response', 'reputation report', 'sentiment analysis', 'guest feedback trends', or any review monitoring and response task.
metadata:
  version: "1.0.0"
  author: "HospitalityOS"
---

# HospitalityOS™ Hotel Intelligence Suite
## Guest Review & Reputation Intelligence Skill

### Purpose
Deliver actionable guest review analysis and reputation management intelligence for hotel leaders. Transform raw review data into strategic insights, alert on emerging issues, and enable professional reputation response strategies.

---

## Data Acquisition Protocol
*See detailed specifications in: ../DATA_ACQUISITION_PROTOCOL.md*

### Data Sources by Tier
**Tier 1 – Email Alerts (Primary)**
- Gmail for Revinate/ReviewPro alert notifications
- OTA platform notification emails (TripAdvisor, Google, Booking.com, Expedia)
- Internal survey system alerts

**Tier 2 – Direct Platform Access**
- TripAdvisor Business Admin panel review feeds
- Google Business profile reviews
- Booking.com Property Manager reviews
- Expedia Partner Central reviews
- Revinate and ReviewPro management dashboards
- Social media mention tracking (Facebook, Instagram)

**Tier 3 – Manual Data Input**
- User-pasted review text with platform source and date
- Exported reputation tool reports
- Internal feedback submissions
- Survey data uploads

### Required Data Elements
- Review text (full comment or summary)
- Numeric rating (1–5 scale or platform equivalent)
- Platform source (TripAdvisor, Google, Booking.com, Expedia, direct/internal)
- Review date
- Guest name (optional, often masked by platforms)
- Department impacted (inferred from text or specified)

---

## Property Context
Before analysis begins, establish property context:
- **Brand Promise**: property positioning (luxury, upscale, select-service, economy)
- **Property Type**: full-service hotel, resort, extended stay, boutique, etc.
- **Service Level**: determines tone and depth of response (luxury responses are warmer and personal; select-service are efficient and action-focused)
- **Comp Set**: competitor properties for benchmarking
- **Staff Messaging**: brand voice, typical response tone for management replies
- **Recent Initiatives**: ongoing renovations, staffing changes, service launches (context for trend analysis)

---

## Role-Specific Intelligence

**General Manager**
- Weekly reputation trend briefing (rating trajectory, emerging issues by department)
- Urgent alerts (safety, cleanliness, legal liability, discrimination)
- Competitive benchmarking vs. comp set properties

**Director of Sales & Marketing**
- Competitive reputation positioning (how property ranks vs. market)
- Sentiment themes driving bookings (pool, location, amenities)
- Positive review highlights for marketing asset generation

**Operations & Department Heads**
- Department-specific feedback trends (e.g., front desk speed, housekeeping cleanliness, F&B quality)
- Root cause analysis for negative patterns (e.g., AC noise in building 2 = HVAC maintenance issue)
- Actionable improvement recommendations

---

## Core Analysis Framework

### 1. Review Categorization
Classify each review across three dimensions:

**Department Attribution**
- Front Desk / Check-in
- Housekeeping / Cleanliness
- Food & Beverage
- Maintenance / Facilities
- Pool / Spa / Recreation
- Parking / Valet
- Concierge / Guest Services
- Leadership / Overall
- Other

**Sentiment Classification**
- **Positive**: 4–5 stars, praises specific experience(s)
- **Negative**: 1–2 stars, complains about specific issue(s)
- **Mixed**: 3 stars or contains both praise and criticism

**Thematic Tags**
- Cleanliness, Noise, Staffing, Amenities, Location, Value, Safety, Responsiveness, Decor, Technology, Breakfast, Valet Service, Noise (specify source: AC, neighbors, traffic), etc.

### 2. Trend Detection
**Trailing 90-Day Analysis**
- Track average rating by platform (TripAdvisor, Google, Booking.com, Expedia)
- Identify rating trajectory (improving, declining, stable)
- Flag emerging patterns: 3+ mentions of same issue = potential systemic problem
- Compare recency-weighted sentiment (recent reviews weighted higher)
- Detect seasonal patterns vs. structural issues

### 3. Urgent Flags
Escalate immediately to GM and ownership:
- **Safety Concerns**: injury, theft, assault, break-in
- **Cleanliness Crisis**: bed bugs, mold, pests, hygiene violations
- **Discrimination or Harassment**: guest feels unsafe or unwelcome
- **Health Code Violations**: food poisoning, health inspector findings
- **Legal Liability Exposure**: slip-and-fall, property damage claims
- **Breach of Confidentiality**: staff named or operational secrets exposed

### 4. Competitive Benchmarking
- Compare property's average rating to comp set on same platform
- Identify competitor strengths (e.g., "competitor A has better parking reviews")
- Assess market position (leader, challenger, follower in reputation category)
- Highlight competitive vulnerabilities to address

### 5. Sentiment Scoring
Weight by platform authority and recency:
- **High Authority**: Google (local search), TripAdvisor (independent travelers)
- **Medium Authority**: Booking.com, Expedia (OTA platforms)
- **Recency Multiplier**: reviews <7 days old = 1.5x weight; <30 days = 1.2x; >90 days = 0.5x

---

## Management Response Framework

### Core Principles
- **Tone**: Empathetic, professional, never defensive, never templated
- **Specificity**: Reference the exact experience mentioned in the review (names of dishes, room number if disclosed, specific service issue)
- **Accountability**: Take responsibility where appropriate; avoid blame-shifting
- **Action**: Describe specific corrective action taken or planned (not generic apologies)
- **Calibration**: Match property tier (luxury = personal warmth; select-service = efficient, direct)
- **Confidentiality**: Never reveal staff names (unless positive), compensation details, or sensitive operational info

### Response Structure
1. **Acknowledgment**: "Thank you for taking the time to share your feedback about [specific experience]."
2. **Validation**: "We understand [specific concern], and we take that seriously."
3. **Ownership**: "We fell short of [brand promise], and that's on us." (for negative reviews)
4. **Corrective Action**: "We have already [specific action taken] and [future action planned]."
5. **Recovery**: "We'd love the opportunity to restore your confidence. Please contact [GM/manager name] at [direct contact]." (negative reviews only)
6. **Gratitude**: "Thank you for choosing [property name]." (positive reviews: reinforce brand promise)

### Response Calibration

**Luxury Property Response**
- Warmer, more personal tone
- Reference specific amenity or service experience
- Invite direct relationship with GM
- Offer specific recovery experience

**Select-Service Property Response**
- Efficient, direct, friendly
- Brief acknowledgment and action
- Simple contact method
- Focus on resolution

### Negative Review Response (Key Rules)
- Always include a specific recovery action (never generic "we're sorry")
- Name a recovery opportunity (complimentary upgrade, amenity credit, meal on us)
- Provide direct contact to decision-maker (GM, DOSM, operations manager)
- Avoid deflection or excuses
- Acknowledge impact on guest experience

### Positive Review Response (Key Rules)
- Thank specifically for what they mentioned (don't be generic)
- Reinforce the brand promise they experienced
- Invite return visit or engagement
- Keep response brief (don't overshadow their positive sentiment)

### Response Priority
1. **Critical**: Urgent flags (safety, legal, cleanliness crisis) — respond within 24 hours
2. **High**: Recent negative reviews (last 7 days) — respond within 48 hours
3. **Medium**: Older negative reviews (8–30 days) — respond within 5 business days
4. **Low**: Positive reviews (maintain brand voice) — respond within 2 weeks

---

## Output Formats

### Daily Review Digest
- New reviews in past 24 hours by platform
- Sentiment classification (positive/negative/mixed) with flag icons
- Department attribution and thematic tags
- Draft management response for each review requiring response
- Escalation flags for urgent issues

### Weekly Reputation Briefing
- Rating trend analysis by platform (chart of 90-day trajectory)
- Department performance scorecard (average sentiment score by department)
- Emerging issues (patterns detected, root causes suggested)
- Competitive benchmarking summary
- Response rate and quality metrics (% of reviews responded to, avg response time)
- Action items (staffing, training, infrastructure improvements)

### Monthly Report
- Comprehensive review analytics (volume, sentiment distribution, rating trends)
- Department deep-dives (top strengths, improvement areas)
- Competitive market analysis
- Emerging themes and systemic issues
- Management response effectiveness (guest replies to responses)
- Strategic recommendations for owner reporting

### Response Queue
- Prioritized list of reviews requiring management response
- Draft responses (ready-to-edit)
- Escalation flags (urgent, legal, safety concerns)
- Response owner assignment (GM, DOSM, department manager)
- Target response deadline

---

## Brand Integrity
HospitalityOS™ Guest Review & Reputation Intelligence Skill is a proprietary service of HospitalityOS, Inc. All analysis, response frameworks, and competitive benchmarking data remain confidential to the property operator.

**v1.0.0** | Skill created for HospitalityOS™ Hotel Intelligence Suite
