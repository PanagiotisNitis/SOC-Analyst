# Room: SIEM_Splunk
## Introduction
Slunk is a Security Information and Event Management (SIEM) tool used to collect, index, search, and analyze machine data
SOC analysts use Splunk to detect threats, investigate incidents, and build dashboards for monitoring

---

## Splunk components
- Forwarders → Collect logs from endpoints & send to Splunk
- Indexer → Stores and indexes incoming data
- Search Head → Interface to query and visualize data
- Deployment Server → Manages configuration across agents

---

## Types of Data Collected
- Windows Event Logs (Security, System, Application)
- Linux Syslogs (/var/log)
- Firewall logs
- IDS/IPS logs(Snort, Suricata, Zeek)
- Endpoint Detection logs (EDR/AV)
- Cloud logs (AWS, Azure, GCP)

---

## Splunk Search Basics (SPL - Search Processing Language)
General Syntax:
index=<index_name> source=<log_source> "search_term"
Examples
- Find failed logins (Windows):
index=wineventlog EventCode=4625
- Successful SSH logins (Linux):
index=syslog "Accepted password"
- Top 10 source IPs by failed logins:
index=winevenlog EventCode=4625
| stats count by src_ip
| sort -count
| head 10
- Detect new user account creation:
index=winevenlog EventCode=4720
- Detect suspicious process execution:
index=wineventlog EventCode=4688
| table _time, user, New_Process_Name, Parent_Process_Name

---

## Dashboards & Alerts
- Dashboards: Visual representation of searches (failed logins, suspicious IPs)
- Alerts: Triggered when conditions are met (e.g., >10 failed logins in 5 minutes)
- Examples Alert SPL:
index=wineventlog EventCode=4625
| stats count by src_ip
| where count > 10

---

## SOC Use Cases
- Brute-force detection: Monitor multiple failed login attempts
- Privilege escalation: Alert on new privileged user accounts
- Persistence detection: Identify scheduled tasks or new services
- Lateral movement: Look for explicit credential logons (Event ID 4648)
- Malware activity: Correlate process creation with known IOCs

---

## Integrations
-Splunk can integrate with:
    - Suricata / Zeek → Network detection logs
    - EDR tools (CrowdStrike, SentinelOne)
    - Cloud monitoring (AWS CloudTrail, Azure Monitor, GCP logs)
    - Threat Intelligence feeds

---

## Conlusion
Splunk is a powerful tool for SOC operations
A SOC Analyst should be confortable with:
- Writing SPL queries
- Building dashboards and alerts
- Investigating incidents using log correlation