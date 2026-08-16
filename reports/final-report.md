# Cyberion ThreatShield — Final Project Report

## 1. Executive Summary

Cyberion ThreatShield is a SOC detection engineering and threat hunting project designed to demonstrate the end-to-end process of security monitoring, detection, investigation, threat hunting, and incident response.

The project uses Wazuh, Windows telemetry, Sysmon, Sigma detection rules, and MITRE ATT&CK mapping.

---

## 2. Project Objectives

- Build a security monitoring environment.
- Collect Windows security telemetry.
- Develop Sigma detection rules.
- Implement Wazuh detection rules.
- Simulate controlled attack activity.
- Conduct hypothesis-driven threat hunts.
- Investigate security alerts.
- Create incident-response playbooks.
- Map detections to MITRE ATT&CK.
- Assess detection coverage.

---

## 3. Architecture

![Wazuh Architecture](../architecture/wazuh.jpeg)

The environment consists of:

- Windows endpoint
- Sysmon
- Wazuh agent
- Wazuh manager
- Wazuh dashboard
- Attack simulation environment

---

## 4. Detection Engineering

The project contains the following Sigma detections:

| Detection | MITRE ATT&CK | Status |
|---|---|---|
| Suspicious PowerShell | T1059.001 | Implemented |
| Encoded PowerShell | T1059.001 | Implemented |
| Scheduled Task | T1053.005 | Implemented |
| Discovery Commands | Multiple Discovery Techniques | Implemented |

---

## 5. Threat Hunting

Threat hunts conducted:

### Hunt 001 — PowerShell

Investigated suspicious PowerShell execution.

### Hunt 002 — Discovery

Investigated Windows discovery commands.

### Hunt 003 — Persistence

Investigated potential persistence mechanisms.

---

## 6. Incident Investigations

### INC-001 — Suspicious PowerShell

Documented in:

`incidents/INC-001-powershell.md`

### INC-002 — Suspicious Login

Documented in:

`incidents/INC-002-suspicious-login.md`

---

## 7. Incident Response

The project includes response playbooks for:

- Suspicious PowerShell
- Malware detection
- Compromised accounts

---

## 8. MITRE ATT&CK Coverage

Detection coverage is documented in:

`mitre/detection-coverage.md`

---

## 9. Evidence

### Wazuh Agent

![Wazuh Agent](../evidence/wazuh-agent.png)

### Investigation

![Investigation](../evidence/investigation.png)

---

## 10. Dashboard

![Wazuh Dashboard](../dashboards/wazuh-dashboard.png)

---

## 11. Results

Document the actual results obtained during testing.

Examples:

- Number of detections tested: TBD
- Number of successful detections: TBD
- Number of false positives: TBD
- Threat hunts completed: TBD
- Incidents investigated: TBD
- MITRE techniques covered: TBD

---

## 12. Detection Gaps

Document techniques that were not successfully detected and explain why.

---

## 13. Lessons Learned

Document lessons related to:

- Log collection
- Detection engineering
- Threat hunting
- Incident investigation
- False positives
- MITRE ATT&CK
- Incident response

---

## 14. Future Improvements

Potential improvements include:

- Additional Sigma rules
- Additional Windows telemetry
- Network monitoring
- Threat intelligence integration
- Automated response
- Additional MITRE ATT&CK coverage
- Additional attack simulations

---

## 15. Conclusion

Cyberion ThreatShield demonstrates an end-to-end SOC workflow from telemetry collection and detection engineering through threat hunting, incident investigation, incident response, and detection coverage assessment.
