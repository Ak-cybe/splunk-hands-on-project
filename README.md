<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=32&duration=3000&pause=1000&color=00F5FF&center=true&vCenter=true&multiline=true&repeat=true&width=900&height=120&lines=%F0%9F%9B%A1%EF%B8%8F+Splunk+SIEM+%E2%80%94+SOC+Analyst+Lab;Dashboard+Building+%7C+Threat+Detection+%7C+Log+Analysis" alt="Typing SVG" />

![Splunk](https://img.shields.io/badge/Splunk-000000?style=for-the-badge&logo=splunk&logoColor=white)
![SIEM](https://img.shields.io/badge/SIEM-Dashboard-blue?style=for-the-badge)
![SOC](https://img.shields.io/badge/SOC-Analyst-red?style=for-the-badge)
![SSH](https://img.shields.io/badge/SSH-Brute_Force-green?style=for-the-badge)
![Apache](https://img.shields.io/badge/Apache-Web_Traffic-D22128?style=for-the-badge&logo=apache&logoColor=white)
![SPL](https://img.shields.io/badge/SPL-Queries-orange?style=for-the-badge)

**A hands-on SIEM lab portfolio covering SSH brute-force detection and web traffic analysis using Splunk dashboards, SPL queries, and geo-location threat intelligence.**

</div>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🎯 What This Project Covers

This repository contains **two complete Splunk SIEM dashboards** built from scratch — each with a step-by-step lab guide, SPL queries, importable XML, and real log data.

| # | Dashboard | Events | Key Skills | Guide |
|---|-----------|--------|-----------|-------|
| 1 | 🛡️ **SSH Log Analysis** | 1,201 SSH events | Brute-force detection, failed login analysis, geo-location mapping | [`SSH_LOG_ANALYSIS.md`](SSH_LOG_ANALYSIS.md) |
| 2 | 🌐 **Web Traffic Analysis** | 2,000 Apache events | HTTP status analysis, URI pattern detection, IP attribution | [`WEB_TRAFFIC_DASHBOARD.md`](WEB_TRAFFIC_DASHBOARD.md) |

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 📸 Dashboard Previews

### 🛡️ SSH Log Analysis Dashboard

![SSH Dashboard](screenshots/dashboard-complete.png)

> **Panels:** Total SSH Events · Successful Logins · Failed Logins · Invalid User Attempts · Failed Logins by Username · Brute Force IPs · Geo-Location Map

---

### 🌐 Web Traffic Analysis Dashboard

![Web Traffic Dashboard](screenshots/web-traffic-dashboard.png)

> **Panels:** Total Web Requests · Successful Responses · Client Errors (4xx) · Server Errors (5xx) · Top URIs · Top IPs · Geo-Location Map

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/iY8CRBdQXODJSCERIr/giphy.gif" width="25"> Skills Demonstrated

| Category | Skills |
|----------|--------|
| **SIEM Operations** | Dashboard creation, panel configuration, shared time tokens, XML source editing |
| **SPL Queries** | `stats count`, `top`, `where`, `table`, `iplocation`, `geom`, field filtering |
| **Threat Detection** | Brute-force identification, credential stuffing patterns, 4xx/5xx anomaly detection |
| **Log Analysis** | SSH authentication logs (JSON), Apache access logs (JSON), syslog (`auth` index) |
| **Geo-Intelligence** | IP-to-country resolution, choropleth mapping, geo-blocking recommendations |
| **SOC Workflow** | Alert triage mindset, threat hunting queries, analyst tips embedded throughout |

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/WUlplcMpOCEmTGBtBW/giphy.gif" width="25"> Quick Start

### Option 1 — Follow the Step-by-Step Guide

1. Pick a dashboard → [`SSH_LOG_ANALYSIS.md`](SSH_LOG_ANALYSIS.md) or [`WEB_TRAFFIC_DASHBOARD.md`](WEB_TRAFFIC_DASHBOARD.md)
2. Upload the log data from the `data/` folder into Splunk
3. Follow the task-by-task instructions to build each panel manually
4. Learn SPL by doing ✅

### Option 2 — One-Click XML Import

1. Open Splunk → **Dashboards** → **Create New Dashboard**
2. Click **Edit** → **Source** (top-left)
3. Paste the XML from:
   - [`xml/ssh_dashboard.xml`](xml/ssh_dashboard.xml) — SSH Dashboard
   - [`xml/web_traffic_dashboard.xml`](xml/web_traffic_dashboard.xml) — Web Traffic Dashboard
4. Click **Save** → Done 🚀

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 📂 Project Structure

```
splunk-soc-project/
│
├── 📄 README.md                          ← You are here
├── 📄 SSH_LOG_ANALYSIS.md                ← SSH Dashboard step-by-step guide
├── 📄 WEB_TRAFFIC_DASHBOARD.md           ← Web Traffic Dashboard guide
│
├── 📁 screenshots/
│   ├── 🖼️ dashboard-complete.png         ← SSH dashboard screenshot
│   └── 🖼️ web-traffic-dashboard.png      ← Web Traffic dashboard screenshot
│
├── 📁 data/
│   ├── 📊 ssh_logs_new.json              ← 1,201 SSH authentication events
│   └── 📊 apache_logs.json               ← 2,000 Apache web traffic events
│
└── 📁 xml/
    ├── 📝 ssh_dashboard.xml              ← Importable Splunk XML (SSH)
    └── 📝 web_traffic_dashboard.xml      ← Importable Splunk XML (Web Traffic)
```

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🔧 Prerequisites

| Requirement | Details |
|-------------|---------|
| **Splunk** | Enterprise (local) or Cloud — [free trial](https://www.splunk.com/en_us/download.html) works |
| **GeoIP** | Built-in `iplocation` command + `geo_countries` lookup (ships with Splunk) |
| **Knowledge** | Basic SPL, HTTP status codes, SSH authentication concepts |

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 📊 Data Sources Overview

### SSH Logs (`ssh_logs_new.json`)

| Field | Example | Purpose |
|-------|---------|---------|
| `id.orig_h` | `31.184.137.182` | Source IP (attacker) |
| `id.resp_h` | `164.254.24.82` | Destination IP (target server) |
| `event_type` | `Failed SSH Login` | Event classification |
| `username` | `root`, `admin` | Targeted account |
| `auth_attempts` | `8` | Number of auth attempts per session |

**Event Types:** `Successful SSH Login` · `Failed SSH Login` · `Multiple Failed Authentication Attempts` · `Connection Without Authentication`

### Apache Logs (`apache_logs.json`)

| Field | Example | Purpose |
|-------|---------|---------|
| `ip` | `185.62.57.52` | Client IP |
| `method` | `GET` | HTTP method |
| `uri` | `/wp-admin` | Requested URI |
| `status` | `403` | HTTP response code |
| `user_agent` | `sqlmap/1.5.1` | Client identifier (detect scanners) |

**Attack Indicators in Data:** SQL injection (`UNION SELECT`), XSS (`<script>alert(1)</script>`), LFI (`../../../../etc/shadow`), admin probing (`/wp-admin`, `/phpmyadmin`), malicious referrers

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🗺️ Roadmap

- [x] SSH Log Analysis Dashboard + Guide
- [x] Web Traffic Analysis Dashboard + Guide
- [x] Standalone XML files for import
- [x] Real log data with attack patterns
- [x] Dashboard screenshots
- [ ] Windows Event Log Dashboard
- [ ] Firewall Log Analysis Dashboard
- [ ] Automated Alert Rules (saved searches)

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🤝 Contributing

This is an educational project. Feel free to:
- ⭐ **Star** this repo if it helped you
- 🍴 **Fork** and build your own dashboards
- 📬 **Open an issue** for suggestions or corrections

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=16&duration=4000&pause=1000&color=00F5FF&center=true&vCenter=true&repeat=true&width=500&lines=Built+with+%E2%9D%A4%EF%B8%8F+by+Amresh+Kumar;SOC+Analyst+Portfolio+%7C+July+2026;%E2%AD%90+Star+this+repo+if+it+helped+you!" alt="Footer" />

![Views](https://komarev.com/ghpvc/?username=amresh-splunk-soc&label=Profile+Views&color=00f5ff&style=flat-square)

**📜 License:** Educational Use

</div>
