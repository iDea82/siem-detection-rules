# Threat Hunt Playbook — After-Hours Authentication Anomalies

Hunt ID: TH-2026-001
Author: Adesina Tijani
Date: 2026-05-26
MITRE ATT&CK: T1078 Valid Accounts, T1133 External Remote Services

## Hypothesis
An attacker using compromised credentials is authenticating to systems
outside normal business hours to avoid detection by security staff.

## Trigger
- Threat intelligence indicating credential theft in the sector
- Anomalous authentication volume detected in SIEM
- Periodic scheduled hunt (monthly)

## Data Sources Required
- Windows Security Event Log — Event IDs 4624, 4625, 4648
- VPN authentication logs
- Cloud console login logs — CloudTrail ConsoleLogin

## Investigation Steps
1. Identify accounts with more than 40% after-hours logons
2. Verify with account owner — is this expected behavior?
3. Check source IP against threat intelligence
4. Review what resources were accessed during after-hours sessions
5. Check for lateral movement from flagged accounts
6. Compare against VPN logs

## True Positive Indicators
- Source IP from unusual geographic location
- Source IP matches known threat actor infrastructure
- Account owner confirms no after-hours activity
- Lateral movement detected following after-hours logon

## False Positive Indicators
- On-call staff with legitimate after-hours access patterns
- Service accounts running scheduled tasks
- Employees in different time zones

## Escalation Criteria
- Any account with source IP matching threat intel — P1
- Admin accounts with more than 60% after-hours logons — P2
- Multiple accounts from same source IP — P1

## Hunt Result
[ ] No findings — environment clean for this technique
[ ] Findings — escalated to incident response
[ ] False positives identified — tuning applied
[ ] Detection rule created or updated
