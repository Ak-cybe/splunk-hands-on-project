<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,12,19,24,30&height=200&section=header&text=Splunk%20SIEM%20-%20SOC%20Analyst%20Lab&fontSize=36&fontColor=ffffff&animation=fadeIn&fontAlignY=35&desc=SSH%20%7C%20Web%20%7C%20DNS%20%7C%20FTP%20%7C%20SMTP%20%7C%20DHCP%20%7C%20Tunnel%20%7C%20AWS%20GuardDuty&descSize=16&descAlignY=55&descColor=00F5FF" width="100%" />

<div align="center">

<img src="https://media.giphy.com/media/077i6AULCXc0FKTj9s/giphy.gif" width="100" />

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=32&duration=3000&pause=1000&color=00F5FF&center=true&vCenter=true&multiline=true&repeat=true&width=900&height=120&lines=%F0%9F%9B%A1%EF%B8%8F+Splunk+SIEM+%E2%80%94+SOC+Analyst+Lab;8+Dashboards+%7C+Threat+Detection+%7C+Cloud+Security" alt="Typing SVG" />

<img src="https://media.giphy.com/media/SWoSkN6DxTszqIKEqv/giphy.gif" alt="Coder GIF" width="400">

<br/>

![Splunk](https://img.shields.io/badge/Splunk-000000?style=for-the-badge&logo=splunk&logoColor=white)
![SIEM](https://img.shields.io/badge/SIEM-Dashboard-blue?style=for-the-badge)
![SOC](https://img.shields.io/badge/SOC-Analyst-red?style=for-the-badge)
![SSH](https://img.shields.io/badge/SSH-Brute_Force-green?style=for-the-badge)
![Apache](https://img.shields.io/badge/Apache-Web_Traffic-D22128?style=for-the-badge&logo=apache&logoColor=white)
![DNS](https://img.shields.io/badge/DNS-Log_Analysis-4FC3F7?style=for-the-badge)
![FTP](https://img.shields.io/badge/FTP-Log_Analysis-66BB6A?style=for-the-badge)
![SMTP](https://img.shields.io/badge/SMTP-Phishing_Detection-FF7043?style=for-the-badge)
![DHCP](https://img.shields.io/badge/DHCP-Rogue_Device-AB47BC?style=for-the-badge)
![Tunnel](https://img.shields.io/badge/Tunnel-Covert_Channel-FFA726?style=for-the-badge)
![AWS](https://img.shields.io/badge/AWS-GuardDuty-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![SPL](https://img.shields.io/badge/SPL-Queries-orange?style=for-the-badge)

**A comprehensive SIEM lab portfolio with 8 Splunk dashboards covering SSH, Web Traffic, DNS, FTP, SMTP, DHCP, Tunnel, and AWS GuardDuty cloud threat analysis — built with SPL queries, importable XML, and geo-location threat intelligence.**

<br/>

<img src="https://img.shields.io/badge/📊_Total_Events-8,701-00F5FF?style=for-the-badge" />
<img src="https://img.shields.io/badge/🖥️_Dashboards-8-FF6B6B?style=for-the-badge" />
<img src="https://img.shields.io/badge/📝_Lab_Guides-8-66BB6A?style=for-the-badge" />
<img src="https://img.shields.io/badge/☁️_Cloud-AWS_GuardDuty-FF9900?style=for-the-badge" />

</div>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/VgCDAzcKvsR6OM0uWg/giphy.gif" width="30"> What This Project Covers

This repository contains **8 complete Splunk SIEM dashboards** built from scratch — each with a step-by-step lab guide, SPL queries, importable XML, and real log data.

| # | Dashboard | Events | Key Skills | Guide |
|---|-----------|--------|-----------|-------|
| 1 | 🛡️ **SSH Log Analysis** | 1,201 SSH events | Brute-force detection, failed login analysis, geo-location mapping | [`SSH_LOG_ANALYSIS.md`](SSH_LOG_ANALYSIS.md) |
| 2 | 🌐 **Web Traffic Analysis** | 2,000 Apache events | HTTP status analysis, URI pattern detection, IP attribution | [`WEB_TRAFFIC_DASHBOARD.md`](WEB_TRAFFIC_DASHBOARD.md) |
| 3 | 🌐 **DNS Log Analysis** | 1,500 DNS events | DGA detection, NXDOMAIN analysis, suspicious domain hunting | [`DNS_LOG_ANALYSIS.md`](DNS_LOG_ANALYSIS.md) |
| 4 | 📁 **FTP Log Analysis** | 1,200 FTP events | File transfer monitoring, anonymous access detection, command analysis | [`FTP_LOG_ANALYSIS.md`](FTP_LOG_ANALYSIS.md) |
| 5 | 📧 **SMTP Log Analysis** | 1,000 email events | Phishing detection, attachment analysis, TLS compliance | [`SMTP_LOG_ANALYSIS.md`](SMTP_LOG_ANALYSIS.md) |
| 6 | 🖧 **DHCP Log Analysis** | 800 DHCP events | Rogue device detection, IP lease monitoring, asset discovery | [`DHCP_LOG_ANALYSIS.md`](DHCP_LOG_ANALYSIS.md) |
| 7 | 🔒 **Tunnel Log Analysis** | 1,000 tunnel events | Covert channel detection, protocol analysis, persistent backdoor hunting | [`TUNNEL_LOG_ANALYSIS.md`](TUNNEL_LOG_ANALYSIS.md) |
| 8 | ☁️ **AWS GuardDuty** | 1,000 findings | Cloud threat detection, MITRE ATT&CK mapping, S3→Splunk pipeline | [`AWS_GUARDDUTY_ANALYSIS.md`](AWS_GUARDDUTY_ANALYSIS.md) |

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/3oKIPnAiaMCws8nOsE/giphy.gif" width="30"> Dashboard Previews

### 🛡️ SSH Log Analysis Dashboard

![SSH Dashboard](screenshots/dashboard-complete.png)

> **Panels:** Total SSH Events · Successful Logins · Failed Logins · Invalid User Attempts · Failed Logins by Username · Brute Force IPs · Geo-Location Map

---

### 🌐 Web Traffic Analysis Dashboard

![Web Traffic Dashboard](screenshots/web-traffic-dashboard.png)

> **Panels:** Total Web Requests · Successful Responses · Client Errors (4xx) · Server Errors (5xx) · Top URIs · Top IPs · Geo-Location Map

---

### 🌐 DNS Log Analysis Dashboard

![DNS Dashboard](screenshots/dns-dashboard.png)

> **Panels:** Total DNS Queries · Successful Resolutions · NXDOMAIN Responses · Suspicious Queries · Top Queried Domains · Query Type Distribution · Suspicious Domain Table

---

### 📁 FTP Log Analysis Dashboard

![FTP Dashboard](screenshots/ftp-dashboard.png)

> **Panels:** Total FTP Events · Successful Transfers · Failed Operations · Suspicious Activity · Top Users · Command Distribution · Geo-Location Map

---

### 📧 SMTP Log Analysis Dashboard

![SMTP Dashboard](screenshots/smtp-dashboard.png)

> **Panels:** Total Emails · With Attachments · Unencrypted (No TLS) · Suspicious Emails · Top Senders · Attachment Types · Geo-Location Map

---

### 🖧 DHCP Log Analysis Dashboard

![DHCP Dashboard](screenshots/dhcp-dashboard.png)

> **Panels:** Total DHCP Events · Unique Devices · IP Assignments · Suspicious Devices · Message Type Distribution · Top Devices · Rogue Device Table

---

### 🔒 Tunnel Log Analysis Dashboard

![Tunnel Dashboard](screenshots/tunnel-dashboard.png)

> **Panels:** Total Tunnel Events · Tunnels Established · Tunnels Terminated · Suspicious Tunnels · Protocol Distribution · Top Sources · Geo-Location Map

---

### ☁️ AWS GuardDuty Cloud Threat Dashboard

![GuardDuty Dashboard](screenshots/guardduty-dashboard.png)

> **Panels:** Total Findings · High/Medium/Low Severity · Finding Types · MITRE ATT&CK Tactics · Affected EC2 Instances · Compromised IAM Users · High Severity Detail Table · Threat Source Map

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/iY8CRBdQXODJSCERIr/giphy.gif" width="25"> Skills Demonstrated

| Category | Skills |
|----------|--------|
| **SIEM Operations** | Dashboard creation, panel configuration, shared time tokens, XML source editing |
| **SPL Queries** | `stats count`, `dc()`, `top`, `where`, `table`, `iplocation`, `geom`, `sort`, field filtering |
| **Threat Detection** | Brute-force identification, DGA/C2 detection, phishing triage, rogue device hunting, covert channel analysis |
| **Cloud Security** | AWS GuardDuty, S3→SQS→Splunk pipeline, IAM credential compromise response, MITRE ATT&CK Cloud mapping |
| **Log Analysis** | SSH, Apache, DNS, FTP, SMTP, DHCP, Tunnel, GuardDuty logs (JSON) — 8 source types |
| **Geo-Intelligence** | IP-to-country resolution, choropleth mapping, geo-blocking recommendations |
| **SOC Workflow** | Alert triage mindset, threat hunting queries, incident response playbooks, analyst tips embedded throughout |

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/WUlplcMpOCEmTGBtBW/giphy.gif" width="25"> Quick Start

### Option 1 — Follow the Step-by-Step Guide

1. Pick a dashboard from the table above
2. Upload the corresponding log data from the `data/` folder into Splunk
3. Follow the task-by-task instructions to build each panel manually
4. Learn SPL by doing ✅

### Option 2 — One-Click XML Import

1. Open Splunk → **Dashboards** → **Create New Dashboard**
2. Click **Edit** → **Source** (top-left)
3. Paste the XML from any of the 8 dashboard files in `xml/`:
   - [`xml/ssh_dashboard.xml`](xml/ssh_dashboard.xml) — SSH Dashboard
   - [`xml/web_traffic_dashboard.xml`](xml/web_traffic_dashboard.xml) — Web Traffic Dashboard
   - [`xml/dns_dashboard.xml`](xml/dns_dashboard.xml) — DNS Dashboard
   - [`xml/ftp_dashboard.xml`](xml/ftp_dashboard.xml) — FTP Dashboard
   - [`xml/smtp_dashboard.xml`](xml/smtp_dashboard.xml) — SMTP Dashboard
   - [`xml/dhcp_dashboard.xml`](xml/dhcp_dashboard.xml) — DHCP Dashboard
   - [`xml/tunnel_dashboard.xml`](xml/tunnel_dashboard.xml) — Tunnel Dashboard
   - [`xml/guardduty_dashboard.xml`](xml/guardduty_dashboard.xml) — AWS GuardDuty Dashboard
4. Click **Save** → Done 🚀

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/fwbZnTftCXVocKzfxR/giphy.gif" width="30"> Project Structure

```
splunk-soc-project/
│
├── 📄 README.md                          ← You are here
├── 📄 SSH_LOG_ANALYSIS.md                ← SSH Dashboard guide
├── 📄 WEB_TRAFFIC_DASHBOARD.md           ← Web Traffic Dashboard guide
├── 📄 DNS_LOG_ANALYSIS.md                ← DNS Dashboard guide
├── 📄 FTP_LOG_ANALYSIS.md                ← FTP Dashboard guide
├── 📄 SMTP_LOG_ANALYSIS.md               ← SMTP Dashboard guide
├── 📄 DHCP_LOG_ANALYSIS.md               ← DHCP Dashboard guide
├── 📄 TUNNEL_LOG_ANALYSIS.md             ← Tunnel Dashboard guide
├── 📄 AWS_GUARDDUTY_ANALYSIS.md          ← AWS GuardDuty Cloud guide
│
├── 📁 screenshots/
│   ├── 🖼️ dashboard-complete.png         ← SSH dashboard screenshot
│   ├── 🖼️ web-traffic-dashboard.png      ← Web Traffic screenshot
│   ├── 🖼️ dns-dashboard.png              ← DNS screenshot
│   ├── 🖼️ ftp-dashboard.png              ← FTP screenshot
│   ├── 🖼️ smtp-dashboard.png             ← SMTP screenshot
│   ├── 🖼️ dhcp-dashboard.png             ← DHCP screenshot
│   ├── 🖼️ tunnel-dashboard.png           ← Tunnel screenshot
│   └── 🖼️ guardduty-dashboard.png        ← GuardDuty screenshot
│
├── 📁 data/
│   ├── 📊 ssh_logs_new.json              ← 1,201 SSH authentication events
│   ├── 📊 apache_logs.json               ← 2,000 Apache web traffic events
│   ├── 📊 dns_logs.json                  ← 1,500 DNS query events
│   ├── 📊 ftp_logs.json                  ← 1,200 FTP transfer events
│   ├── 📊 smtp_logs.json                 ← 1,000 SMTP email events
│   ├── 📊 dhcp_logs.json                 ← 800 DHCP lease events
│   ├── 📊 tunnel_logs.json               ← 1,000 tunnel traffic events
│   └── 📊 guardduty_findings.json        ← 1,000 AWS GuardDuty findings
│
└── 📁 xml/
    ├── 📝 ssh_dashboard.xml              ← Importable Splunk XML (SSH)
    ├── 📝 web_traffic_dashboard.xml      ← Importable Splunk XML (Web Traffic)
    ├── 📝 dns_dashboard.xml              ← Importable Splunk XML (DNS)
    ├── 📝 ftp_dashboard.xml              ← Importable Splunk XML (FTP)
    ├── 📝 smtp_dashboard.xml             ← Importable Splunk XML (SMTP)
    ├── 📝 dhcp_dashboard.xml             ← Importable Splunk XML (DHCP)
    ├── 📝 tunnel_dashboard.xml           ← Importable Splunk XML (Tunnel)
    └── 📝 guardduty_dashboard.xml        ← Importable Splunk XML (GuardDuty)
```

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/QssGEmpkyEOhBCb7e1/giphy.gif" width="25"> Prerequisites

| Requirement | Details |
|-------------|---------|
| **Splunk** | Enterprise (local) or Cloud — [free trial](https://www.splunk.com/en_us/download.html) works |
| **GeoIP** | Built-in `iplocation` command + `geo_countries` lookup (ships with Splunk) |
| **Knowledge** | Basic SPL, network protocols (SSH, HTTP, DNS, FTP, SMTP, DHCP), tunneling concepts, AWS basics |

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/l46Cy1rHbQ92uuLXa/giphy.gif" width="30"> Data Sources Overview

### SSH Logs (`ssh_logs_new.json`) — 1,201 events

| Field | Example | Purpose |
|-------|---------|---------|
| `id.orig_h` | `31.184.137.182` | Source IP (attacker) |
| `event_type` | `Failed SSH Login` | Event classification |
| `username` | `root`, `admin` | Targeted account |
| `auth_attempts` | `8` | Number of auth attempts per session |

### Apache Logs (`apache_logs.json`) — 2,000 events

| Field | Example | Purpose |
|-------|---------|---------|
| `ip` | `185.62.57.52` | Client IP |
| `method` | `GET` | HTTP method |
| `uri` | `/wp-admin` | Requested URI |
| `status` | `403` | HTTP response code |

### DNS Logs (`dns_logs.json`) — 1,500 events

| Field | Example | Purpose |
|-------|---------|---------|
| `query` | `malware-c2.evil.com` | Queried domain name |
| `qtype_name` | `A`, `TXT`, `MX` | DNS query type |
| `rcode_name` | `NOERROR`, `NXDOMAIN` | DNS response code |
| `classification` | `Suspicious` | Threat classification |

### FTP Logs (`ftp_logs.json`) — 1,200 events

| Field | Example | Purpose |
|-------|---------|---------|
| `user` | `anonymous`, `admin` | FTP username |
| `command` | `RETR`, `STOR`, `DELE` | FTP command |
| `arg` | `/tmp/malware.exe` | Target file path |
| `reply_code` | `226`, `550` | FTP reply code |

### SMTP Logs (`smtp_logs.json`) — 1,000 events

| Field | Example | Purpose |
|-------|---------|---------|
| `mailfrom` | `noreply@phishing-site.tk` | Sender email address |
| `rcptto` | `ceo@company.com` | Recipient email |
| `subject` | `URGENT: Password Reset` | Email subject line |
| `attachment_type` | `.exe`, `.pdf` | Attachment file type |

### DHCP Logs (`dhcp_logs.json`) — 800 events

| Field | Example | Purpose |
|-------|---------|---------|
| `msg_type` | `DISCOVER`, `ACK` | DHCP message type |
| `mac_address` | `DE:AD:BE:EF:00:01` | Device MAC address |
| `hostname` | `ROGUE-DEVICE` | Device hostname |
| `leased_ip` | `192.168.1.105` | Assigned IP address |

### Tunnel Logs (`tunnel_logs.json`) — 1,000 events

| Field | Example | Purpose |
|-------|---------|---------|
| `tunnel_type` | `GRE`, `Teredo`, `6to4` | Tunnel protocol |
| `action` | `tunnel_established` | Tunnel event type |
| `orig_bytes` | `245000` | Data transferred (bytes) |
| `classification` | `Suspicious` | Threat classification |

### GuardDuty Findings (`guardduty_findings.json`) — 1,000 findings

| Field | Example | Purpose |
|-------|---------|---------|
| `type` | `CryptoCurrency:EC2/BitcoinTool.B!DNS` | GuardDuty finding type |
| `severity` | `8` | Numeric severity (1-10) |
| `tactic` | `Impact` | MITRE ATT&CK tactic |
| `resourceType` | `EC2`, `IAMUser`, `S3Bucket` | Affected AWS resource |
| `sourceIP` | `91.234.56.78` | Threat actor source IP |
| `sourceCountry` | `Russia` | Geo-location of threat |

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/j2pOGeGYKe2xCCKwfi/giphy.gif" width="30"> Roadmap

- [x] SSH Log Analysis Dashboard + Guide
- [x] Web Traffic Analysis Dashboard + Guide
- [x] DNS Log Analysis Dashboard + Guide
- [x] FTP Log Analysis Dashboard + Guide
- [x] SMTP Log Analysis Dashboard + Guide
- [x] DHCP Log Analysis Dashboard + Guide
- [x] Tunnel Log Analysis Dashboard + Guide
- [x] AWS GuardDuty Cloud Threat Dashboard + Guide
- [x] Standalone XML files for all 8 dashboards
- [x] Real log data with attack patterns (8,701 total events)
- [x] Dashboard screenshots
- [ ] Windows Event Log Dashboard
- [ ] Firewall Log Analysis Dashboard
- [ ] Automated Alert Rules (saved searches)

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/LnQjpWaON8nhr21vNW/giphy.gif" width="30"> Contributing

We welcome contributions! Read the full guide: **[`CONTRIBUTING.md`](CONTRIBUTING.md)**

| Action | How |
|--------|-----|
| ⭐ **Star** | Show your support — helps others discover this project |
| 🍴 **Fork** | Clone and build your own dashboards |
| � **Report Bug** | [Open an Issue](https://github.com/Ak-cybe/splunk-hands-on-project/issues/new) |
| 💡 **Suggest Feature** | Request a new dashboard or analysis module |
| 🔒 **Security** | Report vulnerabilities via [`SECURITY.md`](SECURITY.md) |

<div align="center">

### If you found this helpful, please consider giving it a ⭐!

<img src="https://media.giphy.com/media/dWesBcTLavkZuG35MI/giphy.gif" width="400" />

</div>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 💬 Join Our WhatsApp Community

<div align="center">

<img src="https://img.shields.io/badge/WhatsApp-Join%20Channel-25D366?style=for-the-badge&logo=whatsapp&logoColor=white" alt="WhatsApp Badge"/>

<br/><br/>

### 🚀 **FREE & Premium IT Learning Resources — All in One Channel**

<a href="https://whatsapp.com/channel/0029VbCTIha7YScxsJGpj60Y">
<img src="https://img.shields.io/badge/👉_JOIN_NOW-25D366?style=for-the-badge&logo=whatsapp&logoColor=white&labelColor=128C7E" height="50" alt="Join WhatsApp Channel"/>
</a>

<br/><br/>

</div>
👤 About the owner

🔒 **[Amresh Kumar](https://github.com/Ak-cybe)**

🎓 BCA Student | Cybersecurity & Ethical Hacking Enthusiast

☁️ AWS Cloud Security | 🤖 AI in Security

🎯 Building Practical SOC & AI Security Skills Through Detection

💡 Building automated SOC workflows that turn hours of manual triage into seconds of machine precision

> 📢 **We provide FREE & Premium IT learning resources** — cybersecurity PDFs, AI tools, coding projects, cloud computing materials, networking labs, desktop support notes, interview preparation content, practical tutorials, and career-focused tech education to help students and beginners build real-world IT skills.

| 📚 What You Get | 🎯 Topics Covered |
|:----------------|:-------------------|
| 🔒 Cybersecurity PDFs & Labs | Pentesting, SOC, Blue Team, Red Team |
| 🤖 AI Tools & Resources | ChatGPT, Claude, AI automation workflows |
| 💻 Coding Projects | Python, JavaScript, full-stack development |
| ☁️ Cloud Computing Materials | AWS, Azure, GCP labs & study guides |
| 🌐 Networking Labs | CCNA, CompTIA Network+, packet analysis |
| 🖥️ Desktop Support Notes | IT support, helpdesk, troubleshooting |
| 📝 Interview Preparation | Resume tips, STAR answers, mock Q&A |
| 🎓 Certification Materials | Security+, CySA+, AZ-500, AWS SAA |
| 🛠️ Practical Tutorials | Hands-on labs, real-world projects |
| 📈 Career-Focused Education | Job hunting, portfolio building, skills roadmaps |

<div align="center">

**Whether you want to learn cybersecurity, networking, cloud computing, coding, system administration, AI tools, or prepare for IT jobs and certifications — this channel shares valuable educational content, practical labs, and premium study materials for tech learners.**

<br/>

### 📲 [**Click Here to Join the WhatsApp Channel →**](https://whatsapp.com/channel/0029VbCTIha7YScxsJGpj60Y)

<br/>

</div>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

<div align="center">

### 💀 Threat Coverage Matrix

```
┌─────────────────────────────────────────────────────────────────┐
│                    MITRE ATT&CK Coverage                       │
├──────────────────┬──────────────────┬───────────────────────────┤
│ 🔍 Reconnaissance│ 🚪 Initial Access│ 🔑 Credential Access      │
│   DNS, Tunnel    │  SSH, GuardDuty  │  SSH, FTP, IAM            │
├──────────────────┼──────────────────┼───────────────────────────┤
│ 📤 Exfiltration  │ 💣 Impact        │ 🕵️ Command & Control       │
│  FTP, S3, SMTP   │  GuardDuty       │  DNS, Tunnel              │
├──────────────────┼──────────────────┼───────────────────────────┤
│ 🔄 Persistence   │ ⬆️ Priv Escalation│ 🛡️ Defense Evasion       │
│  DHCP, IAM       │  GuardDuty       │  Tunnel, GuardDuty        │
└──────────────────┴──────────────────┴───────────────────────────┘
```

</div>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

<div align="center">

<img src="https://media.giphy.com/media/LnQjpWaON8nhr21vNW/giphy.gif" width="60" />

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=16&duration=4000&pause=1000&color=00F5FF&center=true&vCenter=true&repeat=true&width=500&lines=Built+with+%E2%9D%A4%EF%B8%8F+by+Amresh+Kumar;SOC+Analyst+Portfolio+%7C+August+2026;8+Dashboards+%7C+8%2C701+Events+%7C+Cloud+%2B+On-Prem" alt="Footer" />

![Views](https://komarev.com/ghpvc/?username=amresh-splunk-soc&label=Profile+Views&color=00f5ff&style=flat-square)
![Stars](https://img.shields.io/github/stars/Ak-cybe/splunk-hands-on-project?style=flat-square&color=00F5FF)
![Forks](https://img.shields.io/github/forks/Ak-cybe/splunk-hands-on-project?style=flat-square&color=FF6B6B)
![Last Commit](https://img.shields.io/github/last-commit/Ak-cybe/splunk-hands-on-project?style=flat-square&color=66BB6A)
![License](https://img.shields.io/github/license/Ak-cybe/splunk-hands-on-project?style=flat-square&color=AB47BC)
![Repo Size](https://img.shields.io/github/repo-size/Ak-cybe/splunk-hands-on-project?style=flat-square&color=FFA726)

**📜 License:** [MIT](LICENSE) — Free to use, modify, and share

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,12,19,24,30&height=80&section=footer" width="100%" />

</div>
