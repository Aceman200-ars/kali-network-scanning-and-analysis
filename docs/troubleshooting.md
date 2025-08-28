# Troubleshooting

## Nikto shows "0 hosts tested"
- Confirm target is reachable: `ping <IP>`
- Include schema: `http://<IP>` (not just `<IP>`)
- Update DB: `nikto -update`
- Check firewall/NAT rules; ensure web service is running

## Nmap OS Guess Unreliable in VMs
- Virtual NIC fingerprints reduce accuracy; rely on service evidence + banners

## Wireshark Permissions
- Run as non-root with capture group or use `sudo` judiciously
