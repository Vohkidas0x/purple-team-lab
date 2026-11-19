# Lab 01: SSH Brute Force Simulation & Detection

* **MITRE ATT&CK:** [T1110.001 — Brute Force: Password Guessing](https://attack.mitre.org/techniques/T1110/001/)
* **Objective:** Simulate an automated SSH credential guessing attack and identify the resulting host-level authentication artifacts.

---

### 🔴 1. Red Team Simulation
Using **Hydra** from Kali Linux against an isolated Ubuntu target (`192.168.56.102`):

```bash
hydra -l testuser -P passwords.txt ssh://192.168.56.102 -t 4
```

---

### 🔵 2. Blue Team Telemetry (`/var/log/auth.log`)
Inspecting `/var/log/auth.log` on the target host immediately reveals high-frequency failed login attempts from a single source IP:

```text
Nov 19 03:40:12 ubuntu-lab sshd[2411]: Invalid user testuser from 192.168.56.101 port 51422
Nov 19 03:40:12 ubuntu-lab sshd[2411]: Failed password for invalid user testuser from 192.168.56.101 port 51422 ssh2
Nov 19 03:40:13 ubuntu-lab sshd[2413]: Failed password for invalid user testuser from 192.168.56.101 port 51424 ssh2
```

#### Quick Triage Command (Bash)
To extract and count top offending source IPs from SSH logs:
```bash
grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr
```

---

### 🟣 3. Purple Team Remediation & Hardening
1. **Disable Password Logins:** Set `PasswordAuthentication no` in `/etc/ssh/sshd_config` and enforce Ed25519 SSH keys.
2. **Automated Banning:** Configure **Fail2Ban** (`maxretry = 3`, `bantime = 3600`) to automatically block offending IPs at the firewall level.
