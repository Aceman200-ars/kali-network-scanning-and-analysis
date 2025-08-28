# Findings & Recommendations (Executive Summary)

During lab scanning of `10.0.2.15`, the host exposed **TCP 135 (MS RPC), 445 (SMB), and 5357 (WSDAPI)**. Packet captures confirmed expected DNS and TCP flows. Web baseline scanning required troubleshooting (see `docs/troubleshooting.md`).

| Area     | Evidence                                               | Risk     | Why it Matters                                          | Recommendation                                    |
|----------|--------------------------------------------------------|----------|---------------------------------------------------------|---------------------------------------------------|
| RPC/135  | `scans/nmap/<ts>_deep.nmap`                            | Medium   | RPC exposure may increase attack surface                | Restrict access; monitor RPC usage                |
| SMB/445  | `scans/nmap/<ts>_deep.gnmap`                           | High     | Common lateral movement vector + legacy issues          | Disable SMBv1; enforce signing; restrict shares   |
| WSD/5357 | `scans/nmap/<ts>_deep.xml`                             | Low–Med  | Service discovery unnecessarily exposed                 | Limit to local; disable if unused                 |
| Web      | `scans/nikto/<ts>.txt` (if reachable)                  | Varies   | Quick misconfig detection                               | Patch, remove risky defaults                      |
| DNS/TCP  | `pcaps/*.pcapng`                                       | Informal | Confirms request/response behavior                      | Baseline normal flows for future comparison       |

**Notes**  
- Zenmap aggressive OS guess indicators suggested a VM (VirtualBox).  
- DNS query to `www.google.com` observed during browsing test. :contentReference[oaicite:2]{index=2}
