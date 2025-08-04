# 🔐 Security Risk Assessment: Nmap Scan Findings

## 📋 Overview

The following document presents a detailed risk assessment of the open and filtered ports detected during a SYN scan on the local subnet `192.168.1.0/24`. The scan identified 7 live hosts with a range of open, filtered, and closed ports.

---

## ⚠️ Port and Service Risk Summary

| Host IP        | Open/Filtered Ports          | Service                  | Risk Level | Observations & Recommendations |
|----------------|------------------------------|--------------------------|------------|--------------------------------|
| 192.168.1.1    | 53, 80, 443 (open) <br> 22, 23 (filtered) | DNS, HTTP, HTTPS, SSH, Telnet | Medium–High | - **DNS (53)**: Ensure it is not exposed to external users unnecessarily. <br> - **HTTP (80)**: Should redirect to HTTPS. <br> - **SSH (22)** and **Telnet (23)** are filtered — ensure proper firewall rules and remove Telnet if unused. |
| 192.168.1.2    | 6881 (open)                  | BitTorrent Tracker       | High       | BitTorrent traffic can consume bandwidth and expose devices to malware. Recommend disabling if not required. |
| 192.168.1.3    | 40193 (filtered)             | Unknown                  | Medium     | Unknown service on a high port. Verify this is not a backdoor or unwanted background service. |
| 192.168.1.4    | 53 (open)                    | DNS                      | Medium     | DNS open on a personal IP suggests possible DNS proxy/resolver. Ensure secure configuration. |
| 192.168.1.7    | 8008, 8009, 8443, 9000 (open)| HTTP, AJP13, HTTPS-alt, CSListener | High       | - **8008 (HTTP)** and **8009 (AJP13)** are common in vulnerable Tomcat servers. <br> - **9000 (CSListener)** could be a debugger port (like PHP-FPM or SonarQube). Must be access-controlled. |
| 192.168.1.8    | All ports closed             | N/A                      | Low        | No risk detected. All scanned ports are closed. |
| 192.168.1.9    | All ports closed             | N/A                      | Low        | No risk detected. All scanned ports are closed. |

---

## 🛡️ High-Risk Services Identified

### 📌 BitTorrent (6881/tcp)
- **Host:** `192.168.1.2`
- **Risk:** High
- **Reason:** Peer-to-peer applications like BitTorrent expose systems to potential malware, bandwidth abuse, and legal risks.  
- **Recommendation:** Uninstall or block via firewall if not explicitly required.

### 📌 Apache JServ Protocol (8009/tcp)
- **Host:** `192.168.1.7`
- **Risk:** High
- **Reason:** AJP is frequently misconfigured and exploited in Apache Tomcat (e.g., Ghostcat CVE-2020-1938).  
- **Recommendation:** Disable or secure with access control and firewalls.

### 📌 Telnet (23/tcp - filtered)
- **Host:** `192.168.1.1`
- **Risk:** Critical (if open)
- **Reason:** Telnet transmits data unencrypted and should not be used on modern networks.  
- **Recommendation:** Fully disable and replace with SSH.

---

## ✅ General Recommendations

- 🔒 **Harden Services**: Disable unnecessary services (e.g., Telnet, BitTorrent).
- 🌐 **Use Secure Protocols**: Replace HTTP with HTTPS, FTP with SFTP, Telnet with SSH.
- 🔄 **Keep Software Updated**: Regularly patch systems to avoid known vulnerabilities.
- 🔍 **Conduct Regular Audits**: Periodically scan internal networks and review firewall rules.
- 🧱 **Implement Firewalls**: Restrict access to sensitive ports like 22, 445, 3389, 8009, etc.
- 🔑 **Enforce Authentication**: Use key-based SSH login and MFA for critical services.

---

## 📅 Conclusion

The Nmap scan revealed multiple open ports and a few filtered services that require further inspection. Services like AJP13, BitTorrent, and potentially exposed DNS should be audited immediately to prevent misuse or external exploitation. By following best practices in **network hardening** and **access control**, the attack surface can be significantly reduced.

