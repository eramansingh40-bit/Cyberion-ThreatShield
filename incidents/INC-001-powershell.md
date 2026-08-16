# INC-001 — Suspicious PowerShell Execution

## Incident Summary

| Field            | Value                           |
| ---------------- | ------------------------------- |
| Incident ID      | INC-001                         |
| Severity         | High                            |
| Status           | Closed                          |
| Detection        | Suspicious PowerShell           |
| MITRE Technique  | T1059.001 — PowerShell          |
| Host             | DESKTOP-4OHMOT5                 |
| User             | DESKTOP-4OHMOT5\const           |
| Wazuh Agent IP   | 192.168.224.1                   |
| Wazuh Rule ID    | 100201                          |
| Wazuh Rule Level | 12                              |
| Date/Time        | Aug 16, 2026 @ 19:22:03.133 IST |

## 1. Initial Alert

Wazuh generated a **High-severity alert (Level 12)** with Rule ID `100201`:

**Suspicious PowerShell Execution detected**

The detection was triggered by **Sysmon Event ID 1 — Process Create**. The event identified the execution of `powershell.exe` with a command that uses PowerShell's Base64 decoding function:

```text
"C:\WINDOWS\System32\WindowsPowerShell\v1.0\powershell.exe" -Command [Convert]::FromBase64String('V2F6dWhUZXN0')
```

The Base64 value:

```text
V2F6dWhUZXN0
```

decodes to:

```text
WazuhTest
```

The activity was mapped by Wazuh to **MITRE ATT&CK T1059.001 — Command and Scripting Interpreter: PowerShell**.

## 2. Investigation

### PowerShell command line

Observed command:

```text
"C:\WINDOWS\System32\WindowsPowerShell\v1.0\powershell.exe" -Command [Convert]::FromBase64String('V2F6dWhUZXN0')
```

The command contains Base64-encoded content. The decoded value is `WazuhTest`, indicating that the observed activity was consistent with a controlled Wazuh detection test rather than an identified malicious payload.

### Parent process

Parent process:

```text
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
```

Parent Process ID:

```text
10276
```

Parent User:

```text
DESKTOP-4OHMOT5\const
```

### Child process

The observed process was:

```text
powershell.exe
```

Process ID:

```text
23812
```

The supplied event does not provide evidence of an additional malicious child process.

### User account

Observed user:

```text
DESKTOP-4OHMOT5\const
```

Logon ID:

```text
0x3115B
```

Terminal Session ID:

```text
1
```

Integrity Level:

```text
High
```

### Source/Destination IP

Wazuh reported the agent IP:

```text
192.168.224.1
```

No source or destination network IP was recorded in the supplied Sysmon Event ID 1.

Therefore, `192.168.224.1` should be treated as the **Wazuh agent IP**, not as confirmed attacker/source IP evidence.

### File activity

The executed binary was:

```text
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
```

No malicious file creation, modification, or download was identified in the supplied event.

The recorded SHA256 was:

```text
7600FFE12DA441FE89D035B13801E8E91D064BC544A27B19A5CF49F6AB8B18F5
```

This hash corresponds to the observed `powershell.exe` image and should not be treated as a malicious-file IOC without additional validation.

### Persistence mechanisms

No persistence mechanism was identified in the supplied telemetry.

There was no evidence of:

* Scheduled task creation
* Registry Run key modification
* Windows service creation
* Startup-folder modification
* WMI persistence
* Other persistence activity

### Related events

The detection was associated with:

* Sysmon Event ID 1 — Process Create
* Wazuh Rule ID `100201`
* MITRE ATT&CK `T1059.001`
* Rule description: `Suspicious PowerShell Execution detected`
* Rule fired count: `3`

The supplied evidence does not establish additional malicious activity beyond the PowerShell execution.

## 3. Timeline

| Time                            | Event                                      | Evidence           |
| ------------------------------- | ------------------------------------------ | ------------------ |
| Aug 16, 2026 @ 19:22:02.322 IST | PowerShell process executed                | Sysmon Event ID 1  |
| Aug 16, 2026 @ 19:22:02.322 IST | Base64 decoding command observed           | Sysmon CommandLine |
| Aug 16, 2026 @ 19:22:03.133 IST | Wazuh generated High-severity alert        | Wazuh Rule 100201  |
| Aug 16, 2026 @ 19:22:03.133 IST | `Suspicious PowerShell Execution detected` | Wazuh              |

**Observed command:**

