# MITRE ATT&CK Detection Coverage

## Objective

The objective of this assessment is to evaluate the current detection coverage of the **Cyberion-ThreatShield** SOC project against selected MITRE ATT&CK techniques using Wazuh endpoint telemetry, Sysmon events, Linux authentication logs, and custom detection rules.

The assessment is based on events observed in the Wazuh Dashboard on **August 16, 2026**.

---# 1. Observed Wazuh Detection Activity

The Wazuh Dashboard showed several security-relevant events during the investigation period.

### PowerShell Activity

Multiple PowerShell detections were observed:

* `Suspicious PowerShell Execution detected`
* `Powershell.exe spawned a powershell process which executed a base64 encoded command`
* `Powershell was used to delete files or directories`
* PowerShell launched `SecEdit.exe`

The custom Wazuh rule generated:

```text
Rule ID: 100201
Level: 12
MITRE: T1059.001
Technique: PowerShell
Tactic: Execution
```

This provides strong evidence that **T1059.001 — PowerShell** is currently implemented.

---

# 3. T1059.001 — PowerShell

### Evidence

Observed events included:

```text
18:21:50 — Suspicious PowerShell Execution detected
18:21:56 — Suspicious PowerShell Execution detected
18:22:03 — Suspicious PowerShell Execution detected
```

The investigated Sysmon Event ID 1 contained:

```text
Image:
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe

CommandLine:
powershell.exe -Command "IEX 'Write-Output WazuhTest'"

Hash:
SHA256=7600FFE12DA441FE89D035B13801E8E91D064BC544A27B19A5CF49F6AB8B18F5
```

The event was mapped to:

```text
T1059.001 — PowerShell
```

### Assessment

**Status: Fully Implemented ✅**

The project has:

* Sysmon process telemetry
* Custom Wazuh detection
* MITRE mapping
* Threat hunting capability
* Investigation evidence
* Incident documentation

---

# 4. T1053.005 — Scheduled Task

### Evidence

The following Wazuh event was observed:

```text
18:14:01 — Suspicious Scheduled Task Creation detected:
schtasks.exe /create
```

This confirms that scheduled-task creation was successfully detected by the Wazuh custom rule.

### Assessment

**Status: Detection implemented ✅**

The current limitation is that a dedicated response playbook has not yet been documented.

Therefore:

```text
Detection: ✅
Wazuh Alert: ✅
Hunt: ✅
Playbook: ❌
```

---

# 5. Discovery Activity

Several discovery events were observed:

```text
18:12:35 — Discovery activity executed
18:12:35 — Discovery activity executed
18:12:35 — Discovery activity executed
18:12:35 — Discovery activity executed
```

The project currently contains detection coverage for selected Windows discovery commands.

These detections can be mapped to:

### T1057 — Process Discovery

Process enumeration commands can provide visibility into running processes.

**Assessment: Partially/fully implemented depending on the exact command telemetry.**

For the coverage matrix, the current implementation is recorded as:

```text
Detection: ✅
Wazuh Alert: ✅
Hunt: ✅
Playbook: ❌
```

### T1087 — Account Discovery

Account enumeration activity can indicate attempts to identify local or domain accounts.

Current project coverage:

```text
Detection: ✅
Wazuh Alert: ✅
Hunt: ✅
Playbook: ❌
```

### T1016 — System Network Configuration Discovery

Network configuration discovery can include commands such as:

```text
ipconfig
ipconfig /all
route print
```

The project's discovery detection capability provides coverage for this class of activity.

Current status:

```text
Detection: ✅
Wazuh Alert: ✅
Hunt: ✅
Playbook: ❌
```

---

# 6. T1046 — Network Service Scanning

### Current evidence

The supplied Wazuh event list does not contain sufficient evidence of actual network service scanning.

Although discovery detection exists, the observed events do not demonstrate that a tool such as a network scanner performed service enumeration.

### Assessment

**Status: Partially Implemented ⚠️**

Current limitations:

* Limited network telemetry
* No dedicated network-service-scanning rule
* No dedicated hunt
* No response playbook

### Planned improvement

Integrate additional network telemetry from:

* Windows Firewall
* Sysmon network connection events
* Zeek
* Suricata
* Snort

Then create dedicated detection logic for suspicious scanning behavior.

---

# 7. T1078 — Valid Accounts

### Observed authentication activity

The Wazuh Dashboard showed:

```text
PAM: Login session opened
Successful sudo to ROOT executed
PAM: Login session closed
```

These events demonstrate successful authentication and privilege elevation activity.

However, they **do not by themselves prove T1078 — Valid Accounts**.

A successful `sudo` operation can be completely legitimate.

### Assessment

**Status: Partially Implemented ⚠️**

Current telemetry provides authentication visibility, but additional context is required to confidently identify the use of compromised or abused valid credentials.

Required improvements include:

* Correlation of authentication events
* Source IP analysis
* Account behavior analysis
* Unusual login-time detection
* Multiple failed-to-successful login correlation
* Windows Event ID 4624/4625 monitoring

---

# 8. T1003 — OS Credential Dumping

### Current evidence

No confirmed credential-dumping event appears in the supplied Wazuh event list.

Events such as PowerShell activity and `SecEdit.exe` execution should not automatically be classified as credential dumping.

### Assessment

**Status: Partially Implemented ⚠️**

The project currently lacks sufficient endpoint telemetry and dedicated rules for detecting credential-dumping techniques.

### Planned improvements

Add monitoring for:

* LSASS access
* Credential-dumping process behavior
* Suspicious handle access
* Security tool alerts
* Sysmon process-access telemetry
* Windows Security events

---

# 9. Additional Security Events Observed

The investigation also identified several events that are useful for threat hunting but should not automatically be classified as malicious.

