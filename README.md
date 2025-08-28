# Kali Network Scanning & Analysis Lab

A polished, reproducible walkthrough for host/service discovery and basic web/server assessment using **Nmap, Wireshark, Zenmap, and Nikto**. Designed to demonstrate practical methodology, clear documentation, and actionable findings.

## Goals
- Build a repeatable workflow for network recon and packet analysis
- Produce recruiter-friendly artifacts (commands, outputs, screenshots, and narrative)
- Practice ethical, scoped testing on lab targets only

## Lab Environment
- Host: VirtualBox/VMware
- Target: `10.0.2.15` (lab VM)
- Kali: 2025.x
- Timezone: America/New_York

See `docs/environment.md` for exact VM specs and network layout.

## Tools & How I Used Them

### 1) Nmap — Network/Service Discovery + OS Fingerprinting
**Why it matters:** Quickly identifies open ports, exposed services and versions, and potential misconfigurations.  
**Representative commands:**
```bash
# Fast top-ports scan
nmap --top-ports 1000 -T4 -oA scans/nmap/initial 10.0.2.15

# Service/version detection + default scripts + OS guess
nmap -sC -sV -O -Pn -T4 -oA scans/nmap/deep 10.0.2.15
```
### 2) Wireshark — Packet Analysis & Protocol Verification

**Why it matters:**  
Provides visibility into live or captured traffic. Used to verify service behavior at the packet level and to confirm Nmap findings by observing DNS, TCP, and HTTP flows directly.

**Representative workflow:**
- Captured traffic while the target performed a DNS lookup to `www.google.com`.
- Applied filters to isolate interesting flows:
  - `dns` → show DNS queries/responses
  - `tcp.flags.syn==1 && tcp.flags.ack==0` → new TCP connections
  - `http.request` → cleartext HTTP traffic
  - `tls.handshake` → SSL/TLS negotiations

**What I observed:**  
DNS queries resolved successfully, followed by TCP sessions consistent with expected browser activity. No unexpected cleartext credentials were found in this capture.

---

## 3) Zenmap — GUI-Based Scanning Profiles

**Why it matters:**  
A graphical wrapper for Nmap that allows creation of repeatable scan profiles, side-by-side comparisons, and easy visualization for reports. Recruiters and teams often appreciate its reproducibility.

**Representative usage:**
Created profiles for:
- **Fast Top Ports** → `--top-ports 1000 -T4`
- **Service Detect** → `-sC -sV -T4`
- **Aggressive OS Guess** → `-O -Pn -T4`

**What I observed:**  
Zenmap’s OS fingerprinting results suggested the host was a **VirtualBox VM**, which aligns with my lab environment setup. Saved screenshots and exported reports are stored in `scans/zenmap/`.

---

## 4) Nikto — Web Server Baseline Assessment

**Why it matters:**  
Provides a quick “first look” at web server configurations, default files, and known vulnerabilities. While not exhaustive, it is useful for flagging obvious misconfigurations early in testing. 

**Representative command:**
```bash
nikto -host http://10.0.2.15 -output scans/nikto/nikto-scan.txt -Ask no

