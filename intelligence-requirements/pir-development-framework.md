# Priority Intelligence Requirements — Development Framework

**Analyst:** Millie Altman

**Classification:** UNCLASSIFIED // FOR PORTFOLIO USE  
**Date:** June 2025  
**Status:** Final  

---

## Purpose

This document defines the methodology used to develop, structure, and maintain Priority Intelligence Requirements (PIRs) for cyber threat intelligence programs. It is intended to serve as a repeatable framework applicable across organizational contexts — from defense contractors to critical infrastructure operators to government agencies.

A PIR is a formally stated intelligence question that drives collection, analysis, and production activity. PIRs exist because intelligence resources are finite — analysts cannot research everything, so leadership must define what questions matter most to the organization's mission and risk posture.

---

## What a PIR Is — and Is Not

**A PIR is:**
- A specific, answerable intelligence question tied to a decision a leader needs to make
- Scoped to a defined time horizon and organizational context
- Prioritized against other PIRs based on mission impact

**A PIR is not:**
- A topic ("ransomware")
- A vague concern ("threat actors targeting us")
- A collection requirement ("monitor dark web forums")
- An already-answered question

The difference between a strong PIR and a weak one is specificity and decision relevance. A strong PIR, when answered, enables a specific defensive or operational decision. A weak PIR produces research that no one acts on.

---

## PIR Development Methodology

### Step 1 — Identify the Decision Maker and Their Decisions

PIRs are not written by analysts for analysts. They are written to support decisions made by leadership — CISOs, operations directors, program managers, or contracting officers. The first step is identifying who needs intelligence and what decisions they are facing.

Questions to ask:
- What decisions does leadership make in the next 30/90/180 days that depend on threat information?
- What would change about those decisions if a specific threat materialized?
- What keeps leadership up at night that intelligence could actually address?

### Step 2 — Identify the Organization's Critical Assets and Functions

PIRs must be grounded in what actually matters to the organization. Work through:
- What data, systems, or capabilities, if compromised, would most impact mission continuity?
- What regulatory obligations (FISMA, DFARS, CMMC) create specific threat exposure?
- What third-party dependencies or supply chain relationships introduce risk?

### Step 3 — Assess the Threat Landscape

Map the organization's profile against known threat actor targeting patterns:
- Which threat actors have historically targeted this sector, geography, or contract type?
- What TTPs are most commonly observed against similar organizations?
- What intelligence gaps exist — what do we not know that we need to know?

### Step 4 — Draft PIR Candidates

Write candidate PIRs using this structure:

```
[Threat Actor or Category] + [Specific Action or Capability] + 
[Against What Asset or Function] + [In What Timeframe or Context]
```

**Strong PIR example:**
> Are nation-state actors, specifically those assessed to target defense industrial base organizations, currently conducting reconnaissance or initial access operations against Blue Stripe Tech's internet-facing VPN infrastructure in advance of the U.S. Air Force contract award?

**Weak PIR example:**
> What are threat actors doing to defense contractors?

### Step 5 — Prioritize PIRs

Not all PIRs are equal. Prioritize using two axes:

| Axis | Question |
|---|---|
| **Likelihood** | How probable is this threat to materialize given current intelligence? |
| **Impact** | If this threat materialized, how severely would it affect mission, operations, or compliance? |

PIRs in the high likelihood / high impact quadrant are Priority 1. Work down from there. Limit active PIRs to a manageable number, typically 3 to 5 for a small CTI program, up to 10 for a mature enterprise program.

### Step 6 — Define Indicators of Satisfaction

For each PIR, define what a satisfactory answer looks like. This prevents PIRs from remaining permanently open and ensures analysts know when they have produced enough intelligence to support a decision.

**Example:** For a PIR asking whether a threat actor is conducting reconnaissance, indicators of satisfaction might include:
- Confirmed or denied presence of scanning activity from known actor infrastructure against organizational assets
- Assessment of whether observed indicators are consistent with pre-compromise targeting patterns
- Recommendation on whether defensive posture adjustment is warranted

### Step 7 — Review and Refresh

PIRs are not permanent. They should be reviewed:
- When a significant threat intelligence development occurs
- When organizational priorities or contract scope changes
- On a defined cycle — quarterly at minimum for active programs

Answered PIRs should be formally closed and archived. New threats may generate new PIRs between review cycles.

---

## PIR Quality Checklist

Before finalizing any PIR, validate it against the following:

- [ ] Is the PIR a question, not a topic or statement?
- [ ] Is it answerable with available or collectable intelligence?
- [ ] Does answering it enable a specific decision?
- [ ] Is it scoped to a defined timeframe or context?
- [ ] Is it distinct from other active PIRs — no overlap?
- [ ] Has it been prioritized relative to other PIRs?
- [ ] Have indicators of satisfaction been defined?

---

## PIR Lifecycle

```
Identify Decision    →    Draft PIR    →    Prioritize
        ↑                                        ↓
   Review & Refresh                       Assign Collection
        ↑                                        ↓
   Close or Update    ←    Produce Report    ←    Analyze
```

---

## Relationship to Intelligence Production

PIRs drive the entire intelligence production cycle:

- **Collection:** What sources should analysts monitor to answer this PIR?
- **Analysis:** What does the collected information tell us about the PIR question?
- **Production:** The finished intelligence product answers the PIR and supports the decision it was built around
- **Dissemination:** The product reaches the decision maker who originated the PIR requirement

A PIR that does not eventually produce a finished intelligence product or inform a defensive decision has failed its purpose.

---

## References

- Office of the Director of National Intelligence — Intelligence Community Directive 204 (Roles and Responsibilities for the National Intelligence Priorities Framework)
- MITRE ATT&CK — Framework for TTP-based collection requirement development
- SANS FOR578 — Cyber Threat Intelligence (PIR development methodology)
- DoD Intelligence Production Program guidance
