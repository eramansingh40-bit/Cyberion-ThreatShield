# INC-001 — Suspicious PowerShell Execution

## Incident Summary

| Field | Value |
|---|---|
| Incident ID | INC-001 |
| Severity | High |
| Status | Closed |
| Detection | Suspicious PowerShell |
| MITRE Technique | T1059.001 — PowerShell |
| Host | amandeep-virtual-machine |
| User | amandeep |
| Date/Time |  |

## 1. Initial Alert

Describe the Wazuh alert that triggered the investigation.

## 2. Investigation

Investigate:

- PowerShell command line
- Parent process
- Child processes
- User account
- Source/destination IP
- File activity
- Persistence mechanisms
- Related events

## 3. Timeline

| Time | Event | Evidence |
|---|---|---|
| Timestamp | PowerShell executed | Wazuh/Sysmon |
| Aug 16, 2026 @ 17:47:13.735 - |$cmd = 'Write-Output "Wazuh PowerShell Detection Test"'
$enc = [Convert]::ToBase64String([Text.Encoding]::Unicode.GetBytes($cmd))
powershell.exe -EncodedCommand $enc  powershell.exe -Command "IEX 'Write-Output WazuhTest'" | Suspicious PowerShell Execution detected |

## 4. Indicators of Compromise

- IP addresses: 192.168.224.1
- Domains: 
- File hashes: SHA256:
7600FFE12DA441FE89D035B13801E8E91D064BC544A27B19A5CF49F6AB8B18F5
- File paths: C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
- Processes: powershell.exe

## 5. MITRE ATT&CK

- T1059.001 — PowerShell

## 6. Impact Assessment

Document the affected endpoint, account, files, or services.

## 7. Containment

Document actions taken to contain the incident.

## 8. Eradication

Document malicious files, processes, persistence mechanisms, or accounts removed.

## 9. Recovery

Document system restoration and validation.

## 10. Root Cause

Document how the activity occurred.

## 11. Lessons Learned

Document improvements required for future detection.

## 12. Final Verdict

- [ ] True Positive
- [ ] False Positive
- [ ] Benign Activity

Final conclusion: TBD
