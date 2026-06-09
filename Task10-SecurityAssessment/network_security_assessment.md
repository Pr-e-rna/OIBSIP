# Network Security Assessment Report

**Prepared by:** Prerna Ishwar  
**Internship:** Security Analyst — Oasis Infobyte SIP Program  
**Assessment Date:** 2026-06-08  
**Tools Used:** Nmap 7.99, Wireshark

---

## 1. Executive Summary

This report presents the findings of a network security assessment conducted on a local Windows 11 machine (localhost/127.0.0.1). The assessment involved active network scanning using Nmap to identify open ports and services, and passive traffic analysis using Wireshark to capture and analyze network communications. Two open ports were identified, both associated with core Windows services that present known security risks if left unprotected. DNS traffic analysis revealed unencrypted domain resolution activity, highlighting a risk of DNS eavesdropping and spoofing.

---

## 2. Scope and Methodology

### 2.1 Scope
| Parameter | Detail |
|-----------|--------|
| Target | localhost (127.0.0.1) |
| OS | Microsoft Windows 11 24H2 – 25H2 |
| Network | Local machine (loopback + Wi-Fi interface) |
| Assessment Type | Non-destructive, passive + active scanning |

### 2.2 Methodology
The assessment followed a two-phase approach:

**Phase 1 — Active Scanning (Nmap)**
- Service version detection (`-sV`)
- OS fingerprinting (`-O`)
- Results saved to `nmap_results.txt`

**Phase 2 — Passive Traffic Analysis (Wireshark)**
- Live packet capture on Wi-Fi interface
- DNS filter applied to isolate domain resolution traffic
- 1,297 total packets captured; 8 DNS packets analyzed

---

## 3. Nmap Scan Results

### 3.1 Commands Executed
```bash
nmap -sV -O localhost
nmap -sV localhost -oN nmap_results.txt
```

### 3.2 Open Ports Identified

| Port | Protocol | State | Service | Version |
|------|----------|-------|---------|---------|
| 135 | TCP | Open | msrpc | Microsoft Windows RPC |
| 445 | TCP | Open | microsoft-ds | Windows SMB |

Total ports scanned: 1000  
Closed ports: 998  
Open ports: 2

### 3.3 OS Detection
- **Detected OS:** Microsoft Windows 11 24H2 – 25H2
- **Device Type:** General Purpose
- **Network Distance:** 0 hops (localhost)

---

## 4. Vulnerability Analysis — Open Ports

### 4.1 Port 135 — Microsoft RPC (Remote Procedure Call)

**Severity: Medium**

| Field | Detail |
|-------|--------|
| Service | Microsoft Windows RPC |
| Known CVEs | MS03-026, CVE-2003-0352 |
| Attack Vector | Network |
| Risk | Remote code execution if unpatched |

**Description:**  
RPC (Remote Procedure Call) is a Windows protocol used for inter-process communication. Port 135 is used by the RPC Endpoint Mapper to direct clients to the correct port for a specific service. Historically, this port has been targeted by worms such as the **Blaster worm (2003)** which exploited MS03-026 to execute arbitrary code remotely.

**Risk Assessment:**  
On a local machine not exposed to the internet, risk is moderate. However, if this machine were on a corporate network or directly internet-facing, port 135 would be a high-priority attack surface.

**Recommendations:**
- Block port 135 at the network perimeter firewall
- Ensure all Windows security patches are applied (Windows Update)
- Use Windows Firewall to restrict RPC access to trusted IP ranges only

---

### 4.2 Port 445 — SMB (Server Message Block)

**Severity: High**

| Field | Detail |
|-------|--------|
| Service | Microsoft-DS / SMB |
| Known CVEs | CVE-2017-0144 (EternalBlue), MS17-010 |
| Attack Vector | Network |
| Risk | Remote code execution, ransomware delivery |

**Description:**  
SMB (Server Message Block) is used for file sharing, printer sharing, and network communication between Windows machines. Port 445 was the primary attack vector for the **WannaCry ransomware (2017)** and the **EternalBlue exploit**, which affected over 200,000 systems globally.

**Risk Assessment:**  
This is the highest severity finding in this assessment. SMBv1 in particular is extremely dangerous and should be disabled. Even SMBv2/v3 should be restricted to trusted network segments only.

**Recommendations:**
- Disable SMBv1 immediately via PowerShell:
  ```powershell
  Set-SmbServerConfiguration -EnableSMB1Protocol $false
  ```
- Block port 445 at the network perimeter — never expose to the internet
- Ensure MS17-010 patch is applied
- Enable Windows Defender and keep it updated

