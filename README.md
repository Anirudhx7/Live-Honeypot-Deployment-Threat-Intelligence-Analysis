# 🐝 Live Honeypot Deployment & Threat Intelligence Analysis  
**T-Pot | Suricata | Elastic Stack | OSINT | Botnet Analysis**

A cloud-hosted T-Pot honeypot capturing **20,000+ real-world intrusion attempts** in 48 hours.  
This project focuses on attacker behavior, botnet activity, network telemetry, and threat intelligence enrichment through NSM tools and the Elastic Stack.

---

## 📸 Dashboard Previews

### **T-Pot Landing Page**
![T-Pot Landing Page](https://github.com/Anirudhx7/Live-Honeypot-Deployment-Threat-Intelligence-Analysis/blob/e3dfba2dc8bb8518e0f7745afbe8aae0d8938a1d/images/tpot-landing.png)


### **Kibana Dashboards**
![Kibana](https://github.com/Anirudhx7/Live-Honeypot-Deployment-Threat-Intelligence-Analysis/blob/d57a32776c635a0d992c063269cd93c4f1ffd81e/images/kibana-dashboard.png)

### **Attack Map**
![Attack Map](https://github.com/Anirudhx7/Live-Honeypot-Deployment-Threat-Intelligence-Analysis/blob/43147a38e490e55f240184efb56664373bc6a9c6/images/attackmap.png)

> *Images above were captured from the live honeypot environment.*

---

# 🎯 Project Objectives
- Deploy a fully functional T-Pot honeypot on cloud infrastructure  
- Capture high-volume malicious traffic (botnets + manual attacks)  
- Analyze attacker TTPs using Suricata + Elastic Stack  
- Identify IOCs (IPs, User-Agents, ports, honeypot interactions)  
- Map findings to MITRE ATT&CK  
- Produce a structured Threat Intelligence Report  

---

# ⚙️ Deployment Overview
The honeypot was deployed using **T-Pot 24.x**, which bundles 20+ honeypots, NSM tooling, and Elastic Stack integrations.  
Once deployed, T-Pot automatically collects, processes, and visualizes attack telemetry.

---

# 🧩 **Core System Services**
Below is a curated summary of the services essential to this project.

### **System Services**
- **SSH** – Remote secure access into the host  
- **NGINX** – Reverse proxy securing access to dashboards & tools  

### **Elastic Stack**
- **Elasticsearch** — Stores all honeypot events  
- **Logstash** — Normalizes, parses and forwards data  
- **Kibana** — Dashboards for analysis & visualization  

### **Tools**
- **CyberChef** — Data decoding & transformation  
- **Elasticvue** — Elasticsearch cluster browser  
- **Attack Map** — Real-time global attack visualization  
- **Spiderfoot** — OSINT automation for enrichment  

### **Network Security Monitoring (NSM)**
- **Suricata** — IDS/IPS generating signatures & alerts  
- **P0f** — Passive OS fingerprinting  
- **Fatt** — Network metadata extraction from PCAP  

### **Honeypots Included**
A curated subset of T-Pot’s 23 honeypots:
- Cowrie  
- Dionaea  
- Log4Pot  
- Heralding  
- Honeytrap  
- ElasticPot  
- Mailoney  
- ADBHoney  
(Full list available in T-Pot docs.)

These honeypots simulate multiple protocols (SSH, Telnet, SMB, SQL, HTTP, ICS/SCADA, etc.) to attract diverse attacks.

---

# 🔌 Required Ports (Summary)
These are the key ports used in the deployment:

| Port | Protocol | Purpose |
|------|----------|---------|
| 64295 | tcp | SSH access to host |
| 64297 | tcp | T-Pot Web UI via NGINX |
| 64294 | tcp | Sensor → Hive data forwarding |
| 80, 443 | tcp | Web services & dashboards |
| 21, 22, 23, 25 | tcp | Honeypot services (FTP/SSH/Telnet/SMTP) |
| 3306, 1433 | tcp | Database honeypots |
| 5060 | udp/tcp | SIP honeypots |
| 8080, 8443 | tcp | Web application honeypots |

> Ports depend on which honeypots are active. Above list includes only those relevant to captured traffic.

---

# 🔑 Accessing the Environment

### **SSH Access**
```bash
ssh -l <OS_USERNAME> -p 64295 <your-ip>
```

### **Web UI**
```
https://<your-ip>:64297
```

Provides:
- Kibana  
- Attack Map  
- CyberChef  
- Elasticvue  
- Spiderfoot  

---

# 📊 Kibana Dashboards
Kibana provides:
- Attack heatmaps  
- Suricata alert histograms  
- Honeypot interaction timelines  
- Username/password tagclouds  
- Botnet scanning behavior  
- Attacker country distribution  
- Port-based attack histograms  

These dashboards were used to identify:
- Brute-force patterns  
- Password spraying  
- Mirai-like repeating sequences  
- Reconnaissance bursts  
- High-noise botnet signatures  

---

# 🌍 Attack Map
The **Attack Map** provides:
- Live source IPs  
- Geo-location of attackers  
- Protocol targeted  
- Honeypot triggered  
- Attack frequency  

This helped differentiate:
- **Automated botnets** (fast, repetitive, identical payloads)  
- **Human attackers** (slow, selective probing)  

---

# 🔍 Threat Intelligence & Findings

### **Top Observed Behaviors**
- High-volume SSH brute force (Mirai-derived)
- Telnet credential spraying targeting IoT devices  
- Distributed scanning from cloud ASNs  
- Web exploit attempts on port 80/443  
- Repeated exploitation attempts targeting SMB  

### **IOC Extraction**
Extracted:
- Malicious IPs  
- Suspicious User-Agents  
- Suricata signature IDs (SIDs)  
- Frequent ports & protocols  

IOC files included:
- `ioc-ips.txt`  
- `ioc-useragents.txt`  
- `ioc-suricata-sids.txt`  

### **MITRE ATT&CK Mapping**
| Behavior | Technique |
|----------|-----------|
| Brute Force | T1110 |
| Port Scanning | T1046 |
| Exploit Public-Facing App | T1190 |
| Active Scanning | T1595 |
| Remote Service Attempts | T1021 |

---

# 📘 Threat Intelligence Report (Full)
See:  
```
/Reports/Threat_Intel_Report.md
```

Contains:
- Attack summary  
- Botnet pattern analysis  
- IOCs  
- MITRE mapping  
- Recommendations  

---

# 🧠 Learning Outcomes
From this project I gained hands-on experience in:

- Deploying multi-honeypot environments  
- Investigating attacker telemetry in real-time  
- Using Suricata for signature-based detection  
- Building dashboards & correlations in Kibana  
- Performing triage using OSINT tools  
- Extracting & documenting IOCs  
- Translating observations into a threat intel report  

---

# 📁 Repository Structure
```
/Reports
    Threat_Intel_Report.md

/IOCs
    ioc-ips.txt
    ioc-useragents.txt
    ioc-suricata-sids.txt

/images
    tpot-landing.png
    kibana-dashboard.png
    attack-map.png
```

---

# 🏁 Final Notes
T-Pot allowed me to capture **real-world internet attack traffic** and transform it into actionable threat intelligence — bridging the gap between theory and practical security monitoring.



## 📬 Contact

LinkedIn: <a href="linkedin.com/in/anirudh-mehandru">linkedin.com/in/anirudh-mehandru <a>
