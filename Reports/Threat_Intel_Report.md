# 🛡️ Threat Intelligence Report — T-Pot Honeypot Deployment & Analysis

## 1. Overview  
A cloud-hosted **T-Pot honeypot** was deployed to capture and analyze malicious internet traffic across multiple protocols.  
Within the first **48 hours**, the system recorded **20,000+ intrusion attempts**, targeting SSH, Telnet, HTTP, SMB, SQL, and other internet-exposed services.

Data was processed and visualized using:

- **Suricata IDS**
- **Elasticsearch**
- **Kibana Dashboards**
- **T-Pot Honeypot Suite (Cowrie, Dionaea, Heralding, Conpot, etc.)**

This environment enabled real-time observation of attacker TTPs, botnet propagation, reconnaissance methods, and payload delivery patterns.

---

## 2. Key Findings

### 🔥 Botnet Activity  
- Strong signature of **Mirai** and **Gafgyt** variants  
- Predictable attack waves every **5–10 minutes**  
- Repeated credential attacks targeting SSH & Telnet  
- Identical payloads, timing loops, and UA strings → automated IoT botnet behavior

### 🧭 Human Reconnaissance  
- Low-frequency, irregular probes across SMB, SQL, admin pages  
- Targeted enumeration (e.g., `/wp-admin`, `/phpmyadmin`)  
- Unique command structures → non-automated sources

### 🧨 Exploit Attempts  
- Suricata triggered multiple CVE-based alerts  
- Web RCE attempts (PHP-based exploit kits)  
- Shellcode execution attempts via Dionaea & ElasticPot  
- Mixed vectors across HTTP/443, SQL (3306/1433), RDP (3389)

### 📡 High-Volume Scanning  
- Distributed scanning from compromised VPS nodes  
- Traffic clusters from ASNs in **Romania, Netherlands, China, Ukraine**

---

## 3. MITRE ATT&CK Mapping

| Behavior | Technique ID | Name |
|----------|-------------|-------|
| SSH brute force | **T1110** | Brute Force |
| Automated scanning | **T1046** | Network Service Scanning |
| HTTP exploit attempts | **T1190** | Exploit Public-Facing Applications |
| Broad probing across IP space | **T1595** | Active Scanning |
| Targeting remote services | **T1021** | Remote Services |

These mappings correspond directly to telemetry captured during analysis.

---

## 4. IOC Summary (Indicators of Compromise)

Types of IOCs extracted:

- Malicious IP addresses  
- Suspicious botnet User-Agents  
- Suricata signature IDs (SIDs)  
- Targeted ports and protocols  
- Credential brute-force patterns  
- Behavioral fingerprints from cowrie & heralding logs  

IOC sources included:

- Suricata alerts  
- Honeypot logs (Cowrie, Heralding, Dionaea)  
- Kibana dashboards  
- p0f OS fingerprinting  
- Fatt network metadata  
- OSINT sources (ASN, GeoIP, threat feeds)

📁 Full IOC sets located in `/IOCs`.

---

## 5. Traffic Characteristics & Patterns

### 🌐 Geographic Distribution
Top attacker origins:

- **Romania** (AS9009 M247)  
- **Netherlands** (Host Sailor / Global Layer)  
- **China** (Tencent Cloud, China Unicom)  
- **Ukraine** (BlazingFast C2 infrastructure)  
- **Argentina** (Telecom Argentina)  

### 💥 Common Attack Payloads
- Telnet & SSH brute force (IoT botnets)  
- CVE scanning against HTTP services  
- SQL enumeration  
- SIP scanning (UDP/5060)  
- RDP credential attacks  

### ⏱ Temporal Behavior
- Botnets showed mechanical timing loops (predictable waves)  
- Manual attacks showed irregular timing and varied enumeration  

This distinction made it easy to categorize traffic into botnet vs. human activity.

---

## 6. Threat Intelligence Insights

### 💀 Malware Families Observed
- **Mirai** (primary)
- **Gafgyt**
- **Unknown IoT botnet variants**

### 🚨 High-Fidelity Suricata Alerts
- **ET MALWARE Mirai Variant Activity**
- **ET SCAN SSH Bruteforce**
- **ET EXPLOIT Possible Shellcode Attempt**
- **ET WEB_SERVER CVE Exploit Attempt**
- **ET CNC Known Botnet C2 Traffic**

These represent real exploitation attempts and active botnet propagation patterns.

### 🕵️ Infrastructure Assessment
- Multiple IPs mapped to known **malicious ASNs**  
- VPS-driven scanning from DigitalOcean, Linode, Scaleway  
- IoT botnet origins from China Unicom & Telecom Argentina  
- C2 infrastructure traces from BlazingFast & M247  

---

## 7. Conclusions

This honeypot deployment successfully captured a high-quality corpus of **real-world attacker behavior**, providing insights into:

- IoT botnet propagation  
- Credential stuffing infrastructure  
- Automated and manual reconnaissance  
- Active exploit attempts targeting exposed services  
- Early-stage C2 communication patterns  

This dataset showcases the value of deception-based telemetry for generating actionable threat intelligence.

---

## 8. Recommendations & Next Steps

### 📌 Data Enrichment
- Expand ASN + GeoIP enrichment  
- Integrate AbuseIPDB / OTX scorecards  
- Cluster attacker IPs by ASN behavior  

### 📌 Detection Engineering
- Build SPL / SIEM rules using extracted IOCs  
- Create alert thresholds based on botnet cycles  

### 📌 Environment Expansion
- Increase log retention window  
- Add Windows honeypots for RDP-specific telemetry  
- Deploy second-region honeypot to compare geo differences  

---

## 9. Appendix

### 📁 Repository Structure
```
/Reports
    Threat_Intel_Report.md

/IOCs
    ioc-ips.txt
    ioc-useragents.txt
    ioc-suricata-sids.txt
    ioc-ips-enriched.csv

/images
    dashboards, attack map, service panels...
```

### 📌 Notes
This report reflects **actual telemetry** captured from a live internet-facing honeypot and demonstrates the full intelligence lifecycle:

**Collection → Detection → Enrichment → Analysis → Reporting**

