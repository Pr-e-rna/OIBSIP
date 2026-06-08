# Task 8: Capture Network Traffic with Wireshark

## Objective
Capture and analyze network traffic using Wireshark, filtering DNS packets to observe real-time domain resolution activity.

## Tool Used
- **Wireshark** — [https://www.wireshark.org](https://www.wireshark.org)

## System Info
- **Interface Captured:** Wi-Fi (local network)
- **Filter Applied:** `dns`
- **Total Packets Captured:** 1297
- **Packets Displayed (DNS):** 8 (0.6%)
- **Capture Date:** 2026-06-08

## Command / Filter Used
```
Display Filter: dns
```

## Captured Packets Analysis

| No. | Time (s) |   Source    | Destination | Protocol |                      Info                         |
|-----|----------|-------------|-------------|----------|---------------------------------------------------|
|  62 |   2.198  | 192.168.1.4 | 192.168.1.1 |    DNS   |         Standard query — claude.ai (HTTPS)        |
|  64 |   2.198  | 192.168.1.4 | 192.168.1.1 |    DNS   |        Standard query — claude.ai (A record)      |
|  72 |   2.260  | 192.168.1.1 | 192.168.1.4 |    DNS   |        Response — claude.ai → 160.79.104.10       |
|  80 |   2.275  | 192.168.1.1 | 192.168.1.4 |    DNS   |         Response — claude.ai HTTPS record         |
| 387 |  10.840  | 192.168.1.4 | 192.168.1.1 |    DNS   |        Standard query — accounts.google.com       |
| 389 |  10.840  | 192.168.1.4 | 192.168.1.1 |    DNS   |       Standard query — accounts.google.com (A)    |
| 398 |  10.906  | 192.168.1.1 | 192.168.1.4 |    DNS   |  Response — accounts.google.com → 192.178.211.84  |
| 400 |  10.907  | 192.168.1.1 | 192.168.1.4 |    DNS   | Response — accounts.google.com SOA ns1.google.com |

## Key Observations

### 1. DNS Query-Response Pattern
- **192.168.1.4** is the local machine (client)
- **192.168.1.1** is the router/DNS resolver
- The client sends a query → router resolves it → sends back the IP address
- This is standard DNS resolution behavior

### 2. claude.ai Resolution
- The client queried `claude.ai` and received IP `160.79.104.10`
- Both an **A record** (IPv4) and **HTTPS record** were requested, showing modern DNS behavior

### 3. accounts.google.com Resolution
- Resolved to `192.178.211.84`
- SOA (Start of Authority) record also returned, pointing to `ns1.google.com`

## Security Implications

### DNS is Unencrypted by Default
- All DNS queries shown here are sent in **plaintext**
- An attacker on the same network can see every domain you visit using a tool like Wireshark
- This is known as **DNS eavesdropping**

### Mitigation
- Use **DNS over HTTPS (DoH)** or **DNS over TLS (DoT)** to encrypt DNS queries
- Windows 11 supports DoH natively under Settings → Network → DNS

### DNS Spoofing Risk
- Without DNSSEC, an attacker could respond with a fake IP address before the real DNS server does
- This is called a **DNS spoofing / cache poisoning attack**

## Files in This Repository
|            File          |                    Description                  |
|--------------------------|-------------------------------------------------|
| `wireshark_capture.pcap` |             Raw packet capture file             |
|        `README.md`       |         This file analysis and explanation      |
|      `screenshots/`      | Screenshot of Wireshark with DNS filter applied |

## References
- [Wireshark Documentation](https://www.wireshark.org/docs/)
- [DNS over HTTPS — RFC 8484](https://datatracker.ietf.org/doc/html/rfc8484)
- [DNS Spoofing — OWASP](https://owasp.org/www-community/attacks/DNS_Spoofing)