---

## 5. Wireshark Traffic Analysis Results

### 5.1 Capture Summary
| Parameter | Value |
|-----------|-------|
| Interface | Wi-Fi |
| Total Packets | 1,297 |
| Filter Applied | `dns` |
| DNS Packets Displayed | 8 (0.6%) |
| Capture Duration | ~11 seconds |

### 5.2 DNS Traffic Observed

| Packet | Direction | Query/Response | Domain | Resolved IP |
|--------|-----------|---------------|--------|-------------|
| 62, 64 | Client → Router | Query | claude.ai | — |
| 72, 80 | Router → Client | Response | claude.ai | 160.79.104.10 |
| 387, 389 | Client → Router | Query | accounts.google.com | — |
| 398, 400 | Router → Client | Response | accounts.google.com | 192.178.211.84 |

**Client IP:** 192.168.1.4 (local machine)  
**DNS Resolver:** 192.168.1.1 (home router)

### 5.3 DNS Security Findings

**Finding 1: Unencrypted DNS Traffic**  
**Severity: Medium**

All DNS queries are transmitted in plaintext over UDP port 53. Any attacker on the same network segment can passively capture all DNS queries using tools like Wireshark, revealing every domain the user visits — even if the actual web traffic is encrypted via HTTPS.

**Recommendations:**
- Enable **DNS over HTTPS (DoH)** in Windows 11:  
  Settings → Network & Internet → Wi-Fi → DNS server assignment → Manual → Enable DNS over HTTPS
- Use privacy-respecting DNS resolvers: Cloudflare (1.1.1.1) or Google (8.8.8.8) with DoH support

**Finding 2: No DNSSEC Validation Observed**  
**Severity: Low–Medium**

DNS responses are not cryptographically signed, making the system potentially vulnerable to DNS spoofing/cache poisoning attacks where an attacker on the network could return fake IP addresses for legitimate domains.

**Recommendations:**
- Configure DNS resolver to use DNSSEC-validating servers
- Consider using enterprise DNS solutions with built-in DNSSEC support

---

## 6. Overall Risk Summary

| Finding | Port/Protocol | Severity | Status |
|---------|--------------|----------|--------|
| Microsoft RPC exposed | 135/TCP | Medium | Open |
| SMB exposed (EternalBlue risk) | 445/TCP | High | Open |
| Unencrypted DNS traffic | UDP/53 | Medium | Active |
| No DNSSEC validation | DNS | Low–Medium | Active |

**Overall Risk Rating: Medium-High**

---

## 7. Remediation Priority

1. **Immediate:** Disable SMBv1, ensure MS17-010 patch applied
2. **Short-term (1 week):** Enable DoH for DNS encryption
3. **Medium-term (1 month):** Review and restrict RPC access via firewall rules
4. **Ongoing:** Regular Nmap scans to monitor for new open ports

---

## 8. Conclusion

This security assessment identified two open ports (135 and 445) on the target Windows 11 system, both associated with core Windows services that carry significant historical exploitation risk. The Wireshark analysis further revealed that DNS traffic is transmitted in plaintext, exposing browsing activity to potential eavesdropping on the local network. The most critical remediation action is ensuring SMBv1 is disabled and all relevant Windows security patches are applied. Implementing DNS over HTTPS would further strengthen the security posture of this system.

---

## 9. Files in This Repository

| File | Description |
|------|-------------|
| `network_security_assessment.md` | This report |
| `nmap_results.txt` | Raw Nmap scan output |
| `wireshark_capture.pcap` | Wireshark packet capture file |
| `screenshots/` | Screenshots from both tools |

---

## 10. References

- Nmap Documentation — [https://nmap.org/docs.html](https://nmap.org/docs.html)
- Wireshark Documentation — [https://www.wireshark.org/docs/](https://www.wireshark.org/docs/)
- MS17-010 EternalBlue — [https://docs.microsoft.com/en-us/security-updates/securitybulletins/2017/ms17-010](https://docs.microsoft.com/en-us/security-updates/securitybulletins/2017/ms17-010)
- CVE-2017-0144 — [https://nvd.nist.gov/vuln/detail/CVE-2017-0144](https://nvd.nist.gov/vuln/detail/CVE-2017-0144)
- DNS over HTTPS — RFC 8484 — [https://datatracker.ietf.org/doc/html/rfc8484](https://datatracker.ietf.org/doc/html/rfc8484)
- NIST Cybersecurity Framework — [https://www.nist.gov/cyberframework](https://www.nist.gov/cyberframework)
