# 📡 Network Scanning and Port Enumeration using Nmap


---

## 📝 Task Objective

To scan the local network using Nmap to identify active devices, enumerate open ports, analyze associated services, and assess potential security risks.

---

## 🧰 Tools Used

- **Nmap** – For active network scanning
- **Wireshark** – For packet capture and analysis
- **CMD / Terminal** – For executing commands
- **Online Resources** – Port/service reference guides (IANA, SpeedGuide)

---

## 🔧 Methodology

1. **Installed Nmap**
   - Downloaded from [https://nmap.org/download.html](https://nmap.org/download.html)
   - Verified using: `nmap --version`
  
2.  **Identify Local IP Range**
   - Used `ipconfig` (Windows) or `ip a` (Linux/macOS)
   - Subnet: `192.168.1.0/24`

3. **Run TCP SYN Scan**
   ```bash
   nmap -sS 192.168.1.0/24 -oN Nmap_scan_results.txt

4. **Capture Packets using Wireshark**
   - Wireshark was run during the Nmap scan to monitor live packet flow.
   - The packet capture was saved as Wireshark_scan_capture.pcapng.
   - This helped confirm TCP handshakes, SYN-ACK behavior, and filtered states.

5. **Analyze Discovered Services**
   - Each open port was mapped to its associated service.
   - Online resources (e.g., IANA, Shodan, SpeedGuide) were used to verify service purpose.
   - Services were grouped by risk: low, moderate, high.

6. **Document Risk Assessment**
   - Risks for each service were added to services_risks.md:
      - Exposure to default credentials
      - Outdated protocols (e.g., Telnet)
      - Vulnerabilities in HTTP interfaces
   - Recommendations were provided (e.g., disabling, firewalling, patching).
    
