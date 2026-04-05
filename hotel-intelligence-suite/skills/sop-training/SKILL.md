---
name: sop-training
description: >
  Hotel SOP and training documentation generator. Use when the user asks to 'create an SOP', 'write training materials', 'onboarding checklist', 'department procedures', 'brand standards documentation', 'housekeeping standards', 'front desk procedures', or any hotel operations documentation.
metadata:
  version: "1.0.0"
  author: "HospitalityOS"
---

# HospitalityOS™ Hotel Intelligence Suite
## SOP & Training Documentation Skill

This skill generates professional Standard Operating Procedures and comprehensive training documentation for hospitality properties, ensuring consistent service delivery, regulatory compliance, and rapid staff onboarding.

### Data Acquisition Protocol

**Reference:** ../DATA_ACQUISITION_PROTOCOL.md

**Required Inputs:**
- Verbal or written process descriptions from department heads
- Existing brand standards documents
- Current or outdated SOPs
- Safety and compliance requirements
- Training checklists and reference materials

**Data Sources (Priority Order):**
1. **Tier 1:** Google Drive (existing SOP documents), Gmail (brand standards updates)
2. **Tier 2:** Brand extranet systems (Marriott MGS, Hilton Lobby, IHG Merlin) for current brand standards
3. **Tier 3:** User verbal descriptions, rough notes, or legacy SOP documents

### Property Context Requirements

- Brand affiliation (Marriott, Hilton, IHG, independent, etc.)
- Service level (luxury, upscale, mid-scale, economy)
- Union status and negotiated agreements
- Local regulations and health department codes
- Property size and staffing structure

### SOP Structure Template

Every procedure document includes:

**Document Header:**
- Property name and location
- Department and procedure title
- Version date and author
- Review schedule (typically annual)

**Purpose:** One-sentence outcome statement explaining why the procedure exists

**Scope:** Who performs this, when, under what conditions

**Responsible Roles:** Primary performer, supervisor, escalation contacts

**Prerequisites:** Required supplies, system access, training completion

**Step-by-Step Procedure:**
- Numbered steps (one action per step)
- Clear decision points marked as "IF [condition] THEN [action]"
- Estimated completion time for full procedure
- Quality checkpoints integrated throughout

**Safety & Compliance Callouts:** **Bold, prominent formatting** for critical safety or compliance requirements

**Common Exceptions:** 3–5 most frequent "what if" scenarios with resolutions

**Escalation Matrix:** Decision tree for when to contact supervisor, engineering, or MOD

**Version History:** Track changes, authors, and dates

### Department-Specific Frameworks

**FRONT DESK:** Check-in, check-out, walk procedures, VIP handling, complaint resolution, cash handling, night audit

**HOUSEKEEPING:** Room cleaning sequence, departure vs. stayover, deep clean schedule, inspection checklist, lost & found, laundry operations

**F&B:** Table service sequence, bar operations, room service, buffet setup/breakdown, allergen protocols, POS procedures

**ENGINEERING/MAINTENANCE:** Preventive maintenance schedule, work order workflow, emergency response (fire, flood, power outage, elevator entrapment), HVAC seasonal changeover

**SALES & EVENTS:** Site visit protocol, BEO creation, group check-in coordination, event setup and strike

**SECURITY:** Access control, incident reporting, guest de-escalation, emergency evacuation

### Writing Guidelines

- **Audience:** Line-level staff with minimal hospitality experience
- **Language:** Simple, direct, short sentences
- **Format:** Numbered steps for sequences, bullet points for checklists
- **Key actions and safety steps:** Always bolded for visibility
- **Time estimates:** Include for full procedures
- **Visual aids:** Specify where diagrams or photos would enhance clarity
- **Cross-references:** Link to brand standards and related procedures
- **Accessibility:** New hire should complete procedure independently after one read-through plus supervised practice

### Training Package Builder

For comprehensive training programs, structure as:
1. Role overview and expectations
2. Department SOPs ordered by frequency of use
3. Knowledge check questions (5–10 per procedure)
4. 30/60/90-day milestone checklist
5. Cross-training map showing prerequisite skills

### Output Format

- **Medium:** Word document (.docx) using the Word skill for professional formatting
- **Multi-procedure packages:** Include table of contents
- **Length:** Documentation pages typically 8–20 pages depending on department complexity
- **Footer:** HospitalityOS™ Hotel Intelligence Suite trademark

---

**HospitalityOS™ Hotel Intelligence Suite**
Professional hospitality operations software and training documentation.
