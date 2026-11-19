# Lab 02: Nmap SYN Scan Simulation & Detection

* **MITRE ATT&CK:** [T1046 — Network Service Discovery](https://attack.mitre.org/techniques/T1046/)
* **Objective:** Simulate a stealth TCP SYN port scan and identify the resulting packet-level anomalies in Wireshark.

---

### 🔴 1. Red Team Simulation
Running a half-open TCP SYN scan (`-sS`) against the top 1,000 ports of an isolated target (`192.168.56.102`):

```bash
sudo nmap -sS -Pn -T4 192.168.56.102
```

---

### 🔵 2. Blue Team Telemetry (Wireshark / Packet Analysis)
Filtering the capture in **Wireshark** reveals a burst of incomplete TCP handshakes from a single source IP:
* **Wireshark Display Filter:** `tcp.flags.syn == 1 && tcp.flags.ack == 0`
* **Artifact:** Hundreds of outbound `SYN` packets to sequential ports followed immediately by `RST` (reset) packets—never completing the 3-way handshake (`SYN → SYN-ACK → ACK`).

---

### 🟣 3. Purple Team Remediation & Hardening
1. **Minimize Attack Surface:** Close unused ports and restrict SSH/management interfaces to specific IP ranges via **UFW** (`sudo ufw default deny incoming`).
2. **IDS Alerting:** Enable **Suricata** or **Snort** port-scan thresholds to alert when a single host probes multiple ports within a short time window.
