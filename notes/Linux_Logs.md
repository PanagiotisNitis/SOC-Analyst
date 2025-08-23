# Room: Linux Logs

## Introduction
Linux systems generate logs that record system events, authentication attempts, errors, and service activity.
As a SOC Analyst, logs are critical for monitoring, detection, and incident response.

Logs are mainly stored in /var/log/ and handled by:

- rsyslog (traditional logging system)

- systemd-journald (modern logging via journalctl)

---

## Key Log Files
| File                                    | Description                                  |
| --------------------------------------- | -------------------------------------------- |
| `/var/log/auth.log`                     | Authentication events (login, sudo, ssh)     |
| `/var/log/syslog` / `/var/log/messages` | General system activity                      |
| `/var/log/secure`                       | Authentication & authorization (RHEL/CentOS) |
| `/var/log/kern.log`                     | Kernel logs                                  |
| `/var/log/dmesg`                        | Boot & hardware events                       |
| `/var/log/faillog`                      | Failed login attempts                        |
| `/var/log/lastlog`                      | Records of last logins                       |

---

## Viewing Logs

- cat /var/log/auth.log → display log file

- less /var/log/syslog → view with navigation

- tail -f /var/log/auth.log → real-time monitoring

- journalctl → view systemd logs

    - journalctl -u ssh.service → show SSH logs

    - journalctl --since "2023-08-01" → filter by date

---

## Useful Examples
- Find failed SSH login attempts:
grep "Failed password" /var/log/auth.log

- Find successful SSH logins:
grep "Accepted password" /var/log/auth.log

- Check sudo usage:
grep "sudo" /var/log/auth.log

- Show last 10 logins:
last-n 10

---

## SOC/Incident Response Use Cases
- Detect brute-force attacks against SSH.

- Track unauthorized sudo attempts.

- Investigate privilege escalation.

- Monitor suspicious services starting at boot.

---

## Tools for Log Analysis
- ausearch / aureport → auditing with auditd

- logwatch → automatic daily reports

- plunk / ELK / Graylog → central log aggregation & analysis

---

## Conclusion
Linux logs are a primary data source for SOC Analysts.
They help in:
- Threat detection (brute force, privilege escalation, malware activity)
- Incident response (timeline reconstruction, identifying attacker activity)
- Compliance & monitoring
