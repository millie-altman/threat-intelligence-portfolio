# Scams, Phishing, and System Outages in Interior Alaska
### A Community Case Study Combining Open-Source Reporting with Local Crowdsourced Threat Data

**Author:** Millie
**Type:** Regional cyber-threat case study / OSINT synthesis
**Sources:** FBI/IC3 public reporting, news media, informal community survey (Facebook)

---

## Overview

This case study combines two layers of evidence to map cyber threat activity in Interior Alaska:

1. **Crowdsourced, ground-level data** -- responses to a Facebook post asking Interior Alaska residents what cyber attacks, scams, or suspicious digital activity they had personally encountered.
2. **Open-source reporting on larger incidents** that affected Alaska and the broader U.S. -- the FBI's 2025 Internet Crime Report figures for Alaska, the 2021 ransomware attack on the Alaska Court System, the July 2024 911 outage in the Fairbanks area, and the 2024 Change Healthcare ransomware attack.

The goal is to demonstrate how national- and state-level cyber incidents connect to the day-to-day scam activity residents actually experience, and to practice OSINT collection, source synthesis, and threat-trend analysis on a regional scale.

---

## Methodology

- Community data was collected via an open Facebook post inviting residents of Interior Alaska to share personal experiences with cyber attacks or scams. Responses are anonymized to initials and lightly grouped by theme; substance is unaltered.
- Background incidents were researched using FBI press releases, the IC3 2025 Internet Crime Report, and contemporaneous news coverage (Anchorage Daily News, Alaska Public Media, KTOO, StateScoop, The Hill, AHA, HIPAA Journal, and others).
- This is an informal, open-source case study, not a verified incident database, intended for portfolio and educational purposes.

---

## Statewide and National Context

### Record-Breaking Financial Losses Reported by Alaskans (FBI/IC3, 2025)

Alaskans filed 3,202 complaints with the FBI's Internet Crime Complaint Center (IC3) in 2025, reporting losses of nearly **$40 million**, a 52% increase (over $13.6 million) from 2024 and the highest losses ever recorded in the state for cyber-enabled crime. About 46% of losses (over $18.6 million) were cryptocurrency-related. The costliest categories were:

| Crime Type | 2025 Reported Losses (Alaska) |
|---|---|
| Investment fraud | $13.2 million |
| Confidence/romance fraud | $7.1 million |
| Business email compromise (BEC) | $7 million |

Alaskans 60+ accounted for $16.2 million in losses, the highest of any age group, driven primarily by investment fraud, romance fraud, and tech support scams. Over the past decade, cumulative reported losses in Alaska have exceeded $158 million.

> "Behind these numbers are real people -- Alaskan families who lost hard-earned savings, retirement funds, and financial security." — Matthew Schlegel, SAC, FBI Anchorage Field Office

### Alaska Court System Cyberattack (2021)

In late April 2021, IT staff detected malware on a handful of the Alaska Court System's ~3,000 computers. The system disconnected from the internet on May 1, 2021, taking down CourtView (case search), e-filing, online bail/fee payments, virtual hearing access, and external court email for more than two weeks. No ransom demand was received, and officials reported no evidence that personal data, court records, or payment data were stolen. The attacker's identity and motive were never publicly disclosed. The court breach occurred the same year as a separate, larger cyberattack on Alaska's Department of Health and Social Services, which exposed residents' Social Security numbers and health records.

### Fairbanks-Area 911 Outage (July 2024)

In July 2024, 911 dispatch centers in Fairbanks, Wasilla, and Soldotna went offline for roughly seven hours overnight, forcing Fairbanks International Airport's communications center to temporarily field all 911 traffic for the Fairbanks North Star Borough.

**Important distinction:** this was *not* a cyberattack. It was caused by a faulty software update from CrowdStrike to its "Falcon" security sensor, which triggered system crashes worldwide — affecting airlines, hospitals, banks, broadcasters, and emergency dispatch across multiple states and countries. CrowdStrike confirmed it was an accidental defect, not malicious activity. It's included here as a case study in infrastructure fragility: a single flawed update to a *defensive* security tool was enough to take 911 dispatch offline in Interior Alaska.

### Change Healthcare Ransomware Attack (February 2024)

On February 21, 2024, UnitedHealth Group disclosed that its subsidiary Change Healthcare, a major medical claims clearinghouse, had been compromised by the Russia-linked **ALPHV/BlackCat** ransomware group, which gained access via stolen credentials on a system lacking multi-factor authentication. The resulting outage froze prescription and insurance claims processing for weeks, affecting over 90% of U.S. pharmacies at some point. The breach exposed personal and health data for an estimated 190 million people — the largest healthcare data breach on record — with UnitedHealth Group reportedly paying ~$22 million in ransom and estimating total attack costs near $2.9 billion.

