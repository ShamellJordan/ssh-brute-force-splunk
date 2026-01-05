## 📌 Overview
This project demonstrates the end-to-end detection of SSH brute-force attacks using Splunk. Repeated failed SSH authentication attempts were intentionally generated against an Ubuntu host, collected from `/var/log/auth.log`, and ingested into Splunk for analysis. Detection logic was developed using SPL, a real-time alert was configured, and activity was visualized through a custom dashboard. This lab closely mirrors workflows performed by Blue Team / SOC analysts in real enterprise environments.

---

## 🛠 Environment and Tools
- Ubuntu 22.04 LTS Virtual Machine
- Splunk Enterprise (free trial / developer edition)
- VirtualBox
- OpenSSH Server
- Log source: `/var/log/auth.log`
- Terminal / SSH client

This environment simulates a small-scale SIEM deployment ingesting Linux authentication logs, similar to enterprise security monitoring environments.

---

## 🧪 Lab Steps Performed
1. Deployed an Ubuntu virtual machine and installed Splunk Enterprise
2. Configured Splunk to ingest Linux authentication logs from `/var/log/auth.log`
3. Generated multiple failed SSH login attempts to simulate brute-force activity
4. Verified event ingestion by searching for `Failed password` messages
5. Extracted attacker IP addresses and usernames using SPL with regular expressions
6. Aggregated failed login attempts by attacker and target user account
7. Created a real-time alert to trigger on brute-force behavior
8. Built a Splunk dashboard panel and bar chart to visualize findings

**Primary SPL detection query**

index=* "Failed password"
| rex "Failed password for (?<user>\S+) from (?<src_ip>\S+)"
| stats count by src_ip user

This query identifies which IPs attempted to log in, which accounts they targeted, and how many failures occurred.

---

## 🛡 Relevance to Blue Team / SOC Operations
This lab reflects real SOC analyst responsibilities, including:

- Monitoring authentication logs for malicious activity
- Detecting brute-force and credential-stuffing attacks
- Understanding the attack lifecycle and log artifacts created
- Writing SPL detections and tuning alert thresholds
- Creating dashboards to provide situational security awareness
- Translating raw logs into actionable intelligence

The workflow mirrors enterprise use cases such as:
- VPN authentication monitoring
- Linux server access monitoring
- Cloud VM access auditing

---

## 🧠 Key Skills and Knowledge Gained
Through this project, the following skills were developed:

- Log analysis and interpretation of Linux authentication events
- Practical use of Splunk Search Processing Language (SPL)
- Regex-based field extraction and parsing techniques
- Detection engineering fundamentals
- Alert creation, testing, and validation
- Security dashboard design and visualization best practices
- Understanding how brute-force techniques manifest in real logs

---

## 🚀 Future Enhancements Planned
Planned capabilities to extend this lab include:

- Geo-IP enrichment and attacker location mapping
- Detection of “multiple failures followed by a successful login”
- Integration with Fail2Ban for automated IP blocking
- Email / webhook alert notifications
- MITRE ATT&CK technique mapping and documentation
- Adding Windows RDP brute-force detection as a parallel case study

---

## 🖼 Screenshot Descriptions
Screenshots included in `/screenshots` folder demonstrate:

- Raw failed SSH authentication events in Splunk
- SPL query results showing attacker IP, username, and event count
- Alert configuration details and trigger conditions
- Evidence of alert firing in Splunk audit logs
- Dashboard visualization displaying failed SSH attempts

---

## ✅ Conclusion
This project showcases practical Blue Team detection engineering experience using Splunk. It demonstrates the full lifecycle from log ingestion to detection, alerting, and visualization. By simulating SSH brute-force activity and developing detections around it, this lab reinforces how security teams identify and respond to authentication-based attacks in real operational environments.

