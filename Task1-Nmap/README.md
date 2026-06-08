# Task 1: Basic Network Scanning with Nmap

## Objective
Perform a network scan to identify open ports and services on a local machine using Nmap.

## Tool Used
- **Nmap 7.99** — [https://nmap.org](https://nmap.org)

## System Scanned
- **Target:** localhost (127.0.0.1)
- **OS Detected:** Microsoft Windows 11 24H2 – 25H2
- **Scan Date:** 2026-06-08

## Commands Used

```bash
# Full scan with OS and service version detection
nmap -sV -O localhost

# Save results to file
nmap -sV localhost -oN nmap_scan_results.txt
```

## Scan Results

|   Port  | State |    Service   |        Version       |
|---------|-------|--------------|----------------------|
| 135/tcp | open  |     msrpc    | Microsoft Windows RPC|
| 445/tcp | open  | microsoft-ds |      Windows SMB     |

Total: 998 closed ports (not shown), 2 open ports detected.

## Findings & Significance

### Port 135 — Microsoft RPC (Remote Procedure Call)
- **What it is:** RPC is used by Windows for inter-process communication, including DCOM services.
- **Security Risk:** Port 135 has historically been exploited by worms like Blaster (MS03-026). It should be blocked on public-facing interfaces.
- **Recommendation:** Restrict access via firewall rules; ensure Windows patches are up to date.

### Port 445 — Microsoft-DS (SMB)
- **What it is:** Server Message Block (SMB) protocol used for file sharing, printer sharing, and network communication between Windows machines.
- **Security Risk:** Port 445 was the attack vector for the **WannaCry ransomware (2017)** and **EternalBlue exploit**. Leaving it open without patching is a critical vulnerability.
- **Recommendation:** Block port 445 at the network perimeter. Disable SMBv1. Ensure MS17-010 patch is applied.

## Key Takeaways
- Even a localhost scan reveals services that could be exploited if exposed to a network.
- Windows RPC and SMB are common attack surfaces that require active monitoring.
- Regular network scanning with Nmap helps identify unintended open ports before attackers do.

## Files in This Repository
|           File          |           Description             |
|-------------------------|-----------------------------------|
| `nmap_scan_results.txt` | Raw Nmap output saved during scan |
| `README.md`             | This file analysis & explanation  |
| `screenshots/`          | Screenshot of Nmap output from CMD |

## References
- [Nmap Documentation](https://nmap.org/docs.html)
- [CVE MS03-026 — RPC Vulnerability](https://docs.microsoft.com/en-us/security-updates/securitybulletins/2003/ms03-026)
- [EternalBlue / WannaCry — MS17-010](https://docs.microsoft.com/en-us/security-updates/securitybulletins/2017/ms17-010)
