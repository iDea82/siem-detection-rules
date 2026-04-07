# SIEM Detection Rules Library

A collection of production-ready detection rules for **Splunk Enterprise Security** 
and **Microsoft Sentinel**, organized by MITRE ATT&CK tactic and mapped to specific 
adversary techniques.

Each rule includes full documentation, response guidance, known false positives, 
and severity escalation logic — written to be deployed directly into a SOC environment.

---

## Coverage Map

| Tactic | Technique | Rule | SPL | KQL |
|--------|-----------|------|-----|-----|
| Credential Access (TA0006) | T1110 — Brute Force | Brute Force Login Detection | ✅ | ✅ |
| Execution (TA0002) | T1059.001 — PowerShell | Suspicious PowerShell Execution | ✅ | ✅ |
| Exfiltration (TA0010) | T1048 / T1041 — Exfiltration | Large Outbound Data Transfer | ✅ | ✅ |
| Persistence (TA0003) | T1053.005 — Scheduled Task | Suspicious Scheduled Task Creation | ✅ | ✅ |

---

## Repository Structure

siem-detection-rules/
│
├── credential-access/
│   ├── brute-force-detection.spl
│   └── brute-force-detection.kql
│
├── execution/
│   ├── suspicious-powershell.spl
│   └── suspicious-powershell.kql
│
├── exfiltration/
│   ├── large-data-transfer.spl
│   └── large-data-transfer.kql
│
└── persistence/
├── new-scheduled-task.spl
└── new-scheduled-task.kql

---

## Rule Anatomy

Every rule in this library follows the same structure:

**Header** — MITRE ATT&CK mapping, platform, severity, 
description, known false positives, and response guidance.

**Detection Logic** — Query that identifies the specific 
adversary behavior with tunable thresholds.

**Enrichment** — Severity scoring, MITRE tagging, and 
investigation priority fields appended to every result.

**Output** — Clean, analyst-ready table with all fields 
needed to begin investigation immediately.

---

## How to Deploy

### Splunk Enterprise Security
1. Navigate to **Search & Reporting**
2. Paste the `.spl` rule content into the search bar
3. Verify results against your environment
4. Tune thresholds based on your baseline
5. Save as a **Correlation Search** with appropriate alert actions

### Microsoft Sentinel
1. Navigate to **Analytics → Create → Scheduled query rule**
2. Paste the `.kql` rule content into the rule query field
3. Configure the rule frequency and lookback period
4. Set alert severity to match the rule documentation
5. Map to the MITRE ATT&CK technique noted in the rule header

---

## Tuning Guidance

Detection rules are not set-and-forget. Every rule in this 
library should be tuned to your specific environment:

- **Run without thresholds first** — understand your baseline 
  before applying filters
- **Whitelist known-good behavior** — software deployment tools, 
  backup jobs, administrative scripts
- **Track false positive rate** — a rule generating more than 
  5% false positives needs retuning
- **Review quarterly** — attacker techniques evolve, 
  detection logic must evolve with them

---

## MITRE ATT&CK Framework

All rules are mapped to the 
[MITRE ATT&CK Enterprise Matrix](https://attack.mitre.org/). 
Each rule header contains the specific Tactic ID, Technique ID, 
and Sub-technique ID where applicable.

---

## Author

Adesina Tijani — Security Operations Analyst  
Detection Engineering · Splunk ES · Microsoft Sentinel  
[linkedin.com/in/adesina-tijani-6372693b5](https://linkedin.com/in/adesina-tijani-6372693b5)  
[github.com/iDea82](https://github.com/iDea82)