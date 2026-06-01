# Defensive Architecture Analysis

This folder contains threat-informed security architecture analysis produced for defense contractors and federal environments. Each analysis translates regulatory compliance requirements and threat intelligence findings into actionable defensive control recommendations mapped to MITRE ATT&CK.

---

## Contents

| Document | Description |
|---|---|
| [Defensive Architecture Analysis — Blue Stripe Tech](./defensive-architecture-analysis.md) | Threat-informed security architecture analysis for a fictional DoD contractor preparing to support the U.S. Air Force Cyber Security Center. Covers Zero Trust design, domain-level control mapping with ATT&CK TTP alignment, RMF lifecycle integration, and prioritized defensive recommendations. |

---

## Supporting Diagrams

| Diagram | Description |
|---|---|
| [Network Architecture](./images/network-architecture.png) | Layered network security architecture showing perimeter controls, DMZ, corporate network segmentation, and SOC integration |
| [RMF Lifecycle](./images/rmf-lifecycle.png) | DoD Risk Management Framework six-step lifecycle with NIST SP 800-series publication mapping |
| [Trust Boundaries](./images/trust-boundaries.png) | Explicit trust boundary enforcement points across User, LAN-to-WAN, and Remote-to-Internal transitions |

---

## Analytical Approach

Architecture analysis in this folder is grounded in two principles:

**Threat-informed design** — control selection is driven by adversary behavior rather than compliance checklists alone. Every control recommendation is mapped to the ATT&CK techniques it mitigates, connecting regulatory requirements to real-world threat actor tradecraft.

**Defense-in-depth** — security controls are layered across architectural domains (User, Workstation, Network, Remote Access, Application) so that failure of any single control does not expose the organization to unmitigated risk.

---

## Regulatory & Framework Alignment

Analysis in this folder applies the following frameworks and compliance drivers:

- NIST SP 800-53 Rev. 5 — Security and Privacy Controls
- NIST SP 800-37 — Risk Management Framework
- DoD Instruction 8510.01 — RMF for DoD IT
- FISMA, DFARS 252.204-7012, CMMC 2.0, Executive Order 13556 (CUI)
- MITRE ATT&CK — TTP mapping for threat-informed control selection

---

## Connection to Portfolio

The defensive recommendations in this analysis are directly informed by the Priority Intelligence Requirements established for Blue Stripe Tech — specifically PIR 1 (nation-state initial access operations) and PIR 3 (CUI exfiltration techniques). The control selections address the adversary behaviors documented in the [Volt Typhoon threat actor profile](https://github.com/millie-altman/threat-actor-profiles/blob/main/nation-state/volt-typhoon.md) and validated through emulation exercises in the [CTI Research Lab](https://github.com/millie-altman/cti-research-lab).
