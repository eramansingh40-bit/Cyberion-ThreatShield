# PowerShell Incident Response Playbook

## Objective

Provide a repeatable procedure for investigating suspicious PowerShell activity.

## 1. Detection

Review the Wazuh alert.

## 2. Triage

Collect:

- Hostname
- Username
- Timestamp
- PowerShell command
- Parent process
- Source IP
- Destination IP

## 3. Investigation

Review Sysmon and Windows events.

Determine:

- What executed?
- Who executed it?
- Which process spawned PowerShell?
- What files were created?
- Was network communication performed?
- Was persistence established?

## 4. Containment

If malicious activity is confirmed:

- Isolate the endpoint
- Disable compromised accounts if necessary
- Block confirmed malicious indicators

## 5. Eradication

- Terminate malicious processes
- Remove malicious files
- Remove persistence
- Reset compromised credentials

## 6. Recovery

- Restore normal connectivity
- Verify endpoint health
- Monitor for recurring activity

## 7. Documentation

Record:

- Timeline
- Evidence
- IOCs
- MITRE techniques
- Root cause
- Lessons learned
