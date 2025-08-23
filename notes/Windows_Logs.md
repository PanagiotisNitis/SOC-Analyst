# Room: Windows Logs
## Introduction
Windows Event Logs capture system, security, and application events.
For SOC Analysts, they are crucial for detecting intrusions, investigating incidents, and monitoring system activity.

Logs can be accessed via:

- Event Viewer (eventvwr.msc)
- PowerShell (Get-WinEvent, Get-EventLog)
- SIEM tools (Splunk, ELK, Sentinel, etc.)

---

| Log Category         | Location                                       | Description                                   |
| -------------------- | ---------------------------------------------- | --------------------------------------------- |
| **System**           | Event Viewer → Windows Logs → System           | OS & hardware events                          |
| **Application**      | Event Viewer → Windows Logs → Application      | Application-related logs                      |
| **Security**         | Event Viewer → Windows Logs → Security         | Authentication, access attempts, audit events |
| **Setup**            | Event Viewer → Windows Logs → Setup            | Windows installation/setup logs               |
| **Forwarded Events** | Event Viewer → Windows Logs → Forwarded Events | Logs from other systems                       |

---

## Important Event IDs (Security Logs)
| Event ID | Description                              |
| -------- | ---------------------------------------- |
| **4624** | Successful login                         |
| **4625** | Failed login                             |
| **4634** | Logoff                                   |
| **4648** | Logon with explicit credentials          |
| **4672** | Special privileges assigned to new logon |
| **4688** | Process creation                         |
| **4689** | Process termination                      |
| **4720** | User account created                     |
| **4726** | User account deleted                     |
| **4732** | User added to security group             |
| **1102** | Audit log cleared                        |

---

## Viewing Logs
- Event Viewer:
    - Run → eventvwr.msc → Navigate to logs
- PowerShell Examples:
Get-EventLog -LogName Security -Newest 20
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625} | Format-List
- Command Prompt:
wevtutil qe Security /c:10 /rd:true /f:text

---

## Useful Examples for SOC
- Detect brute-force login attempts:
  Check multiple 4625 (failed logons) in short time.
- Detect privilege escalation:
  Look for 4672 events.
- Investigate lateral movement:
  Look at 4648 (logon with explicit credentials).
- Detect persistence:
  Monitor for 4720 (user created) or 4732 (group membership changes)
- Detect suspicious processes:
  Track 4688 (process creation) events.

---

## Tools for Windows Log Analysis
- Sysinternals Suite (Sysmon, Autoruns, Process Explorer)
- Sysmon (System Monitor): provides enhanced logging (process creation, network connections, registry changes)
- Splunk / ELK / Azure Sentinel for log aggregation & detection.

---

## Conclusion
Windows Event Logs are a goldmine for SOC analysts.
They enable:
- Threat detection(brute force, privilege escalation, persistence)
- Incident response (timeline analysis,atacker TTPs)
