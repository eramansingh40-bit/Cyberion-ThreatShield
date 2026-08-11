# Threat Hunt 003 — Persistence Activity

## 1. Objective

Identify suspicious persistence mechanisms on Windows endpoints.

## 2. Hypothesis

An attacker may attempt to maintain access to a compromised Windows endpoint.

## 3. MITRE ATT&CK

Potential techniques:

- T1053.005 — Scheduled Task/Job: Scheduled Task
- T1547.001 — Registry Run Keys / Startup Folder
- T1543 — Create or Modify System Process

## 4. Data Sources

- Sysmon
- Windows Security Logs
- Task Scheduler Logs
- Windows Registry Events
- Wazuh

## 5. Investigation

Look for:

- New scheduled tasks
- Suspicious startup entries
- Registry modifications
- Unexpected services
- Unusual parent/child process relationships

## 6. Findings

Document suspicious activity discovered during the hunt.

## 7. Evidence

Add screenshots and relevant event information.

## 8. Timeline

Document:

| Time | Event | Host | User | Evidence |
|---|---|---|---|---|
| TBD | TBD | TBD | TBD | TBD |

## 9. Conclusion

Determine whether the hypothesis was confirmed.

## 10. Detection Improvement

Document new or improved Sigma/Wazuh detections.