```text
powershell.exe -Command [Convert]::FromBase64String('V2F6dWhUZXN0')
```

**Decoded value:**

```text
WazuhTest
```

## 4. Indicators of Compromise

* **IP address:** `192.168.224.1` — Wazuh agent IP; not confirmed as attacker/source IP
* **Domains:** None observed
* **File hash:** `SHA256: 7600FFE12DA441FE89D035B13801E8E91D064BC544A27B19A5CF49F6AB8B18F5`
* **File path:** `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe`
* **Process:** `powershell.exe`
* **Process ID:** `23812`
* **Parent Process ID:** `10276`
* **User:** `DESKTOP-4OHMOT5\const`
* **Logon ID:** `0x3115B`

> The PowerShell executable hash is included as an investigation artifact. It is not considered a confirmed malicious IOC based solely on this alert.

## 5. MITRE ATT&CK

Observed technique:

* **T1059.001 — Command and Scripting Interpreter: PowerShell**
* **Tactic:** Execution

The alert was explicitly mapped by Wazuh to:

```text
T1059.001
```

## 6. Impact Assessment

The affected endpoint was:

```text
DESKTOP-4OHMOT5
```

The affected user context was:

```text
DESKTOP-4OHMOT5\const
```

Based on the supplied telemetry:

* No confirmed compromise was identified.
* No malicious file was identified.
* No persistence mechanism was identified.
* No network connection to a malicious destination was identified.
* No credential theft was observed.
* No lateral movement was observed.
* No data exfiltration was observed.

The observed activity was limited to PowerShell execution and Base64 decoding of the test string `WazuhTest`.

## 7. Containment

Because the activity was identified as a controlled Wazuh/Sysmon detection test, no emergency endpoint isolation was required.

The alert was reviewed in Wazuh and the associated PowerShell process, user, command line, parent process, and Sysmon event were investigated.

## 8. Eradication

No malicious files, persistence mechanisms, compromised accounts, or unauthorized processes were identified from the supplied telemetry.

Therefore:

* No malware removal was required.
* No persistence mechanism required removal.
* No user account was disabled.
* No credential reset was required based on this evidence.

## 9. Recovery

The endpoint was reviewed after the alert.

Wazuh/Sysmon telemetry confirmed that the suspicious PowerShell execution was captured successfully by the detection rule.

The detection pipeline was validated through:

```text
PowerShell execution
        ↓
Sysmon Event ID 1
        ↓
Wazuh EventChannel ingestion
        ↓
Custom Rule 100201
        ↓
High-severity alert
```

No additional malicious activity was identified in the supplied evidence.

## 10. Root Cause

The root cause was a **controlled SOC/Wazuh detection test** designed to validate detection of suspicious PowerShell activity.

The PowerShell command used:

```text
[Convert]::FromBase64String('V2F6dWhUZXN0')
```

The Base64 value decodes to:

```text
WazuhTest
```

This activity triggered the custom Wazuh rule:

```text
Rule ID: 100201
Description: Suspicious PowerShell Execution detected
Level: 12
MITRE: T1059.001
```

The test successfully demonstrated that Sysmon PowerShell telemetry was being collected by Wazuh and matched against the custom detection rule.

## 11. Lessons Learned

* Continue monitoring PowerShell process creation through Sysmon.
* Maintain detection for encoded or obfuscated PowerShell commands.
* Correlate PowerShell alerts with parent/child processes.
* Correlate PowerShell activity with network connections and file creation events.
* Correlate PowerShell alerts with authentication events where relevant.
* Distinguish controlled security-testing activity from confirmed malicious activity.
* Avoid treating the hash of a legitimate Windows system executable as a malicious IOC without validation.
* Improve the detection by correlating suspicious PowerShell execution with additional behaviors such as download, execution, persistence, or credential-access activity.

## 12. Final Verdict

* [x] True Positive
* [ ] False Positive
* [ ] Benign Activity

**Final conclusion:** **True Positive — Controlled Detection Test.**

Wazuh correctly detected the execution of PowerShell containing Base64-decoding behavior and generated a Level 12 alert under MITRE ATT&CK **T1059.001 — PowerShell**.

The alert is a true positive for the **detection behavior**, but the supplied evidence does **not indicate an actual malicious compromise**. The decoded payload was `WazuhTest`, confirming that the activity was a controlled SOC/Wazuh testing exercise.

No confirmed malicious file, persistence mechanism, credential compromise, lateral movement, or data exfiltration was identified.

