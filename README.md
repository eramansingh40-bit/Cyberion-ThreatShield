# Cyberion ThreatShield

## SOC Detection Engineering, Threat Hunting & Incident Investigation

Cyberion ThreatShield is an end-to-end Security Operations Center (SOC) detection engineering and threat hunting project designed to demonstrate the practical detection, investigation, and response capabilities required in a modern SOC environment.

The project uses **Wazuh, Windows Security Logs, Sysmon, Sigma detection rules, and MITRE ATT&CK** to build a repeatable workflow for identifying, investigating, and responding to suspicious activity.

---

## 🎯 Project Objectives

The main objectives of Cyberion ThreatShield are to:

* Build a practical SOC monitoring environment.
* Collect and analyze Windows security telemetry.
* Develop Sigma detection rules.
* Implement custom Wazuh detection rules.
* Map detections to MITRE ATT&CK techniques.
* Perform controlled attack simulations.
* Conduct hypothesis-driven threat hunts.
* Investigate security incidents.
* Develop incident-response playbooks.
* Measure detection coverage and identify detection gaps.
* Document findings using evidence-based investigation reports.

---

## 🏗️ Architecture

The project uses Wazuh as the central security monitoring platform.

```text
                         Attack Simulation
                              │
                              ▼
                         Kali Linux
                              │
                              ▼
                      Windows Endpoint
                       ┌──────┴──────┐
                       │             │
                    Windows       Sysmon
                    Events         Logs
                       │             │
                       └──────┬──────┘
                              │
                              ▼
                        Wazuh Agent
                              │
                              ▼
                        Wazuh Manager
                              │
                    ┌─────────┴─────────┐
                    │                   │
              Detection Engine    Security Analysis
                    │                   │
                    ▼                   ▼
              Wazuh Alerts       Threat Hunting
                    │                   │
                    └─────────┬─────────┘
                              ▼
                     Incident Investigation
                              │
                              ▼
                     Incident Response
```

![Wazuh Architecture](architecture/wazuh.jpeg)

---

## 🛠️ Technologies Used

| Technology   | Purpose                             |
| ------------ | ----------------------------------- |
| Wazuh        | SIEM/XDR and security monitoring    |
| Windows      | Endpoint telemetry                  |
| Sysmon       | Detailed Windows system telemetry   |
| Sigma        | Detection rule development          |
| MITRE ATT&CK | Threat technique mapping            |
| Kali Linux   | Controlled attack simulation        |
| GitHub       | Detection library and documentation |

---

# 🔍 Detection Engineering

The project contains Sigma detection rules designed to identify suspicious activity on Windows endpoints.

### Current detections

| Detection             | MITRE ATT&CK      | Purpose                               |
| --------------------- | ----------------- | ------------------------------------- |
| Suspicious PowerShell | T1059.001         | Detect suspicious PowerShell activity |
| Encoded PowerShell    | T1059.001         | Detect encoded PowerShell commands    |
| Scheduled Task        | T1053.005         | Detect scheduled-task creation        |
| Discovery Commands    | T1057/T1087/T1016 | Detect Windows discovery activity     |

Detection rules are stored in:

```text
detections/sigma/
```

Wazuh-specific rules are stored in:

```text
detections/wazuh/
```

---

# 🕵️ Threat Hunting

Cyberion ThreatShield uses a hypothesis-driven threat hunting methodology.

The hunting process is:

```text
Hypothesis
    ↓
Required Telemetry
    ↓
Log Investigation
    ↓
Suspicious Activity
    ↓
Evidence Collection
    ↓
Analysis
    ↓
Conclusion
    ↓
Detection Improvement
```

### Threat Hunts

* **Hunt 001 — Suspicious PowerShell**
* **Hunt 002 — Windows Discovery Activity**
* **Hunt 003 — Persistence Activity**

Hunt documentation is available in:

```text
threat-hunts/
```

---

# 🚨 Incident Investigation

Security incidents generated during controlled testing are documented using a repeatable investigation process.

```text
Alert
 ↓
Triage
 ↓
Validation
 ↓
Evidence Collection
 ↓
Timeline Analysis
 ↓
MITRE Mapping
 ↓
Impact Assessment
 ↓
Containment
 ↓
Eradication
 ↓
Recovery
 ↓
Lessons Learned
```

### Current incidents

* **INC-001 — Suspicious PowerShell Execution**
* **INC-002 — Suspicious Login Activity**

Incident reports are stored in:

```text
incidents/
```

---

# 🛡️ Incident Response Playbooks

The project contains repeatable response procedures for common SOC incidents.

### Available Playbooks

* PowerShell Incident Response
* Malware Detection Response
* Compromised Account Response

Playbooks are stored in:

```text
playbooks/
```

Each playbook follows:

```text
Detection
   ↓
Triage
   ↓
Investigation
   ↓
Containment
   ↓
Eradication
   ↓
Recovery
   ↓
Lessons Learned
```

---

# 🎯 MITRE ATT&CK Detection Coverage

Detections are mapped to MITRE ATT&CK techniques to measure security monitoring coverage.

