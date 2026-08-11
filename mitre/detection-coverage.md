# MITRE ATT&CK Detection Coverage

## Objective

Assess Cyberion-ThreatShield detection coverage against selected MITRE ATT&CK techniques.

## Detection Coverage Matrix

| MITRE ID | Technique | Tactic | Detection | Wazuh Alert | Hunt | Playbook |
|---|---|---|---|---|---|---|
| T1059.001 | PowerShell | Execution | ✅ | ✅ | ✅ | ✅ |
| T1053.005 | Scheduled Task | Persistence | ✅ | ✅ | ✅ | ❌ |
| T1057 | Process Discovery | Discovery | ✅ | ✅ | ✅ | ❌ |
| T1087 | Account Discovery | Discovery | ✅ | ✅ | ✅ | ❌ |
| T1016 | System Network Configuration Discovery | Discovery | ✅ | ✅ | ✅ | ❌ |
| T1046 | Network Service Scanning | Discovery | ⚠️ | ⚠️ | ❌ | ❌ |
| T1078 | Valid Accounts | Defense Evasion | ⚠️ | ⚠️ | ✅ | ✅ |
| T1003 | OS Credential Dumping | Credential Access | ⚠️ | ⚠️ | ❌ | ❌ |

## Legend

- ✅ Fully implemented
- ⚠️ Partially implemented
- ❌ Not implemented

## Detection Gaps

### Gap 1

Technique: T1046

Issue: Detection requires additional network telemetry.

Planned improvement: Add network monitoring and detection logic.

### Gap 2

Technique: T1003

Issue: Credential-access telemetry is currently limited.

Planned improvement: Improve endpoint telemetry and detection coverage.

## Improvement Plan

1. Identify detection gaps.
2. Determine required telemetry.
3. Create detection rules.
4. Test against simulated activity.
5. Validate Wazuh alerts.
6. Document investigation procedure.
7. Update the coverage matrix.
