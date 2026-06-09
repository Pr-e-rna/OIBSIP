# Social Engineering Attacks: A Detailed Research Report

**Prepared by:** Prerna Ishwar  
**Internship:** Security Analyst — Oasis Infobyte SIP Program  
**Date:** 2026-06-08

---

## 1. Introduction

Social engineering is the psychological manipulation of people into performing actions or divulging confidential information. Unlike technical attacks that exploit software vulnerabilities, social engineering exploits human psychology — trust, fear, curiosity, and urgency. It is one of the most effective attack vectors because no amount of technical security can fully protect against a well-deceived human.

---

## 2. Types of Social Engineering Attacks

### 2.1 Phishing

#### How It Works
Phishing involves sending fraudulent emails that appear to come from trusted sources (banks, employers, government agencies) to trick recipients into revealing sensitive information or clicking malicious links.

Variants include:
- **Spear Phishing:** Targeted phishing aimed at a specific individual using personalized information
- **Whaling:** Spear phishing targeting high-profile executives (CEOs, CFOs)
- **Smishing:** Phishing via SMS text messages
- **Vishing:** Phishing via voice calls

#### Real-World Case Study
In **2016**, John Podesta (Hillary Clinton's campaign chairman) fell victim to a spear phishing email disguised as a Google security alert. He entered his credentials on a fake Google login page, giving attackers full access to his email account. The leaked emails significantly impacted the US presidential election.

#### Impact
- Credential theft and account takeover
- Financial fraud and wire transfer scams
- Malware installation through malicious attachments
- Data breaches affecting thousands of customers

#### Prevention
- Train employees to identify phishing emails
- Implement **email filtering** and **anti-spam solutions**
- Enable **Multi-Factor Authentication (MFA)** on all accounts
- Use **DMARC, SPF, and DKIM** to prevent email spoofing
- Conduct regular **simulated phishing exercises**

---

### 2.2 Pretexting

#### How It Works
Pretexting involves creating a fabricated scenario (pretext) to manipulate a victim into providing information or taking an action. The attacker typically impersonates someone in authority — an IT technician, bank official, or HR representative.

Example scenarios:
- Calling an employee pretending to be IT support and asking for their password to "fix an issue"
- Impersonating a vendor to extract financial information
- Posing as a new employee to gain physical access to a building

#### Real-World Case Study
In **2008**, the Hewlett-Packard pretexting scandal involved private investigators hired by HP who impersonated board members and journalists to obtain their phone records from telecommunications companies. This exposed how easily personal information can be obtained through social engineering.

#### Impact
- Unauthorized access to sensitive systems and data
- Financial losses through fraudulent transactions
- Reputational damage to organizations

#### Prevention
- Implement strict **identity verification procedures** before sharing information
- Train staff to never share passwords over the phone or email
- Establish a **callback verification system** for sensitive requests
- Create a culture where employees feel safe questioning unusual requests

---

### 2.3 Baiting

#### How It Works
Baiting exploits human curiosity by leaving physical or digital "bait" that victims pick up and use, unknowingly installing malware or exposing their systems.

Common baiting methods:
- Leaving infected USB drives in parking lots or public areas
- Offering free downloads of pirated software or media laced with malware
- Fake online advertisements promising prizes or rewards

#### Real-World Case Study
A study by the **University of Illinois (2016)** dropped 297 USB drives around a university campus. Nearly **98% were picked up**, and **45% of those were plugged into computers** — with users clicking on files within minutes of inserting the drive. This demonstrated how effective physical baiting attacks are in practice.

#### Impact
- Malware and ransomware infection
- Data theft and keylogging
- Network compromise through infected endpoints

#### Prevention
- **Disable AutoRun/AutoPlay** on all endpoints
- Train employees to never plug in unknown USB devices
- Use **Endpoint Detection and Response (EDR)** solutions
- Implement **USB port controls** via group policy

---

### 2.4 Other Notable Attacks

#### Tailgating / Piggybacking
An attacker physically follows an authorized person into a restricted area by pretending to be a delivery person or employee.

#### Quid Pro Quo
An attacker offers a service (e.g., free IT support) in exchange for information or access credentials.

---

## 3. Why Social Engineering Works

| Psychological Trigger | How Attackers Exploit It |
|----------------------|--------------------------|
| Authority | Impersonating executives or IT staff |
| Urgency | "Your account will be suspended in 24 hours" |
| Fear | "Suspicious activity detected on your account" |
| Curiosity | "You won't believe what someone said about you" |
| Trust | Mimicking familiar brands or known contacts |
| Reciprocity | Offering something free to get something in return |

---

## 4. Organizational Impact

Social engineering attacks have caused some of the most damaging breaches in history:
- **2020 Twitter Hack:** Attackers used phone-based social engineering to trick Twitter employees into providing credentials, compromising accounts of Barack Obama, Elon Musk, and Apple to run a Bitcoin scam
- **2021 Colonial Pipeline:** Initial access was gained through a compromised password, likely obtained through social engineering, leading to a ransomware attack that shut down fuel supplies across the US East Coast

---

## 5. Prevention and Recommendations

1. **Security Awareness Training:** Regular, mandatory training for all employees on recognizing social engineering attempts
2. **Simulated Attacks:** Conduct phishing simulations and pretexting exercises to test employee awareness
3. **Zero Trust Policy:** Never trust, always verify — regardless of who is asking
4. **Clear Reporting Procedures:** Make it easy for employees to report suspicious contacts without fear of blame
5. **MFA Everywhere:** Multi-factor authentication prevents credential theft from being immediately useful
6. **Incident Response Plan:** Have a clear plan for when social engineering attacks succeed

---

## 6. Conclusion

Social engineering remains one of the most dangerous and effective attack vectors in cybersecurity precisely because it targets the human element. Technical defenses alone are insufficient — organizations must invest in ongoing security awareness training, strict verification procedures, and a security-conscious culture to effectively defend against these attacks.

---

## 7. References

- OWASP Social Engineering — [https://owasp.org](https://owasp.org)
- SANS Institute Social Engineering — [https://www.sans.org](https://www.sans.org)
- Verizon DBIR 2023 — [https://www.verizon.com/business/resources/reports/dbir/](https://www.verizon.com/business/resources/reports/dbir/)
- University of Illinois USB Study — [https://www.usenix.org/conference/usenixsecurity16](https://www.usenix.org/conference/usenixsecurity16)
- Twitter 2020 Hack Analysis — [https://www.dfs.ny.gov/Twitter_Report](https://www.dfs.ny.gov/Twitter_Report)
