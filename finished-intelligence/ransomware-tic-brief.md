# Threat Intelligence Collection Brief
## Play Ransomware: Targeting Patterns, TTPs, and Defensive Implications for Defense Contractors

![Ransomware](https://img.shields.io/badge/Threat-Play%20Ransomware-red)
![MITRE ATT&CK](https://img.shields.io/badge/Framework-MITRE%20ATT%26CK-red)
![DoD Contractor](https://img.shields.io/badge/Sector-Defense%20Contractor-navy)
![TLP:CLEAR](https://img.shields.io/badge/TLP-CLEAR-white)
![Status](https://img.shields.io/badge/Status-Final-darkgreen)

**Analyst:** Millie Altman

**Classification:** UNCLASSIFIED // FOR PORTFOLIO USE  
**Date:** June 2025  
**TLP Designation:** TLP:CLEAR  
**Status:** Final  
**Primary Sources:** FBI/CISA/ASD Joint Advisory AA23-352A (Updated June 4, 2025), MITRE ATT&CK v17  

---

## Executive Summary

Play ransomware (also known as Playcrypt) is assessed as one of the most active and operationally sophisticated ransomware groups currently targeting organizations in North America. Since June 2022, the group has compromised approximately 900 entities, with critical infrastructure and defense-adjacent organizations among its documented targets. Play operates as a closed Ransomware-as-a-Service (RaaS) group and employs a double extortion model, exfiltrating data prior to encryption and threatening public release on a Tor-hosted leak site to maximize payment pressure.

This brief provides a comprehensive TTP analysis of Play ransomware, assesses the threat to defense contractor environments, and delivers prioritized defensive recommendations mapped to observed adversary behavior.

---

## Key Judgments

- **[High Confidence]** Play ransomware poses a credible and active threat to defense contractors and organizations handling sensitive government data, based on documented targeting of critical infrastructure sectors and consistent operational tempo through 2025.
- **[High Confidence]** Play's initial access tradecraft, specifically exploitation of known VPN and RDP vulnerabilities and abuse of purchased credentials, directly targets attack surfaces common in contractor environments.
- **[High Confidence]** Play recompiles its ransomware binary for every attack, producing unique hashes per deployment and significantly degrading signature-based detection effectiveness.
- **[Moderate Confidence]** Organizations without mature EDR, network segmentation, and privileged access controls face elevated risk of full domain compromise if Play achieves initial access.
- **[Moderate Confidence]** Play's ESXi variant introduces significant risk to organizations running virtualized infrastructure, potentially enabling mass encryption of VM environments in a single operation.

---

## Threat Actor Profile

| Attribute | Detail |
|---|---|
| **Group Name** | Play (also known as Playcrypt) |
| **Active Since** | June 2022 |
| **Operation Type** | Closed Ransomware-as-a-Service (RaaS) |
| **Extortion Model** | Double extortion — data exfiltration prior to encryption |
| **Known Victims** | ~900 entities as of May 2025 (FBI) |
| **Primary Targeting** | North America, South America, Europe |
| **Target Sectors** | Critical infrastructure, manufacturing, government, defense-adjacent |
| **Motivation** | Financial — ransom payments via cryptocurrency |
| **Leak Site** | Tor-hosted; used to publish stolen data if ransom unpaid |
| **Communication** | Unique @gmx.de or @web.de email per victim; phone-based extortion documented |
| **Attribution Confidence** | Cybercriminal — no assessed nation-state nexus |

**Group Characterization:**
Play distinguishes itself from many ransomware groups through operational discipline and technical sophistication. The group is a closed operation, not openly advertised on criminal forums, which limits affiliate variability and maintains consistent TTP patterns across campaigns. This makes Play's behavior more predictable and therefore more actionable for defensive intelligence purposes.

---

## Threat to Defense Contractor Environments

Defense contractors represent a high-value target category for financially motivated ransomware actors for several reasons:

**Data Value:** Contractors handling CUI, export-controlled technical data, or DoD contract information possess data with significant extortion leverage. The threat of public release on Play's leak site carries substantial reputational, contractual, and regulatory consequences beyond the immediate operational disruption.

**Attack Surface Exposure:** Defense contractors typically operate hybrid environments with remote access infrastructure (VPN, RDP) that must remain accessible for distributed workforces, precisely the attack surface Play prioritizes for initial access. Contractor environments also commonly include virtualized infrastructure subject to Play's ESXi variant.

**Compliance Consequences:** A successful Play intrusion against a DoD contractor would trigger DFARS 252.204-7012 incident reporting obligations (72-hour notification requirement), potential CMMC compliance findings, and could jeopardize contract eligibility.

**Assessed Threat Level: HIGH** for defense contractors without mature VPN patching cadences, privileged access controls, and EDR deployment.

---

## Full Kill Chain Analysis

### Stage 1: Initial Access

Play actors use three primary initial access vectors, all of which are well-documented and exploitable through known, patchable vulnerabilities:

**Vector 1 — Exploitation of Public-Facing Applications (T1190)**
Play has exploited vulnerabilities in FortiOS VPN (CVE-2018-13379, CVE-2020-12812) and Microsoft Exchange (ProxyNotShell: CVE-2022-41040, CVE-2022-41082). In January 2025, initial access brokers with ties to Play exploited CVE-2024-57727 in the SimpleHelp RMM tool to achieve remote code execution against U.S.-based entities.

**Vector 2 — Valid Accounts (T1078)**
Play actors purchase compromised credentials from dark web markets and use them to authenticate directly to victim environments. This technique bypasses perimeter controls entirely when MFA is absent.

**Vector 3 — External Remote Services (T1133)**
Exposed RDP and VPN services are used for direct authentication-based access, frequently combined with purchased credentials.

**CTI Analyst Note:** All three vectors are preventable through consistent patch management and MFA enforcement. The persistence of these vectors in Play's playbook, including CVEs from 2018, indicates the group specifically targets organizations with poor patch hygiene. This is an intelligence-driven observation: organizations patching within 30 days of vendor advisories significantly reduce their exposure to Play's documented initial access techniques.

---

### Stage 2: Discovery & Defense Evasion

Once inside, Play conducts systematic reconnaissance before moving laterally — a hallmark of sophisticated ransomware operations that prioritize pre-encryption data theft.

| Tool / Technique | ATT&CK ID | Purpose |
|---|---|---|
| AdFind | T1016, T1069 | Active Directory queries — maps users, groups, domain structure |
| BloodHound | T1087.002 | AD attack path enumeration — identifies privilege escalation routes |
| Grixba (custom infostealer) | T1518.001 | Enumerates network info; scans for installed antivirus software |
| GMER, IOBit, PowerTool | T1562.001 | Disables antivirus and EDR solutions |
| PowerShell scripts | T1562.001 | Specifically targets Microsoft Defender for disabling |
| Log deletion | T1070.001 | Removes Windows event logs to hinder forensic investigation |

**CTI Analyst Note:** Play's deliberate antivirus enumeration via Grixba before disabling defensive tools demonstrates a disciplined, intelligence-led approach to defense evasion. Organizations relying solely on signature-based antivirus are particularly vulnerable at this stage; if Play disables AV before lateral movement, the rest of the operation proceeds largely undetected.

---

### Stage 3: Lateral Movement & Privilege Escalation

| Tool / Technique | ATT&CK ID | Purpose |
|---|---|---|
| Mimikatz | T1003 | Credential dumping — extracts plaintext passwords and hashes from LSASS |
| WinPEAS | T1059 | Windows privilege escalation enumeration — identifies escalation paths |
| Cobalt Strike | T1071, T1090 | C2 framework — enables persistent remote control and lateral movement |
| SystemBC | T1090.002 | Proxy-based C2 — tunnels traffic to evade network detection |
| PsExec | T1570 | Lateral tool transfer and remote execution across systems |
| Group Policy Objects | T1484.001 | Distributes ransomware executables across the domain at scale |

**CTI Analyst Note:** The use of Group Policy Objects for ransomware distribution is a particularly destructive technique in domain-joined environments, as it allows Play to deploy the ransomware payload to every machine in the domain simultaneously. This is only possible after achieving domain administrator access via Mimikatz. Protecting LSASS and restricting GPO modification rights are, therefore, critical defensive priorities.

---

### Stage 4: Exfiltration

| Tool / Technique | ATT&CK ID | Purpose |
|---|---|---|
| WinRAR | T1560.001 | Compresses stolen data into .RAR archives for staging |
| WinSCP | T1048 | Transfers compressed data to actor-controlled external accounts |

**Exfiltration Pattern:** Play splits data into segments before compression, likely to avoid triggering data loss prevention (DLP) size thresholds. Data is staged locally before transfer — defenders should monitor for unusual WinRAR/WinSCP activity on servers containing sensitive data.

---

### Stage 5: Encryption & Impact

| Technique | ATT&CK ID | Detail |
|---|---|---|
| Data Encrypted for Impact | T1486 | AES-RSA hybrid encryption; intermittent encryption of every other 0x100000 byte block |
| Unique binary per attack | T1027 | Ransomware recompiled for every deployment — unique hash evades signature detection |
| .PLAY extension appended | T1486 | Encrypted files receive .PLAY extension; ransom note (ReadMe.txt) placed in C:/Users/Public/Music/ |
| ESXi variant | T1486 | Powers off all VMs; encrypts .vmdk, .vmem, .vmx, and related VM files using AES-256 |
| Financial Extortion | T1657 | Double extortion — payment demanded via cryptocurrency; non-payment results in leak site publication |
| Telephone extortion | T1657 | Victims receive direct phone calls threatening data release; calls are routed to help desks and customer service numbers found via OSINT |

**CTI Analyst Note:** Play's use of intermittent encryption (encrypting partial file blocks rather than entire files) is specifically designed to maximize encryption speed across large environments while still rendering files unusable. This technique reduces the window between ransomware deployment and full encryption — shrinking the defensive response window to minutes.

---

## Complete ATT&CK TTP Matrix

| Tactic | Technique | ID | Observed Behavior |
|---|---|---|---|
| Initial Access | Exploit Public-Facing Application | T1190 | FortiOS, Exchange, SimpleHelp CVE exploitation |
| Initial Access | Valid Accounts | T1078 | Dark web purchased credentials |
| Initial Access | External Remote Services | T1133 | RDP and VPN abuse |
| Discovery | Network Service Discovery | T1016 | AdFind, Grixba network enumeration |
| Discovery | Security Software Discovery | T1518.001 | Grixba scans for installed AV/EDR |
| Discovery | Account Discovery (Domain) | T1087.002 | BloodHound AD attack path mapping |
| Defense Evasion | Impair Defenses: Disable/Modify Tools | T1562.001 | GMER, IOBit, PowerTool, PowerShell disable AV/EDR |
| Defense Evasion | Indicator Removal: Clear Windows Logs | T1070.001 | Event log deletion to hinder forensics |
| Defense Evasion | Obfuscated Files or Information | T1027 | Unique binary recompilation per deployment |
| Credential Access | OS Credential Dumping | T1003 | Mimikatz LSASS credential extraction |
| Lateral Movement | Lateral Tool Transfer | T1570 | PsExec remote execution |
| Lateral Movement | Domain Policy Modification | T1484.001 | GPO-based ransomware distribution |
| Command & Control | Application Layer Protocol | T1071 | Cobalt Strike C2 |
| Command & Control | Proxy: External Proxy | T1090.002 | SystemBC traffic tunneling |
| Execution | Command and Scripting Interpreter | T1059.001 | PowerShell execution; SimpleHelp RCE |
| Execution | System Services | T1059 | WinPEAS privilege escalation enumeration |
| Collection | Archive Collected Data | T1560.001 | WinRAR .RAR compression of staged data |
| Exfiltration | Exfiltration Over Alternative Protocol | T1048 | WinSCP data transfer to actor accounts |
| Impact | Data Encrypted for Impact | T1486 | AES-RSA hybrid + intermittent encryption; ESXi AES-256 |
| Impact | Financial Theft / Extortion | T1657 | Double extortion — cryptocurrency ransom + leak site threat |

---

## Indicators of Compromise (IOCs)

> **Note:** The following IOCs are sourced from the FBI/CISA joint advisory AA23-352A (updated June 2025). IOC validity degrades over time as actors rotate infrastructure. Always validate against current threat intelligence feeds before actioning. All URLs and domains have been defanged.

### File Indicators

| Indicator | Type | Notes |
|---|---|---|
| `.PLAY` | File Extension | Appended to all encrypted files |
| `ReadMe.txt` | Ransom Note | Placed in `C:/Users/Public/Music/` |
| `PLAY_Readme.txt` | Ransom Note (ESXi) | Placed in root directory and `/vmfs/volumes/` |
| Grixba | Custom Tool | Information-stealer used for network enumeration and AV detection |

### Behavioral Indicators

| Indicator | Type | Notes |
|---|---|---|
| AdFind.exe execution | Process | AD enumeration — high-confidence indicator of pre-ransomware recon |
| BloodHound execution | Process | AD attack path mapping — pre-compromise indicator |
| Mimikatz execution / LSASS access | Process | Credential dumping — immediate containment trigger |
| WinRAR + WinSCP in sequence | Process | Data staging and exfiltration pattern |
| Defender / AV service stopped via PowerShell | Event | Defense evasion — precedes lateral movement |
| Windows event log clearing | Event | T1070.001 — strong indicator of active intrusion |
| GPO modification pushing executables | Event | Domain-wide ransomware distribution imminent |

### Network Indicators

| Indicator | Type | Notes |
|---|---|---|
| @gmx[.]de email addresses | Email | Unique per victim — used for ransom communications |
| @web[.]de email addresses | Email | Alternate contact domain used in communications |
| Cobalt Strike beacon traffic | Network | C2 communication — typically over HTTPS to blend with normal traffic |
| SystemBC proxy traffic | Network | Tunneled C2 — may appear as legitimate HTTPS |
| WinSCP outbound transfers | Network | Exfiltration — look for large outbound transfers to unknown external IPs |

---

## Defensive Recommendations

Recommendations are prioritized by impact against Play's documented kill chain.

### Priority 1 — Close Initial Access Vectors (Highest Impact)

Play's entire operation depends on achieving initial access through three well-documented, preventable vectors. Closing these eliminates the threat entirely.

- **Patch FortiOS, Microsoft Exchange, and RMM tools immediately.** Play has exploited CVEs from as far back as 2018 — meaning unpatched organizations remain vulnerable years after fixes were available. Establish a 30-day patching SLA for internet-facing systems.
- **Enforce MFA on all remote access services** — VPN, RDP, webmail, and any external-facing application. MFA directly defeats the purchased credentials' initial access vector.
- **Audit and restrict RDP exposure.** RDP should never be directly internet-exposed. Place behind VPN with MFA. Disable where not operationally required.
- **Implement credential monitoring.** Subscribe to dark web credential monitoring services to detect if organizational credentials appear in breach datasets before Play can use them.

### Priority 2 — Detect and Disrupt Pre-Ransomware Activity

Play's dwell time between initial access and encryption provides a detection window — if defenders know what to look for.

- **Alert on AdFind, BloodHound, and Mimikatz execution.** These tools have no legitimate operational use in most environments. Detection of any of these should trigger immediate incident response.
- **Monitor for LSASS access.** Configure EDR rules to alert on any process attempting to read LSASS memory. Credential dumping is the pivot point between initial access and domain compromise.
- **Alert on antivirus service termination via PowerShell.** Play disables AV before moving laterally. This event should trigger an immediate alert.
- **Monitor Windows event log clearing (Event ID 1102, 104).** Log deletion is a reliable indicator of an active intrusion in progress.

### Priority 3 — Limit Blast Radius

If Play achieves initial access, these controls limit how far the intrusion can spread.

- **Implement network segmentation.** Isolate sensitive systems (CUI storage, domain controllers, backup infrastructure) from general workstation networks. Prevents GPO-based domain-wide ransomware distribution.
- **Restrict GPO modification rights.** Only authorized administrators should be able to create or modify Group Policy Objects. Monitor GPO changes as a high-fidelity detection opportunity.
- **Protect and monitor virtualization infrastructure.** Play's ESXi variant can encrypt entire VM environments. Restrict ESXi management interface access, enforce MFA on hypervisor management, and maintain offline VM backups.
- **Implement Privileged Access Workstations (PAWs).** Prevent domain admin credentials from being exposed on standard workstations where Mimikatz could harvest them.

### Priority 4 — Exfiltration Detection & Recovery Readiness

- **Monitor for anomalous WinRAR and WinSCP activity,** particularly on servers hosting sensitive data. Large archive creation followed by outbound transfer is a high-confidence exfiltration pattern.
- **Implement DLP controls** on data repositories containing CUI or contract-sensitive information.
- **Maintain offline, immutable backups** following the 3-2-1 rule (3 copies, 2 media types, 1 offline). Test restoration quarterly. Play encrypts network-connected backups — offline copies are the only reliable recovery path.
- **Develop and exercise a ransomware-specific incident response playbook** that includes DFARS 72-hour reporting obligations, legal counsel notification, and executive communication protocols.

---

## Intelligence Gaps

The following areas represent gaps in current public reporting that would benefit from additional collection:

- **Specific defense contractor targeting criteria** — it is not currently assessed which contractor size, contract type, or clearance level most attracts Play's attention
- **Initial access broker relationships** — the specific dark web markets and brokers supplying Play with purchased credentials are not fully characterized in public reporting
- **Post-compromise dwell time** — average time between initial access and ransomware deployment in contractor-specific intrusions is not well documented
- **ESXi variant deployment triggers** — conditions under which Play deploys the ESXi variant versus the Windows variant are not fully understood

---

## Analytical Confidence Assessment

| Judgment | Confidence | Rationale |
|---|---|---|
| Play is an active threat to defense contractors | **High** | Documented critical infrastructure targeting; ~900 victims as of May 2025; consistent operational tempo |
| VPN/RDP exploitation remains primary initial access vector | **High** | Consistent across FBI investigations through January 2025; updated CISA advisory June 2025 |
| Unique binary recompilation defeats signature-based AV | **High** | Confirmed by CISA advisory; consistent with observed detection failures in victim environments |
| Play is financially motivated, not nation-state | **High** | No assessed nation-state nexus; double extortion model is characteristic of cybercriminal operations |
| ESXi variant represents escalating risk to virtualized environments | **Moderate** | Confirmed capability; deployment frequency in contractor environments not fully characterized |

---

## References & Source Confidence

| Source | Confidence | Notes |
|---|---|---|
| FBI/CISA/ASD Joint Advisory AA23-352A (June 2025) | **High** | Primary source; based on FBI investigations through January 2025 |
| MITRE ATT&CK v17 — Software Entry: Play | **High** | Authoritative TTP framework mapping |
| CISA Known Exploited Vulnerabilities Catalog | **High** | Authoritative CVE validation source |
| DFARS 252.204-7012 | **High** | Authoritative regulatory source for contractor incident reporting obligations |

---

*This brief was produced for portfolio demonstration purposes. All analytical judgments are the author's own, derived from publicly available sources. This is an UNCLASSIFIED document containing no sensitive or classified information.*
