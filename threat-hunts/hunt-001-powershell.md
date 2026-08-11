# Threat Hunt 001 — Suspicious PowerShell Activity

## 1. Objective

Identify suspicious PowerShell activity on Windows endpoints.

## 2. Hypothesis

An attacker may use PowerShell to execute commands or scripts on a compromised Windows endpoint.

## 3. MITRE ATT&CK

- Technique: T1059.001
- Name: PowerShell
- Tactic: Execution

## 4. Data Sources

- Windows Security Logs
- Sysmon
- PowerShell Operational Logs
- Wazuh

## 5. Investigation

Search for:

- powershell.exe
- encoded commands
- Invoke-Expression
- DownloadString
- suspicious parent processes

## 6. Findings

Document the suspicious events discovered during the hunt.

## 7. Evidence

Add screenshots or references to evidence collected during the investigation.

## 8. Conclusion

State whether the hypothesis was confirmed or not.

## 9. Detection Improvement

Document any new Sigma or Wazuh detection created as a result of this hunt.
