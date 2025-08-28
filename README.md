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
