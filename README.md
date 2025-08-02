# Cybersecurity Home Lab: Attacker-Defender Simulation

## Overview
This project simulates and documents a small internal network under attack using VirtualBox VMs. It evolved from a focus on network security monitoring and detection to include application security testing.

### Environment
- **Ubuntu Server** (target)
- **Kali Linux** (attacker)
- Both VMs use:
  - Internal Network
  - NAT

---
## Completed
- Initial network setup
- Apache Web Server and UFW configuration
- Recon attack with Nmap and Nikto 
- DoS attack with Apache Bench and mitigation with Fail2Ban
- Nessus vulnerability scan
- DVWA (Damn Vulnerable Web App) configuration
- OWASP ZAP scan on DVWA
- Detection of attacks with Splunk and Wireshark

---
## Next Steps
- Perform manual exploitation of vulnerabilities flagged by ZAP
- Raise DVWA security level and retest attacks

---
## Skills Practiced
- Network configuration and firewalling
- SIEM integration (Splunk)
- Web vulnerability scanning
- Packet analysis
- Application-layer penetration testing

---
## Disclaimer
This lab is for educational purposes only in a contained virtual environment. Do not run scans or attacks on external infrastructure.