### PowerShell → SecEdit.exe

Multiple events reported:

```text
C:\Windows\SysWOW64\SecEdit.exe
```

launched by:

```text
C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
```

`SecEdit.exe` is a legitimate Windows binary.

Therefore, this event should be investigated based on:

* Command line
* Parent process
* User
* Hash
* Integrity level
* Security configuration being modified

It should not automatically be classified as malware.

---

### Service Startup Type Changes

The following events were observed:

```text
19:51:30 — Service startup type was changed
19:49:08 — Service startup type was changed
```

These are potentially interesting persistence/configuration events.

However, additional event details are required before assigning a specific MITRE technique.

Recommended investigation fields:

```text
Service name
Service path
Previous startup type
New startup type
User
Process
Command line
Timestamp
```

---

### Software Protection Service

Multiple events reported:

```text
Software protection service scheduled successfully.
```

These appear to represent normal Windows/software-protection activity unless additional context indicates otherwise.

They should therefore be treated as **informational/low-confidence events** rather than automatically escalated as incidents.

---

# 10. Detection Timeline

The observed activity can be summarized chronologically:

```text
18:10–18:11
Linux authentication/session activity
        ↓
18:12
PowerShell file deletion activity
        ↓
18:12
PowerShell → SecEdit.exe activity
        ↓
18:12
Discovery activity
        ↓
18:14
Suspicious Scheduled Task Creation
        ↓
18:17–18:23
Repeated authentication/sudo activity
        ↓
18:26
Encoded PowerShell activity
        ↓
19:21
Encoded PowerShell / suspicious PowerShell activity
        ↓
19:22
Additional suspicious PowerShell alerts
        ↓
19:51
Service startup type changes
        ↓
19:52
PowerShell spawned PowerShell instance
        ↓
19:53
Software Protection service activity
        ↓
19:54
Application Compatibility Database launched
```

This timeline demonstrates that the Wazuh deployment is collecting telemetry from multiple security-relevant sources and successfully generating alerts for several custom detections.

---

# 11. Detection Coverage Findings

The current assessment identifies three major strengths.

### Strength 1 — PowerShell Detection

The strongest detection coverage is:

```text
T1059.001
PowerShell
```

The project successfully demonstrates:

```text
Telemetry
   ↓
Sysmon Event ID 1
   ↓
Wazuh Agent
   ↓
Custom Rule 100201
   ↓
Level 12 Alert
   ↓
MITRE T1059.001
   ↓
Threat Hunting
   ↓
Investigation
```

### Strength 2 — Scheduled Task Detection

The project successfully detects:

```text
schtasks.exe /create
```

and maps the activity to:

```text
T1053.005
```

### Strength 3 — Discovery Detection

Multiple discovery events were successfully observed in the Wazuh Dashboard, demonstrating that endpoint telemetry can be used for hypothesis-driven threat hunting.

---

# 12. Detection Gaps

## Gap 1 — T1046 Network Service Scanning

### Issue

The current deployment does not provide sufficient network telemetry to confidently identify network-service scanning.

### Improvement

Add:

* Network connection telemetry
* IDS/NSM telemetry
* Zeek
* Suricata/Snort
* Windows Firewall logging

Then create dedicated Wazuh detection rules.

---

## Gap 2 — T1003 OS Credential Dumping

### Issue

The current telemetry does not provide sufficient evidence for reliable credential-dumping detection.

### Improvement

Enable additional Sysmon and Windows security telemetry focused on:

* LSASS access
* Process access
* Suspicious credential-related processes
* Security event correlation

---

## Gap 3 — Incident Response Playbooks

Several techniques have detection and hunting coverage but lack documented response playbooks.

For example:

```text
T1053.005
Scheduled Task
```

Currently:

```text
Detection: ✅
Alert: ✅
Hunt: ✅
Playbook: ❌
```

A playbook should document:

1. Validate the alert.
2. Identify the task name.
3. Identify the creator.
4. Examine the task action.
5. Determine persistence impact.
6. Disable/remove malicious tasks if confirmed.
7. Investigate related processes.
8. Document evidence.
9. Close or escalate the incident.

---

# 13. Improvement Plan

The following roadmap will improve detection maturity:

1. Identify detection gaps.
2. Determine required endpoint and network telemetry.
3. Develop Sigma detection rules.
4. Convert validated detections into Wazuh rules.
5. Generate controlled lab activity.
6. Validate Wazuh alerts.
7. Perform threat hunting.
8. Map confirmed behavior to MITRE ATT&CK.
9. Create incident-response playbooks.
10. Capture investigation evidence.
11. Document false positives.
12. Update the detection coverage matrix.

---

# 14. Overall Assessment

The Cyberion-ThreatShield project currently demonstrates **strong endpoint-based detection capability for PowerShell, scheduled-task creation, and selected discovery activities**.

The strongest evidence is the successful generation of Wazuh alerts for:

```text
T1059.001 — PowerShell
T1053.005 — Scheduled Task
```

and the observed discovery activity.

However, the current telemetry is insufficient to claim full coverage for:

```text
T1046 — Network Service Scanning
T1003 — OS Credential Dumping
T1078 — Valid Accounts
```

These techniques should remain **partial coverage** until additional telemetry and dedicated detection logic are implemented.

The next maturity step is to move from **detection-only coverage** toward complete:

```text
Telemetry
   ↓
Detection
   ↓
Alert
   ↓
Threat Hunt
   ↓
Investigation
   ↓
MITRE Mapping
   ↓
Response Playbook
   ↓
Evidence
   ↓
Coverage Measurement
```

This establishes a repeatable SOC detection-engineering and incident-response workflow for the Cyberion-ThreatShield project.