Example coverage:

| Technique | Name                                   | Detection |
| --------- | -------------------------------------- | --------- |
| T1059.001 | PowerShell                             | ✅         |
| T1053.005 | Scheduled Task                         | ✅         |
| T1057     | Process Discovery                      | ✅         |
| T1087     | Account Discovery                      | ✅         |
| T1016     | System Network Configuration Discovery | ✅         |
| T1046     | Network Service Scanning               | ⚠️        |
| T1078     | Valid Accounts                         | ⚠️        |
| T1003     | OS Credential Dumping                  | ⚠️        |

Detailed coverage assessment:

```text
mitre/detection-coverage.md
```

> Coverage status is updated after each detection is tested against actual lab telemetry.

---

# 📸 Evidence

Evidence collected from the SOC lab is stored in:

```text
evidence/
```

Examples include:

* Wazuh agent connectivity
* Detection alerts
* Security event investigation
* Sysmon telemetry
* Incident investigation evidence

---

# 📊 Wazuh Dashboard

Dashboard screenshots and SOC monitoring views are stored in:

```text
dashboards/
```

Example:

![Wazuh Dashboard](dashboards/wazuh-dashboard.png)

---

# 📁 Project Structure

```text
Cyberion-ThreatShield/
│
├── README.md
│
├── architecture/
│   └── wazuh.jpeg
│
├── detections/
│   ├── sigma/
│   │   ├── suspicious_powershell.yml
│   │   ├── encoded_powershell.yml
│   │   ├── scheduled_task.yml
│   │   └── discovery_commands.yml
│   │
│   └── wazuh/
│       └── custom_rules.xml
│
├── threat-hunts/
│   ├── hunt-001-powershell.md
│   ├── hunt-002-discovery.md
│   └── hunt-003-persistence.md
│
├── incidents/
│   ├── INC-001-powershell.md
│   └── INC-002-suspicious-login.md
│
├── playbooks/
│   ├── powershell.md
│   ├── malware.md
│   └── compromised-account.md
│
├── mitre/
│   └── detection-coverage.md
│
├── evidence/
│   ├── wazuh-agent.png
│   ├── detection-alert.png
│   └── investigation.png
│
├── dashboards/
│   └── wazuh-dashboard.png
│
└── reports/
    └── final-report.md
```

---

# 🔬 Detection Engineering Methodology

Cyberion ThreatShield follows a continuous detection engineering lifecycle:

```text
Attack Simulation
       ↓
Telemetry Collection
       ↓
Detection Development
       ↓
Detection Testing
       ↓
Alert Generation
       ↓
Threat Hunting
       ↓
Incident Investigation
       ↓
Detection Gap Analysis
       ↓
Detection Improvement
       ↓
Retesting
```

This methodology allows detections to be continuously validated and improved.

---

# 📈 Project Results

The following metrics will be updated as the lab is completed:

| Metric                     | Result |
| -------------------------- | -----: |
| Sigma detections           |     4+ |
| Wazuh custom rules         |    TBD |
| Threat hunts               |     3+ |
| Incident investigations    |     2+ |
| Response playbooks         |     3+ |
| MITRE ATT&CK techniques    |    TBD |
| Successful detection tests |    TBD |
| Detection gaps identified  |    TBD |

---

# 🧪 Testing Methodology

All attack simulations are performed in an isolated laboratory environment.

Testing involves generating controlled security telemetry and verifying whether:

1. Windows generates the expected event.
2. Sysmon records the activity.
3. Wazuh receives the telemetry.
4. The detection rule identifies the activity.
5. Wazuh generates an alert.
6. The alert can be investigated.
7. Evidence can be collected.
8. The activity can be mapped to MITRE ATT&CK.
9. Detection gaps can be identified and improved.

---

# 📚 Documentation

| Document                | Location            |
| ----------------------- | ------------------- |
| Sigma detections        | `detections/sigma/` |
| Wazuh rules             | `detections/wazuh/` |
| Threat hunts            | `threat-hunts/`     |
| Incident investigations | `incidents/`        |
| Response playbooks      | `playbooks/`        |
| MITRE coverage          | `mitre/`            |
| Evidence                | `evidence/`         |
| Dashboards              | `dashboards/`       |
| Final report            | `reports/`          |

---

# ⚠️ Disclaimer

This project is intended for **authorized security research, SOC training, detection engineering, and educational purposes**.

All security testing and attack simulations should be performed only against systems and environments that you own or have explicit authorization to test.

---

# 👤 Project Focus

**Cyberion ThreatShield** demonstrates practical experience in:

* SOC Operations
* SIEM Monitoring
* Wazuh
* Windows Security Monitoring
* Sysmon
* Detection Engineering
* Sigma
* Threat Hunting
* Incident Investigation
* Incident Response
* MITRE ATT&CK
* Security Log Analysis
* Detection Coverage Assessment
* Security Documentation

```

This README gives your repository a **professional SOC-project structure**. As you actually complete the lab, replace every `TBD` with your real results and evidence rather than leaving simulated results in the final version.
```



