<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=28&duration=3000&pause=1000&color=AB47BC&center=true&vCenter=true&multiline=true&repeat=true&width=800&height=100&lines=%F0%9F%96%A7+Splunk+SIEM+Dashboard;DHCP+Log+Analysis+%7C+Rogue+Device+Detection" alt="Typing SVG" />

![Splunk](https://img.shields.io/badge/Splunk-000000?style=for-the-badge&logo=splunk&logoColor=white)
![SIEM](https://img.shields.io/badge/SIEM-Dashboard-blue?style=for-the-badge)
![SOC](https://img.shields.io/badge/SOC-Analyst-red?style=for-the-badge)
![DHCP](https://img.shields.io/badge/DHCP-Log_Analysis-AB47BC?style=for-the-badge)
![SPL](https://img.shields.io/badge/SPL-Queries-orange?style=for-the-badge)

</div>

> **Project Type:** SOC Analyst Lab — SIEM Dashboard Building  
> **Platform:** Splunk Enterprise / Splunk Cloud  
> **Data Source:** `dhcp_logs.json` (800 events)  
> **Skill Level:** Beginner → Intermediate

## 📸 Completed Dashboard

![DHCP Log Analysis Dashboard](screenshots/dhcp-dashboard.png)

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 📋 Table of Contents

| #   | Section                                              | Status |
| --- | ---------------------------------------------------- | ------ |
| 0   | [Lab Setup & Prerequisites](#lab-setup--prerequisites) | ⬜      |
| 1   | [Task 1 — DHCP Overview Panels](#task-1--dhcp-overview-panels) | ⬜      |
| 2   | [Task 2 — DHCP Patterns](#task-2--dhcp-patterns) | ⬜      |
| 3   | [Task 3 — Rogue Device Detection](#task-3--rogue-device-detection) | ⬜      |
| 4   | [Final Dashboard Layout](#final-dashboard-layout)    | ⬜      |

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Lab Setup & Prerequisites

### What You Need

| Requirement            | Details                                                                 |
| ---------------------- | ----------------------------------------------------------------------- |
| **Splunk Instance**    | Splunk Enterprise (local) or Splunk Cloud (free trial works)            |
| **Data File**          | `dhcp_logs.json` → host `DHCPServer` (800 DHCP events)                 |
| **Sourcetype**         | `_json` for JSON logs                                                   |
| **Key Fields**         | `msg_type`, `mac_address`, `hostname`, `leased_ip`, `classification`   |

### Data Ingestion

1. **Upload `dhcp_logs.json`**
   - Settings → Add Data → Upload → select `dhcp_logs.json`
   - Set **Host** = `DHCPServer`, **Sourcetype** = `_json`
   - Review & Submit

2. **Verify ingestion:**
   ```spl
   source="dhcp_logs.json" host="DHCPServer" | head 10
   ```

### Create the Dashboard

1. Go to **Dashboards** → **Create New Dashboard**
2. Name it **DHCP Log Analysis Dashboard**
3. Select **Classic Dashboard** (Simple XML) → **Absolute** layout → **Create**

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/VgCDAzcKvsR6OM0uWg/giphy.gif" width="30"> Task 1 — DHCP Overview Panels

**Goal:** Monitor DHCP server health — total events, unique device count, successful IP assignments, and rogue device indicators.

> 🎯 All four panels are **Single Value** visualizations.

---

### Panel 1.1 — Total DHCP Events

**SPL Query:**

```spl
source="dhcp_logs.json" host="DHCPServer" sourcetype="_json"
| stats count AS "Total DHCP Events"
```

**What this does:** Counts all DHCP transactions — DISCOVER, OFFER, REQUEST, ACK, NAK, RELEASE, INFORM. Baseline for server load monitoring.

---

### Panel 1.2 — Unique Devices

**SPL Query:**

```spl
source="dhcp_logs.json" host="DHCPServer" sourcetype="_json"
| stats dc(mac_address) AS "Unique Devices"
```

**What this does:** Counts distinct MAC addresses requesting DHCP leases. The `dc()` (distinct count) function ensures each device is counted once regardless of how many lease requests it makes.

> 🔍 **SOC Analyst Tip:** If unique device count suddenly spikes beyond the expected inventory, rogue devices may have connected to the network. Compare against your CMDB inventory.

---

### Panel 1.3 — IP Assignments (ACK)

**SPL Query:**

```spl
source="dhcp_logs.json" host="DHCPServer" sourcetype="_json" msg_type="ACK"
| stats count AS "IP Assignments"
```

**What this does:** Counts successful IP assignments (DHCP ACK messages). This is the number of devices that actually received valid IP configurations from the server.

---

### Panel 1.4 — Suspicious Devices

**SPL Query:**

```spl
source="dhcp_logs.json" host="DHCPServer" sourcetype="_json" classification="Suspicious"
| stats count AS "Suspicious Devices"
```

**What this does:** Counts events from devices classified as suspicious — rogue devices, unknown hostnames, or devices with anomalous MAC address patterns.

> ⚠️ **Security Implication:** Rogue DHCP devices can be:
> - Unauthorized personal devices (BYOD policy violations)
> - Attacker-planted devices for network pivoting
> - Rogue DHCP servers attempting man-in-the-middle attacks

---

### ✅ Task 1 Result

| Total DHCP Events | Unique Devices | IP Assignments (ACK) | Suspicious Devices |
|----|----|----|-----|

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/iY8CRBdQXODJSCERIr/giphy.gif" width="30"> Task 2 — DHCP Patterns

**Goal:** Understand DHCP message flow distribution and identify the most active devices — essential for capacity planning and anomaly detection.

---

### Panel 2.1 — DHCP Message Type Distribution (Pie Chart)

**SPL Query:**

```spl
source="dhcp_logs.json" host="DHCPServer" sourcetype="_json"
| stats count by msg_type
```

**What this does:** Shows the DORA (Discover-Offer-Request-Acknowledge) flow distribution. Normal patterns:
- **DISCOVER + REQUEST + ACK** should be roughly balanced
- High **NAK** count → IP pool exhaustion or configuration issues
- High **RELEASE** without corresponding new leases → devices disconnecting frequently

> 🔍 **SOC Analyst Tip:** An abnormal ratio of DISCOVER to ACK (many discovers, few ACKs) may indicate DHCP starvation attack — an attacker exhausting the IP pool.

---

### Panel 2.2 — Top Devices by Lease Requests (Bar Chart)

**SPL Query:**

```spl
source="dhcp_logs.json" host="DHCPServer" sourcetype="_json"
| top limit=10 hostname
```

**What this does:** Ranks devices by DHCP request frequency. A single device making excessive lease requests may indicate:
- Misconfigured network interface (rapid DHCP cycling)
- DHCP starvation attack tool
- Network instability on that segment

---

### ✅ Task 2 Result

| DHCP Message Types (Pie Chart) | Top Devices (Bar Chart) |
|---|---|

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/3oKIPEqDGUULpEU0aQ/giphy.gif" width="30"> Task 3 — Rogue Device Detection

**Goal:** Surface suspicious and rogue devices on the network for investigation.

---

### Panel 3.1 — Suspicious / Rogue Device Activity (Statistics Table)

**SPL Query:**

```spl
source="dhcp_logs.json" host="DHCPServer" sourcetype="_json" classification="Suspicious"
| table ts, mac_address, hostname, leased_ip, msg_type
| sort -ts
```

**What this does:** Creates an investigation-ready table of all suspicious DHCP activity — showing when a suspicious device requested an IP, its MAC address, hostname, assigned IP, and message type.

> 🔍 **SOC Analyst Rogue Device Response:**
> 1. Verify the MAC address against your network inventory / CMDB
> 2. Check if the hostname follows your naming convention
> 3. If unknown: locate the physical port via switch MAC address table
> 4. Disable the switch port to isolate the device
> 5. Investigate physically — what is this device?

> ⚠️ **Production Enhancement:** Create a lookup table of known/authorized MAC addresses and alert on any MAC not in the whitelist.

---

### ✅ Task 3 Result

> Full-width statistics table showing all suspicious device activity.

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🏁 Final Dashboard Layout

| Row | Panels | Visualization Type |
|-----|--------|-------------------|
| **Input Bar** | Time Range + Submit | Input controls |
| **Row 1** | Total Events · Unique Devices · IP Assignments · Suspicious Devices | 4× Single Value |
| **Row 2** | Message Type Distribution · Top Devices | Pie Chart + Bar Chart |
| **Row 3** | Rogue Device Activity | Statistics Table (full width) |

---

## <img src="https://media2.giphy.com/media/QssGEmpkyEOhBCb7e1/giphy.gif?cid=ecf05e47a0n3gi1bfqntqmob8g9aid1oyj2wr3ds3mg700bl&rid=giphy.gif" width="25"> Complete Simple XML Reference

The full dashboard XML is available at [`xml/dhcp_dashboard.xml`](xml/dhcp_dashboard.xml). Import via **Dashboards** → **Create** → **Edit** → **Source** → Paste → **Save** ✅

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🔑 Key Takeaways for SOC Analysts

| Concept | What You Practiced |
|---------|-------------------|
| **DHCP Monitoring** | Building dashboards for IP assignment visibility |
| **Asset Discovery** | Using DHCP logs to identify all network-connected devices |
| **Rogue Device Detection** | Spotting unauthorized devices via MAC address analysis |
| **DHCP Attack Detection** | Identifying starvation attacks and rogue DHCP servers |
| **SPL Commands** | `stats count`, `dc()`, `top`, `table`, `sort` |

---

## 📂 Project Structure

```
splunk-soc-project/
├── DHCP_LOG_ANALYSIS.md               ← This file
├── data/
│   └── dhcp_logs.json                 ← DHCP event data (800 events)
└── xml/
    └── dhcp_dashboard.xml              ← Importable Splunk XML
```

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=14&duration=4000&pause=1000&color=AB47BC&center=true&vCenter=true&repeat=true&width=435&lines=Built+with+%E2%9D%A4%EF%B8%8F+by+Amresh+Kumar;SOC+Analyst+Portfolio+Project;August+2026" alt="Footer" />

![Views](https://komarev.com/ghpvc/?username=aksingh-splunk-dhcp&label=Views&color=AB47BC&style=flat-square)

</div>
