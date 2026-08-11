# Threat Hunt 002 — Windows Discovery Activity

## 1. Objective

Identify commands associated with system, account, process, and network discovery.

## 2. Hypothesis

An attacker may perform discovery activities after gaining access to a Windows endpoint.

## 3. MITRE ATT&CK

Potential techniques:

- T1057 — Process Discovery
- T1087 — Account Discovery
- T1016 — System Network Configuration Discovery
- T1049 — System Network Connections Discovery

## 4. Data Sources

- Sysmon
- Windows Security Logs
- Wazuh

## 5. Investigation

Look for commands such as:

- whoami
- tasklist
- systeminfo
- ipconfig
- net user
- net group
- arp
- netstat

## 6. Findings

Document the events identified during the hunt.

## 7. Evidence

Add screenshots and relevant log/event information.

## 8. Conclusion

Determine whether the hypothesis was confirmed.

## 9. Detection Improvement

Document any new or modified detection rules.