---

## Community-Reported Incidents (Interior Alaska)

*Responses below are anonymized to initials and grouped by theme.*

### Impersonation and Fear-Based Phone Scams
> "I happened to screenshot it because I don't have Venmo or that bank." — B.T.

> "I enjoy 'Social Security' calling me and saying I'm going to be arrested for fraud. I share this with whoever is around me, even strangers. Everyone seems to enjoy it. Fake notoriety can be fun." — C.D.W.

**Analysis:** Classic government-impersonation fraud using arrest threats to create urgency — a tactic the FBI specifically warns against, advising people to "take a beat" before responding.

### Phishing, Account Compromise, and Targeted Fraud
> "Phishing via a 3rd party from a known email. They used an event invitation platform." — A.B.

> "I've had someone who hacked my friend's Instagram and asked to paint a mural of me (she's an art student) and I said yes, and she said she would pay me but ended up scamming me. I lost almost $5,000." — L.W.

**Analysis:** Both cases exploit *trust in an existing relationship or familiar platform* rather than an obviously suspicious approach, consistent with the confidence/romance fraud category that cost Alaskans over $7M in 2025.

### Everyday Consumer Scams
Reported by C.D.:
- Card skimmers at businesses with minimal worker-customer interaction
- Rental listing scams requiring application fees or personal info before a viewing
- Marketplace sellers re-listing the same misrepresented item repeatedly to dodge pattern detection
- "Gift cards" requiring account linkage (email/phone/name), often targeting kids via emotional manipulation
- Fraudulent QR code stickers placed over legitimate ones, or fake instruction sheets in product packaging

### Phone as the Primary Threat Vector
> "I have roughly 300 numbers in my blocked list on my phone. The majority are scam-related. My phone is the biggest threat vector by far with texts and calls. Scam emails have diminished considerably in the past couple of years." — L.L.

**Analysis:** Consistent with the broader industry trend of scammers shifting from email (where spam filtering has improved) to SMS/voice channels with weaker automated defenses.

### Workplace Targeting: Payroll and Direct Deposit Fraud
> "I support HR and payroll the last 10+ years. Every workplace I have been we get phishers posing as employees requesting to update their direct deposit from a random Gmail address... Phishers will typically pose as leaders of the company... The biggest red flag is the urgency and that it must be done as soon as possible." — DB C.

**Analysis:** A textbook Business Email Compromise (BEC) pattern, the same category responsible for $7M+ in reported Alaska losses in 2025. The respondent's mitigation (verifying changes only via work email/employee portal) is a strong real-world control example.

### Government and Local Agency Impersonation
> "The one from the DMV." — B.L.

The Fairbanks Police Department publicly warned of fraudulent "Traffic Violation Ticket Overdue Notice" text messages directing recipients to a fake DMV-styled site, with guidance to not click, not provide information, and report/delete.

---

## Cross-Cutting Themes

- **Urgency is the common thread** across nearly every scam reported, from fake arrest threats to "must be done ASAP" payroll changes.
- **Trust is the attack surface** — the most damaging local scams exploited existing relationships or familiar-looking platforms, not obviously suspicious contacts.
- **Scale varies, mechanics don't** — a gas station skimmer and the Change Healthcare ransomware attack both come down to exploiting a security gap for financial/data gain, just at vastly different scale.
- **Not every outage is an attack** — the July 2024 911 disruption shows that accidental software defects can be as disruptive as deliberate attacks, which matters for resilience planning.
- **Age-based loss patterns** — FBI data shows older Alaskans bear disproportionate financial losses, while younger/general respondents reported a higher *volume* of everyday phishing and marketplace scams — suggesting prevention messaging should be tailored by demographic and scam type.

---

## Sources

- FBI Anchorage Field Office, ["Alaskans Report Record-Breaking Financial Losses from Cyber-Enabled Crimes"](https://www.fbi.gov/contact-us/field-offices/anchorage/news/alaskans-report-record-breaking-financial-losses-from-cyber-enabled-crimes)
- Anchorage Daily News, Alaska Public Media, KTOO, StateScoop, The Hill — 2021 Alaska Court System cyberattack coverage
- Alaska Public Media, NBC News, Anchorage Daily News — July 2024 CrowdStrike/911 outage coverage
- American Hospital Association, HIPAA Journal, Congress.gov CRS, Nixon Peabody — Change Healthcare ransomware attack coverage
- Fairbanks Police Department public scam alert (DMV text scam)
- Community survey responses collected via Facebook (Interior Alaska, June 2026)

---

*This write-up is for educational and portfolio purposes. Community responses are anonymized and shared with permission of the original post's intent (an open community survey).*
