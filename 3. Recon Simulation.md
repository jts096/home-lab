# Simulated Reconnaissance Attacks

## Objective
Simulate a pre-attack using scanning tools: Nmap to identify open ports and Nikto to identify web server vulnerabilities. Analyze the attack surface and observe how such pre-attack activity appears in Apache logs, Splunk, and Wireshark to build early threat detection and log analysis skills.

Attacker Machine: Kali Linux (192.168.56.10)   
Target Machine: Ubuntu Server (192.168.56.20) 

## nmap Scan (Kali)
```bash
nmap -sV 192.168.56.20
```

Results:

![](screenshots/Pasted%20image%2020250716025930.png)

- Port 22 (SSH): Open
- Port 80 (HTTP): Open
- Other ports: filtered
### Detection on Ubuntu
#### Wireshark
Captured:

![](screenshots/Pasted%20image%2020250716035540.png)
![](screenshots/Pasted%20image%2020250716035305.png)

- Over 2000 SYN packets were sent by Kali
- Destination ports 22 (SSH) and 80 (HTTP) responded with SYN/ACK
- All other port probes resulted in no reply as UFW was configured to allow only ports 22 and 80

## nikto Web Scan (Kali)
```bash
nikto -host http://192.168.56.20
```
Findings:

![](screenshots/Pasted%20image%2020250716040758.png)

- Server header: `Apache/2.4.52 (Ubuntu)`
- Missing security headers:
    - `X-Frame-Options` (prevents clickjacking)
    - `X-Content-Type-Options` (protects MIME sniffing)
- Server responded with:
    - HTTP methods: GET, POST, OPTIONS, HEAD
    - No CGI directories found
    - ETag header may leak inode information (CVE-2003-1418)
- Apache version is slightly outdated (latest is 2.4.54)
- No critical vulnerabilities found
### Detection on Ubuntu
#### Wireshark

![](screenshots/Pasted%20image%2020250716043629.png)

#### Apache Logs
``` bash
sudo cat /var/log/apache2/access.log
```
![](screenshots/Pasted%20image%2020250716042957.png)

#### Splunk
Used Apache logs as a data source.
Query: `index=main sourcetype=access_combined clientip="192.168.56.10" uri_path!="/"`
![](screenshots/Pasted%20image%2020250717231022.png)
![](screenshots/Pasted%20image%2020250717231209.png)

All detected a rapid sequence of HTTP GET requests from Kali to suspicious paths such as /admin and /cgi-bin. As shown in Splunk, there were over 8000 events recorded in one minute.



