# Network Security Threats: A Comprehensive Research Report

**Prepared by:** Prerna Ishwar  
**Internship:** Security Analyst — Oasis Infobyte SIP Program  
**Date:** 2026-06-08

---

## 1. Introduction

Network security threats are malicious activities that target computer networks with the intent to disrupt services, steal data, or gain unauthorized access. As organizations become increasingly dependent on digital infrastructure, understanding these threats is critical for building effective defenses. This report covers three major categories of network security threats: Denial of Service (DoS) attacks, Man-in-the-Middle (MITM) attacks, and Spoofing attacks.

---

## 2. Denial of Service (DoS) and Distributed Denial of Service (DDoS) Attacks

### 2.1 How It Works
A Denial of Service attack overwhelms a target system — such as a web server, network, or application — with a flood of illegitimate traffic, rendering it unavailable to legitimate users. A Distributed DoS (DDoS) attack scales this up by using thousands of compromised machines (a botnet) to launch the attack simultaneously.

Common DDoS techniques include:
- **Volumetric attacks:** Flooding bandwidth with UDP/ICMP packets
- **Protocol attacks:** Exploiting weaknesses in Layer 3/4 protocols (e.g., SYN flood)
- **Application layer attacks:** Targeting HTTP/HTTPS services with seemingly legitimate requests

### 2.2 Impact
- Service outages costing businesses thousands to millions of dollars per hour
- Reputational damage and loss of customer trust
- Used as a smokescreen while attackers perform other malicious activities

### 2.3 Real-World Example
In **2016**, the Mirai botnet launched a massive DDoS attack against Dyn, a major DNS provider. The attack took down major websites including Twitter, Reddit, Netflix, and GitHub for several hours, affecting millions of users across the US and Europe.

### 2.4 Mitigation Strategies
- Deploy **rate limiting** and **traffic filtering** at the network perimeter
- Use **Content Delivery Networks (CDNs)** with built-in DDoS protection (e.g., Cloudflare)
- Implement **Anycast network diffusion** to spread traffic across multiple servers
- Use **Intrusion Detection Systems (IDS)** to detect abnormal traffic patterns
- Subscribe to **DDoS protection services** from ISPs

---

## 3. Man-in-the-Middle (MITM) Attacks

### 3.1 How It Works
A Man-in-the-Middle attack occurs when an attacker secretly intercepts and potentially alters communications between two parties who believe they are communicating directly with each other. The attacker positions themselves between the victim and the intended destination.

Common MITM techniques include:
- **ARP Spoofing:** Sending fake ARP messages to link the attacker's MAC address with a legitimate IP
- **SSL Stripping:** Downgrading HTTPS connections to HTTP to intercept plaintext data
- **DNS Spoofing:** Returning fake DNS responses to redirect traffic to malicious servers
- **Evil Twin Attack:** Setting up a rogue Wi-Fi access point mimicking a legitimate one

### 3.2 Impact
- Theft of sensitive data including login credentials, financial information, and personal data
- Session hijacking allowing attackers to impersonate legitimate users
- Injection of malicious content into web pages

### 3.3 Real-World Example
In **2015**, researchers discovered that Lenovo laptops shipped with pre-installed adware called **Superfish** that used a self-signed root certificate to perform MITM attacks on all HTTPS traffic, exposing users' encrypted communications to potential interception.

### 3.4 Mitigation Strategies
- Always use **HTTPS** and verify SSL/TLS certificates
- Enable **HTTP Strict Transport Security (HSTS)** on web servers
- Use **VPNs** especially on public Wi-Fi networks
- Implement **mutual TLS (mTLS)** for API communications
- Use **certificate pinning** in mobile applications
- Enable **DNSSEC** to prevent DNS spoofing

---

## 4. Spoofing Attacks

### 4.1 How It Works
Spoofing attacks involve an attacker disguising themselves as a trusted entity to deceive victims or systems. Different types of spoofing target different layers of the network stack.

Common spoofing types include:
- **IP Spoofing:** Forging the source IP address in packets to impersonate another host
- **ARP Spoofing:** Sending fake ARP replies to poison ARP caches on a LAN
- **DNS Spoofing:** Injecting malicious DNS records to redirect users to fake websites
- **Email Spoofing:** Forging the sender address in emails to impersonate trusted senders
- **MAC Spoofing:** Changing the MAC address of a network interface to bypass MAC filtering

### 4.2 Impact
- Bypassing IP-based authentication and access controls
- Enabling MITM attacks through ARP and DNS spoofing
- Facilitating phishing campaigns through email spoofing
- Evading network monitoring and logging

### 4.3 Real-World Example
In **2020**, attackers used **BGP hijacking** (a form of IP spoofing at the routing level) to redirect internet traffic from over 200 networks — including those of major banks and cloud providers — through malicious routers, allowing interception of sensitive traffic.

### 4.4 Mitigation Strategies
- Implement **ingress and egress filtering** (BCP38) to block packets with spoofed source IPs
- Use **Dynamic ARP Inspection (DAI)** on managed switches to prevent ARP spoofing
- Deploy **DNSSEC** to cryptographically sign DNS records
- Use **SPF, DKIM, and DMARC** records to prevent email spoofing
- Enable **802.1X port authentication** to prevent unauthorized devices on a network

---

## 5. Comparison Table

| Threat | Target | Primary Goal | Detection Difficulty |
|--------|--------|--------------|----------------------|
| DoS/DDoS | Availability | Disrupt services | Medium |
| MITM | Confidentiality/Integrity | Intercept/alter data | High |
| Spoofing | Authentication | Impersonate trusted entity | High |

---

## 6. Conclusion

Network security threats continue to evolve in sophistication and scale. DoS/DDoS attacks threaten service availability, MITM attacks compromise data confidentiality and integrity, and spoofing attacks undermine authentication mechanisms. A layered defense strategy combining technical controls, regular monitoring, and security awareness training is essential for organizations to protect their networks against these threats.

---

## 7. References

- OWASP — [https://owasp.org](https://owasp.org)
- NIST Cybersecurity Framework — [https://www.nist.gov/cyberframework](https://www.nist.gov/cyberframework)
- Cloudflare Learning Center — [https://www.cloudflare.com/learning/](https://www.cloudflare.com/learning/)
- Mirai Botnet Case Study — [https://www.incapsula.com/blog/mirai-botnet.html](https://www.incapsula.com/blog/mirai-botnet.html)
- BCP38 Network Ingress Filtering — [https://tools.ietf.org/html/bcp38](https://tools.ietf.org/html/bcp38)
