<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=2,8,14,20,26&height=180&section=header&text=Tunnel%20Log%20Analysis&fontSize=32&fontColor=ffffff&animation=fadeIn&fontAlignY=35&desc=Tunnel%20%7C%20Covert%20Channel%20%7C%20GRE%20%7C%20Teredo&descSize=14&descAlignY=55&descColor=FFA726" width="100%" />

<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=28&duration=3000&pause=1000&color=FFA726&center=true&vCenter=true&multiline=true&repeat=true&width=800&height=100&lines=%F0%9F%94%92+Splunk+SIEM+Dashboard;Tunnel+Log+Analysis+%7C+Covert+Channel+Detection" alt="Typing SVG" />

![Splunk](https://img.shields.io/badge/Splunk-000000?style=for-the-badge&logo=splunk&logoColor=white)
![SIEM](https://img.shields.io/badge/SIEM-Dashboard-blue?style=for-the-badge)
![SOC](https://img.shields.io/badge/SOC-Analyst-red?style=for-the-badge)
![Tunnel](https://img.shields.io/badge/Tunnel-Log_Analysis-FFA726?style=for-the-badge)
![SPL](https://img.shields.io/badge/SPL-Queries-orange?style=for-the-badge)

</div>

> **Project Type:** SOC Analyst Lab — SIEM Dashboard Building  
> **Platform:** Splunk Enterprise / Splunk Cloud  
> **Data Source:** `tunnel_logs.json` (1,000 events)  
> **Skill Level:** Intermediate

## 📸 Completed Dashboard

![Tunnel Log Analysis Dashboard](screenshots/tunnel-dashboard.png)

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 📋 Table of Contents

| #   | Section                                              | Status |
| --- | ---------------------------------------------------- | ------ |
| 0   | [Lab Setup & Prerequisites](#lab-setup--prerequisites) | ⬜      |
| 1   | [Task 1 — Tunnel Overview Panels](#task-1--tunnel-overview-panels) | ⬜      |
| 2   | [Task 2 — Tunnel Patterns](#task-2--tunnel-patterns) | ⬜      |
| 3   | [Task 3 — Geo-Location Analysis](#task-3--geo-location-analysis) | ⬜      |
| 4   | [Final Dashboard Layout](#final-dashboard-layout)    | ⬜      |

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Lab Setup & Prerequisites

### What You Need

| Requirement            | Details                                                                 |
| ---------------------- | ----------------------------------------------------------------------- |
| **Splunk Instance**    | Splunk Enterprise (local) or Splunk Cloud (free trial works)            |
| **Data File**          | `tunnel_logs.json` → host `TunnelSensor` (1,000 tunnel events)         |
| **Sourcetype**         | `_json` for JSON logs                                                   |
| **Key Fields**         | `tunnel_type`, `action`, `id.orig_h`, `orig_bytes`, `classification`   |

### What Are Network Tunnels?

Network tunnels encapsulate one protocol inside another to transport data across incompatible networks. Common tunnel types:

| Protocol | Purpose | Security Risk |
|----------|---------|---------------|
| **GRE** | Generic Routing Encapsulation — connects remote networks | Can bypass firewall rules |
| **Teredo** | IPv6 over IPv4 tunneling | Often used to evade IPv4-only security controls |
| **6to4** | IPv6 transition mechanism | Can create unmonitored network paths |
| **AYIYA** | Anything-In-Anything tunneling | High data exfiltration risk |
| **IP-in-IP** | IP encapsulation | Can hide malicious traffic inside legitimate packets |

> ⚠️ **Why Tunnel Monitoring Matters:** Attackers use tunneling to bypass firewalls, exfiltrate data, and establish covert C2 channels. Any unexpected tunnel from an external IP is a high-priority alert.

### Data Ingestion

1. **Upload `tunnel_logs.json`**
   - Settings → Add Data → Upload → select `tunnel_logs.json`
   - Set **Host** = `TunnelSensor`, **Sourcetype** = `_json`
   - Review & Submit

2. **Verify ingestion:**
   ```spl
   source="tunnel_logs.json" host="TunnelSensor" | head 10
   ```

### Create the Dashboard

1. Go to **Dashboards** → **Create New Dashboard**
2. Name it **Tunnel Log Analysis Dashboard**
3. Select **Classic Dashboard** (Simple XML) → **Absolute** layout → **Create**

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/VgCDAzcKvsR6OM0uWg/giphy.gif" width="30"> Task 1 — Tunnel Overview Panels

**Goal:** High-level tunnel activity metrics — total events, tunnels established, tunnels terminated, and suspicious tunnel count.

> 🎯 All four panels are **Single Value** visualizations.

---

### Panel 1.1 — Total Tunnel Events

**SPL Query:**

```spl
source="tunnel_logs.json" host="TunnelSensor" sourcetype="_json"
| stats count AS "Total Tunnel Events"
```

**What this does:** Baseline count of all tunnel-related network events detected by the sensor.

---

### Panel 1.2 — Tunnels Established

**SPL Query:**

```spl
source="tunnel_logs.json" host="TunnelSensor" sourcetype="_json" action="tunnel_established"
| stats count AS "Tunnels Established"
```

**What this does:** Counts new tunnel sessions. Each established tunnel represents a new encapsulation channel that could be legitimate (VPN, site-to-site) or malicious (C2, data exfiltration).

---

### Panel 1.3 — Tunnels Terminated

**SPL Query:**

```spl
source="tunnel_logs.json" host="TunnelSensor" sourcetype="_json" action="tunnel_terminated"
| stats count AS "Tunnels Terminated"
```

**What this does:** Counts closed tunnel sessions. Compare with established count — a large gap (many established, few terminated) indicates long-lived tunnels that may be persistent backdoors.

> 🔍 **SOC Analyst Tip:** Established ≫ Terminated = possible persistent C2 channel. Investigate the source IPs of long-lived tunnels immediately.

---

### Panel 1.4 — Suspicious Tunnels

**SPL Query:**

```spl
source="tunnel_logs.json" host="TunnelSensor" sourcetype="_json" classification="Suspicious"
| stats count AS "Suspicious Tunnels"
```

**What this does:** Counts tunnel events classified as suspicious — external IPs establishing new tunnels into internal infrastructure.

---

### ✅ Task 1 Result

| Total Tunnel Events | Tunnels Established | Tunnels Terminated | Suspicious Tunnels |
|----|----|----|-----|

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/iY8CRBdQXODJSCERIr/giphy.gif" width="30"> Task 2 — Tunnel Patterns

**Goal:** Analyze tunnel protocol distribution and identify top tunnel sources — essential for detecting unauthorized VPNs and covert channels.

---

### Panel 2.1 — Tunnel Protocol Distribution (Pie Chart)

**SPL Query:**

```spl
source="tunnel_logs.json" host="TunnelSensor" sourcetype="_json"
| stats count by tunnel_type
```

**What this does:** Shows which tunnel protocols are in use. Expected patterns depend on your network:
- **GRE** dominant → typical for site-to-site VPNs
- **Teredo/6to4** present → IPv6 transition tunnels (often unmonitored)
- **AYIYA** appearing → unusual — high-risk tunneling protocol

> 🔍 **SOC Analyst Tip:** If your organization doesn't use IPv6, Teredo and 6to4 tunnels should not exist. Their presence indicates either misconfiguration or an attacker using IPv6 tunnels to bypass IPv4-only security controls.

---

### Panel 2.2 — Top Tunnel Sources by IP (Bar Chart)

**SPL Query:**

```spl
source="tunnel_logs.json" host="TunnelSensor" sourcetype="_json"
| top limit=10 id.orig_h
```

**What this does:** Ranks source IPs by tunnel event volume. External IPs generating high tunnel traffic are the top investigation priority.

> 🔍 **SOC Analyst Tip:** Cross-reference top external tunnel sources with:
> 1. Is this IP a known VPN gateway? → Expected
> 2. Is this IP a partner organization? → Verify with business
> 3. Unknown external IP? → **Immediate investigation required**

---

### ✅ Task 2 Result

| Tunnel Protocol Distribution (Pie Chart) | Top Tunnel Sources (Bar Chart) |
|---|---|

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/3oKIPEqDGUULpEU0aQ/giphy.gif" width="30"> Task 3 — Geo-Location Analysis

**Goal:** Map tunnel traffic origins on a world map to identify connections from unexpected geographic regions.

---

### Panel 3.1 — Tunnel Traffic by Source Country (Choropleth Map)

**SPL Query:**

```spl
source="tunnel_logs.json" host="TunnelSensor" sourcetype="_json"
| table id.orig_h
| iplocation id.orig_h
| stats count by Country
| geom geo_countries featureIdField="Country"
```

**SPL Breakdown:**

| Line | Command | Purpose |
|------|---------|---------|
| 1 | `source=...` | Select all tunnel events |
| 2 | `\| table id.orig_h` | Extract source IPs |
| 3 | `\| iplocation id.orig_h` | Resolve IPs to countries using MaxMind GeoIP |
| 4 | `\| stats count by Country` | Aggregate tunnel events by country |
| 5 | `\| geom geo_countries...` | Render choropleth map |

**What this does:** World heatmap showing where tunnel traffic originates. Tunnels from countries where your organization has no presence are immediate red flags — especially if they're establishing new tunnels into your internal network.

> ⚠️ **Prerequisites:**
> - Splunk's `iplocation` command requires MaxMind GeoIP (ships with Splunk Enterprise)
> - Internal/RFC1918 IPs won't resolve to geographic locations

---

### ✅ Task 3 Result

> Full-width choropleth map showing tunnel traffic origins by country.

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🏁 Final Dashboard Layout

| Row | Panels | Visualization Type |
|-----|--------|-------------------|
| **Input Bar** | Time Range + Submit | Input controls |
| **Row 1** | Total Events · Established · Terminated · Suspicious | 4× Single Value |
| **Row 2** | Protocol Distribution · Top Sources | Pie Chart + Bar Chart |
| **Row 3** | Tunnel Traffic by Source Country | Choropleth Map (full width) |

---

## <img src="https://media2.giphy.com/media/QssGEmpkyEOhBCb7e1/giphy.gif?cid=ecf05e47a0n3gi1bfqntqmob8g9aid1oyj2wr3ds3mg700bl&rid=giphy.gif" width="25"> Complete Simple XML Reference

The full dashboard XML is available at [`xml/tunnel_dashboard.xml`](xml/tunnel_dashboard.xml). Import via **Dashboards** → **Create** → **Edit** → **Source** → Paste → **Save** ✅

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🔑 Key Takeaways for SOC Analysts

| Concept | What You Practiced |
|---------|-------------------|
| **Tunnel Monitoring** | Building dashboards for encapsulated traffic visibility |
| **Covert Channel Detection** | Identifying unauthorized tunnels used for data exfiltration or C2 |
| **Protocol Analysis** | Understanding GRE, Teredo, 6to4, AYIYA tunnel types and their risks |
| **Persistence Detection** | Comparing established vs terminated tunnels to find persistent backdoors |
| **SPL Commands** | `stats count`, `top`, `table`, `iplocation`, `geom` |

---

## 📂 Project Structure

```
splunk-soc-project/
├── TUNNEL_LOG_ANALYSIS.md             ← This file
├── data/
│   └── tunnel_logs.json               ← Tunnel traffic data (1,000 events)
└── xml/
    └── tunnel_dashboard.xml            ← Importable Splunk XML
```

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=14&duration=4000&pause=1000&color=FFA726&center=true&vCenter=true&repeat=true&width=435&lines=Built+with+%E2%9D%A4%EF%B8%8F+by+Amresh+Kumar;SOC+Analyst+Portfolio+Project;August+2026" alt="Footer" />

![Views](https://komarev.com/ghpvc/?username=aksingh-splunk-tunnel&label=Views&color=FFA726&style=flat-square)

</div>

<div align="center">

[![Back to Main README](https://img.shields.io/badge/%E2%AC%85_Back_to_Main_README-000000?style=for-the-badge)](README.md)

</div>

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=2,8,14,20,26&height=80&section=footer" width="100%" />
