# 🛡️ Purple Team Attack & Detection Lab

A structured repository documenting controlled **Red Team attack simulations** alongside **Blue Team telemetry, log analysis, and detection rules**. 

Every lab follows a simple methodology: **Simulate → Capture → Detect → Mitigate.**

---

### 📂 Lab Index & MITRE ATT&CK Mapping

| # | Scenario | MITRE ATT&CK Technique | Offensive Tool | Telemetry / Detection Source |
| :--- | :--- | :--- | :--- | :--- |
| **01** | [SSH Brute Force & Log Analysis](./01-ssh-brute-force) | `T1110.001` (Password Guessing) | Hydra | `/var/log/auth.log`, Fail2Ban |
| **02** | [Nmap SYN Scan Detection](./02-nmap-recon-scanning) | `T1046` (Network Service Discovery) | Nmap | Wireshark (`.pcap`), TCP Flags |

---

### 🧰 Lab Environment
* **Attacker VM:** Kali Linux
* **Target VM:** Ubuntu Server (Isolated Host-Only Network)
* **Analysis Tools:** Wireshark, `tcpdump`, Linux `journalctl` / `auth.log`, Bash
