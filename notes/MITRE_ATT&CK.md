# MITRE ATT&CK Framework
## Introduction
MITRE ATT&CK (Adversarial Tactics, Techniques & Common Knowledge) is a globally recognized knowledge base of adversary behaviors.
It is used by SOC analysts, red teamers, and incident responders to:
- Understand attacker tactics and techniques
- Map detections to adversary behavior
- Improve threat hunting and defense strategies

---

## Structure of MITRE ATT&CK
- Tactics: The "why" - adversary goals (e.g, Initial Access, Execution)
- Techniques: The "how" - specific methods used (e.g., Spearphishing, Credential Dumping)
- Sub-techniques: More granular detail within a technique
- Mitigations: Defensive measures to prevent or detect the activity
- Detections: Suggested log sources and analysis to identify activity

---

## ATT&CK Tactics Overview
| Tactic                 | Description                                         |
| ---------------------- | --------------------------------------------------- |
| Initial Access         | How attackers enter the system (phishing, exploits) |
| Execution              | Running malicious code                              |
| Persistence            | Maintaining access                                  |
| Privilege Escalation   | Gaining higher-level permissions                    |
| Defense Evasion        | Avoiding detection                                  |
| Credential Access      | Stealing passwords/keys                             |
| Discovery              | Understanding the environment                       |
| Lateral Movement       | Moving through the network                          |
| Collection             | Gathering sensitive data                            |
| Command & Control (C2) | Communicating with attacker systems                 |
| Exfiltration           | Stealing data                                       |
| Impact                 | Destroying or encrypting systems/data               |

---

## Example techniques (with Detection Ideas)
- T1059 - Command and Scripting Interpreter (Execution):
Detect unusual PowerShell, Python, or Bash activity
Splunk Example:
index=wineventlog EventCode=4688
| search New_Process_Name="*powershell.exe*" OR New_Process_Name="*cmd.exe*"
- T1078 - Valid Accounts (Persistence):
  Look for new accounts or unusual logins
- T1003 - Credential Dumping (Credential Access):
  Detect access to LSASS or Mimikatz behavior
- T1021 - Remote Services (Lateral Movement):
  Monitor for suspicious RDP, SSH, or SMB sessions

  ---

  ## Mapping SOC workflows to ATT&CK
  - Threat Detection: Use ATT&CK techniques as the baseline for detection rules
  - Threat Hunting: Formulate hunts around specific ATT&CK behaviors
  - Incident Response: Map observed attacker activity to ATT&CK to understand progression
  - Gap Analysis: Identify missing detections in the SOC by reviewing coverage

  ---

  ## Tools & Integrations
  - ATT&CK Navigator: Web tool to visualize and map ATTA&CK coverage
  - SIEMs (Splunk, ELK, Sentinel): Use ATT&CK IDs in detection rules
  - EDR tools (CrowdStrike, Defender ATP): Often map alerts to ATTA&CK techniques

  ---

  ## Example Use Case
  - Brute-force SSH attempts detected → Map to T1110: Brute Force (Credential Access)
  - Suspicious PowerShell script execution → Map to T1059.001: PowerShell (Execution)
  - Lateral movement via RDP → nao ti T1021.001: Remote Desktop Protocol

  This mapping helps SOC analysts build a clear attack timeline

  ---

  ## Conclusion
  MITRE ATT&CK is a universal language for cyber defense
  SOC Analysts use it to:
  - Standarize detection rules
  - Track attacker behavior
  - Strengthen blue team defenses