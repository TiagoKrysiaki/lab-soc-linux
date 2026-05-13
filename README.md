# 🛡️ Linux SOC & DFIR Labs – Monitoring, Detection, Investigation & Incident Response
![SIEM](https://img.shields.io/badge/SIEM-Wazuh-blue)
![Detection](https://img.shields.io/badge/Focus-Threat%20Detection-red)
![OS](https://img.shields.io/badge/OS-Linux-black)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

Practical SOC/DFIR labs demonstrating real-world detection, threat hunting, investigation, persistence analysis, and incident response using Wazuh, auditd, and Linux telemetry.

Hands-on labs focused on Security Operations Center (SOC), Detection Engineering, and DFIR practices using Linux, Wazuh (SIEM), auditd, Suricata, and log analysis.

---

## 🎯 Objective

Simulate realistic attack scenarios and perform the complete SOC/DFIR workflow:

- Monitoring and telemetry collection
- Detection and threat validation
- Investigation (timeline, process analysis, IoCs, persistence hunting)
- Threat classification (MITRE ATT&CK mapping)
- Incident response (containment, eradication, recovery)
- Defense validation and hardening

---

## 🧠 SOC Methodology

Monitoring → Detection → Investigation → Classification → Response

---

## 🚨 Key Skills Demonstrated

- Linux incident response and live response investigation
- Persistence hunting (cron, SSH keys, systemd services)
- Process and parent-child relationship analysis
- EXECVE telemetry analysis with auditd
- Threat hunting and IoC collection
- SIEM monitoring and telemetry validation (Wazuh)
- Detection gap identification and manual investigation
- MITRE ATT&CK mapping and threat classification
- Incident response (containment, eradication, recovery)
- Linux hardening and persistence mitigation
- DFIR-oriented investigation workflow

---

## 🧰 Tools

- Wazuh (SIEM)
- auditd
- auth.log
- Fail2ban
- iptables
- Linux CLI
- Suricata (IDS/NSM)
- tcpdump
- jq
- ps / pstree
- ss / netstat
- systemctl
- cron

---

## 📊 Highlighted Labs

| Lab | Description | Technologies | MITRE |
|-----|------------|-------------|-------|
| [34](./34-soc-linux-persistence-live-response) | Linux persistence + live response + auditd detection + process investigation + persistence hunting | Wazuh, auditd, Linux, Apache | T1059, T1053.003, T1098.004, T1543.002 |
| [33](./33-soc-sqli-exfiltration-enumeration-detection-response) | SQL Injection (SQLi) + data exfiltration + enumeration detection + response validation | Wazuh (log analysis), Apache (access.log), DVWA | T1190, T1048, T1087 |
| [32](./32-soc-dns-tunneling-exfiltration-detection-response-validation) | DNS tunneling + data exfiltration + behavioral detection + egress filtering containment | Suricata (eve.json), tcpdump | T1048.003, T1071.004 |
| [31](./31-soc-web-shell-rce-detection-investigation-response) | Web shell upload + remote command execution (RCE) + post-exploitation investigation + response validation | Wazuh, Apache (access.log), DVWA | T1190, T1505.003, T1059 |
| [30](./30-soc-ssh-bruteforce-persistence-logtampering-response) | SSH brute force + valid access + persistence + log tampering + response validation | Wazuh, auth.log, auditd, Fail2ban | T1110.001, T1078, T1098, T1070.004, T1059 |
| [29](https://github.com/TKrysiaki/lab-soc-linux/tree/main/29-soc-ssh-bruteforce-detection-response-persistence-log-tampering) | SSH brute force + valid access + persistence + log tampering | Wazuh, auth.log | T1110.001, T1078, T1098, T1070.004 |
| [28](https://github.com/TKrysiaki/lab-soc-linux/tree/main/28-soc-ssh-bruteforce-incident-response-persistence-hardening) | SSH brute force + valid access + persistence (no SIEM correlation) | Linux logs, auth.log | T1110.001, T1078, T1098 |
| [27](https://github.com/TKrysiaki/lab-soc-linux/tree/main/27-soc-ssh-bruteforce-detection-response-no-siem) | SSH brute force detection (manual log analysis, no SIEM) | Linux logs, auth.log | T1110.001 |
| [26](https://github.com/TKrysiaki/lab-soc-linux/tree/main/26-soc-ssh-bruteforce-incident-correlation-network-analysis) | SSH brute force detection + network correlation | Wazuh, logs | T1110.001 |
| [25](https://github.com/TKrysiaki/lab-soc-linux/tree/main/25-soc-ssh-bruteforce-detection-response-persistence-remediation) | SSH brute force detection + response + remediation (Fail2ban) | Wazuh, Fail2ban | T1110.001 |
| [24](https://github.com/TKrysiaki/lab-soc-linux/tree/main/24-soc-ssh-bruteforce-detection-response-correlation) | SSH brute force detection + event correlation (SIEM rules) | Wazuh | T1110.001 |
| [23](https://github.com/TKrysiaki/lab-soc-linux/tree/main/23-soc-incident-response-bruteforce-correlation-threatintel) | SSH brute force detection + investigation (timeline + IoCs) | Wazuh | T1110.001 |
| [22](https://github.com/TKrysiaki/lab-soc-linux/tree/main/22-soc-bruteforce-detection-response-wazuh-thehive) | SSH brute force detection using SIEM (Wazuh rules) | Wazuh | T1110.001 |
| [21](https://github.com/TKrysiaki/lab-soc-linux/tree/main/21-ssh-web-attack-detection-correlation-auto-response-wazuh) | Web attack detection + correlation (HTTP logs + SIEM) | Wazuh, web logs | T1190, T1059 |
| [20](https://github.com/TKrysiaki/lab-soc-linux/tree/main/20-ssh-bruteforce-detection-response-wazuh-fail2ban) | Brute force detection + automated blocking (Fail2ban integration) | Wazuh, Fail2ban | T1110.001 |

---

## 📂 Lab Structure

Each lab includes:

- `README.md` → attack overview, detection workflow, investigation summary, MITRE mapping, and response actions  
- `report.md` → detailed SOC/DFIR incident report with timeline, IoCs, persistence analysis, and response validation  
- Evidence → logs, telemetry, alerts, process analysis, screenshots, and investigation artifacts  

---

## 🔍 Detection Examples

### Wazuh — Authentication Correlation

- Rule: `40112`
- Event: Multiple authentication failures followed by successful login
- Detection Logic:
  - Brute force behavior correlation
  - Authentication anomaly validation
  - Suspicious login sequence analysis

### auditd — Linux EXECVE Monitoring

- Event: Suspicious command execution detected
- Commands Observed:
  - `curl`
  - `wget`
  - `chmod`
  - `bash`

- Detection Context:
  - Linux process execution telemetry
  - Persistence activity monitoring
  - Live response investigation support

### MITRE ATT&CK

- [T1110](https://attack.mitre.org/techniques/T1110/) — Brute Force
- [T1078](https://attack.mitre.org/techniques/T1078/) — Valid Accounts
- [T1059](https://attack.mitre.org/techniques/T1059/) — Command and Scripting Interpreter
- [T1053.003](https://attack.mitre.org/techniques/T1053/003/) — Cron
- [T1543.002](https://attack.mitre.org/techniques/T1543/002/) — Systemd Service

---

## 🧑‍💻 Author

Tiago Krysiaki  
Focus: SOC Analyst | Blue Team | Detection Engineering | DFIR  

LinkedIn: https://www.linkedin.com/in/tiagokrysiaki  
Email: t.krysiaki91@gmail.com

---

![GitHub Stats](https://github-readme-streak-stats.herokuapp.com/?user=TKrysiaki&theme=tokyonight)
