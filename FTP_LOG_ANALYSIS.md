<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=3,10,16,22,28&height=180&section=header&text=FTP%20Log%20Analysis&fontSize=32&fontColor=ffffff&animation=fadeIn&fontAlignY=35&desc=FTP | File Transfer | Monitoring&descSize=14&descAlignY=55&descColor=66BB6A" width="100%" />

<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=28&duration=3000&pause=1000&color=66BB6A&center=true&vCenter=true&multiline=true&repeat=true&width=800&height=100&lines=%F0%9F%93%81+Splunk+SIEM+Dashboard;FTP+Log+Analysis+%7C+File+Transfer+Monitoring" alt="Typing SVG" />

![Splunk](https://img.shields.io/badge/Splunk-000000?style=for-the-badge&logo=splunk&logoColor=white)
![SIEM](https://img.shields.io/badge/SIEM-Dashboard-blue?style=for-the-badge)
![SOC](https://img.shields.io/badge/SOC-Analyst-red?style=for-the-badge)
![FTP](https://img.shields.io/badge/FTP-Log_Analysis-66BB6A?style=for-the-badge)
![SPL](https://img.shields.io/badge/SPL-Queries-orange?style=for-the-badge)

</div>

> **Project Type:** SOC Analyst Lab — SIEM Dashboard Building  
> **Platform:** Splunk Enterprise / Splunk Cloud  
> **Data Source:** `ftp_logs.json` (1,200 events)  
> **Skill Level:** Beginner → Intermediate

## 📸 Completed Dashboard

![FTP Log Analysis Dashboard](screenshots/ftp-dashboard.png)

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 📋 Table of Contents

| #   | Section                                              | Status |
| --- | ---------------------------------------------------- | ------ |
| 0   | [Lab Setup & Prerequisites](#lab-setup--prerequisites) | ⬜      |
| 1   | [Task 0 — Time Range Input](#task-0--setting-up-time-range) | ⬜      |
| 2   | [Task 1 — FTP Overview Panels](#task-1--ftp-overview-panels) | ⬜      |
| 3   | [Task 2 — FTP Activity Patterns](#task-2--ftp-activity-patterns) | ⬜      |
| 4   | [Task 3 — Suspicious Transfers & Geo-Location](#task-3--suspicious-transfers--geo-location) | ⬜      |
| 5   | [Final Dashboard Layout](#final-dashboard-layout)    | ⬜      |

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Lab Setup & Prerequisites

### What You Need

| Requirement            | Details                                                                 |
| ---------------------- | ----------------------------------------------------------------------- |
| **Splunk Instance**    | Splunk Enterprise (local) or Splunk Cloud (free trial works)            |
| **Data File**          | `ftp_logs.json` → host `FTPServer` (1,200 FTP transfer events)         |
| **Sourcetype**         | `_json` for JSON logs                                                   |
| **Key Fields**         | `user`, `command`, `arg`, `reply_code`, `success`, `classification`     |

### Data Ingestion

1. **Upload `ftp_logs.json`**
   - Settings → Add Data → Upload → select `ftp_logs.json`
   - Set **Host** = `FTPServer`, **Sourcetype** = `_json`
   - Review & Submit

2. **Verify ingestion:**
   ```spl
   source="ftp_logs.json" host="FTPServer" | head 10
   ```

### Create the Dashboard

1. Go to **Dashboards** → **Create New Dashboard**
2. Name it **FTP Log Analysis Dashboard**
3. Select **Classic Dashboard** (Simple XML)
4. Choose **Absolute** layout
5. Click **Create**

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/WUlplcMpOCEmTGBtBW/giphy.gif" width="30"> Task 0 — Setting Up Time Range

**Why:** A single shared time picker ensures all panels update together when the analyst changes the time window.

### Step-by-Step

| # | Action |
|---|--------|
| 1 | Inside the dashboard editor, click **`+ Add Input`** → Select **Time** |
| 2 | Set **Label** → `Time Range`, **Token** → `time_range` |
| 3 | Click **`+ Add Input`** → Select **Submit** |

> ⚠️ **Important:** For **every panel** below, set its time range to the **Shared Time Picker (`time_range`)** token.

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/VgCDAzcKvsR6OM0uWg/giphy.gif" width="30"> Task 1 — FTP Overview Panels

**Goal:** Quick at-a-glance summary of FTP server activity — total events, successful transfers, failed operations, and suspicious activity count.

> 🎯 All four panels are **Single Value** visualizations.

---

### Panel 1.1 — Total FTP Events

**SPL Query:**

```spl
source="ftp_logs.json" host="FTPServer" sourcetype="_json"
| stats count AS "Total FTP Events"
```

**What this does:** Counts every FTP event — baseline metric showing total file transfer activity volume.

---

### Panel 1.2 — Successful Transfers

**SPL Query:**

```spl
source="ftp_logs.json" host="FTPServer" sourcetype="_json" success="true"
| stats count AS "Successful Transfers"
```

**What this does:** Filters for events where the FTP operation completed successfully (reply codes 226, 230). Normal ratio should be high — a sudden drop signals server issues.

---

### Panel 1.3 — Failed Operations

**SPL Query:**

```spl
source="ftp_logs.json" host="FTPServer" sourcetype="_json" success="false"
| stats count AS "Failed Operations"
```

**What this does:** Counts all failed FTP operations — permission denied (550), login incorrect (530), service unavailable (421). High counts indicate:
- Brute-force login attempts (530 errors)
- Unauthorized file access attempts (550 errors)
- Service degradation (421 errors)

> 🔍 **SOC Analyst Tip:** A burst of 530 errors from a single IP = credential brute-force. Cross-reference with SSH logs to check if the same IP is attacking multiple services.

---

### Panel 1.4 — Suspicious Activity

**SPL Query:**

```spl
source="ftp_logs.json" host="FTPServer" sourcetype="_json" classification="Suspicious"
| stats count AS "Suspicious Activity"
```

**What this does:** Counts events involving suspicious file paths (`malware.exe`, `credentials.txt`) or anonymous access — direct indicators of data theft or malware staging.

---

### ✅ Task 1 Result

| Total FTP Events | Successful Transfers | Failed Operations | Suspicious Activity |
|----|----|----|-----|

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/iY8CRBdQXODJSCERIr/giphy.gif" width="30"> Task 2 — FTP Activity Patterns

**Goal:** Identify the most active users and most used FTP commands — essential for establishing normal baselines and detecting insider threats.

---

### Panel 2.1 — Top FTP Users (Bar Chart)

**SPL Query:**

```spl
source="ftp_logs.json" host="FTPServer" sourcetype="_json"
| top limit=10 user
```

**What this does:** Ranks FTP users by activity volume. Red flags:
- `anonymous` user with high activity → public exposure risk
- Service accounts (`backup_svc`) active outside maintenance windows
- Unknown usernames appearing suddenly

> 🔍 **SOC Analyst Tip:** Create an allowlist of expected FTP users. Any username not on the list triggers an alert.

---

### Panel 2.2 — FTP Command Distribution (Pie Chart)

**SPL Query:**

```spl
source="ftp_logs.json" host="FTPServer" sourcetype="_json"
| stats count by command
```

**What this does:** Shows the distribution of FTP commands (RETR, STOR, LIST, DELE, etc.). Normal patterns are dominated by RETR (download) and STOR (upload). Anomalies:
- High **DELE** (delete) count → potential data destruction/ransomware
- High **STOR** for non-upload accounts → possible malware staging
- **RMD/MKD** from unexpected users → unauthorized directory manipulation

---

### ✅ Task 2 Result

| Top FTP Users (Bar Chart) | FTP Command Distribution (Pie Chart) |
|---|---|

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/3oKIPEqDGUULpEU0aQ/giphy.gif" width="30"> Task 3 — Suspicious Transfers & Geo-Location

**Goal:** Drill into suspicious file transfers and map FTP access origins geographically.

---

### Panel 3.1 — Suspicious File Transfers (Statistics Table)

**SPL Query:**

```spl
source="ftp_logs.json" host="FTPServer" sourcetype="_json" classification="Suspicious"
| table ts, id.orig_h, user, command, arg, reply_msg
| sort -ts
```

**What this does:** Creates an investigation-ready table of all suspicious FTP activity — showing when, from where, who, what command, which file, and the server response. This is your primary forensic view for FTP-related incidents.

> 🔍 **SOC Analyst Tip:** Suspicious file paths like `/tmp/malware.exe` or `/sensitive/credentials.txt` combined with external source IPs are immediate escalation triggers.

---

### Panel 3.2 — FTP Access by Source Country (Choropleth Map)

**SPL Query:**

```spl
source="ftp_logs.json" host="FTPServer" sourcetype="_json"
| table id.orig_h
| iplocation id.orig_h
| stats count by Country
| geom geo_countries featureIdField="Country"
```

**SPL Breakdown:**

| Line | Command | Purpose |
|------|---------|---------|
| 1 | `source=...` | Select all FTP events |
| 2 | `\| table id.orig_h` | Extract source IPs |
| 3 | `\| iplocation id.orig_h` | Resolve IPs to countries |
| 4 | `\| stats count by Country` | Aggregate by country |
| 5 | `\| geom geo_countries...` | Map to choropleth visualization |

**What this does:** Creates a world heatmap of FTP access origins. FTP servers should typically only see connections from expected regions — unexpected countries are immediate red flags for unauthorized access.

> ⚠️ **Note:** Internal/RFC1918 IPs won't resolve to geographic locations via `iplocation`.

---

### ✅ Task 3 Result

> Row 3: Suspicious transfer table. Row 4: Geo-location choropleth map.

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🏁 Final Dashboard Layout

| Row | Panels | Visualization Type |
|-----|--------|-------------------|
| **Input Bar** | Time Range + Submit | Input controls |
| **Row 1** | Total FTP Events · Successful Transfers · Failed Operations · Suspicious Activity | 4× Single Value |
| **Row 2** | Top FTP Users · FTP Command Distribution | Bar Chart + Pie Chart |
| **Row 3** | Suspicious File Transfers | Statistics Table (full width) |
| **Row 4** | FTP Access by Source Country | Choropleth Map (full width) |

---

## <img src="https://media2.giphy.com/media/QssGEmpkyEOhBCb7e1/giphy.gif?cid=ecf05e47a0n3gi1bfqntqmob8g9aid1oyj2wr3ds3mg700bl&rid=giphy.gif" width="25"> Complete Simple XML Reference

The full dashboard XML is available at [`xml/ftp_dashboard.xml`](xml/ftp_dashboard.xml). Import it via:

1. **Dashboards** → **Create New Dashboard** → Name it → **Create**
2. Click **Edit** → **Source** → Paste XML → **Save** ✅

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🔑 Key Takeaways for SOC Analysts

| Concept | What You Practiced |
|---------|-------------------|
| **FTP Monitoring** | Building dashboards for file transfer visibility |
| **Anomaly Detection** | Identifying suspicious file paths and unauthorized access patterns |
| **User Behavior Analysis** | Profiling FTP user activity to detect insider threats |
| **Command Analysis** | Understanding FTP command patterns (RETR, STOR, DELE) and their security implications |
| **SPL Commands** | `stats count`, `top`, `table`, `iplocation`, `geom`, `sort` |

---

## 📂 Project Structure

```
splunk-soc-project/
├── FTP_LOG_ANALYSIS.md                ← This file
├── data/
│   └── ftp_logs.json                  ← FTP transfer data (1,200 events)
└── xml/
    └── ftp_dashboard.xml               ← Importable Splunk XML
```

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=14&duration=4000&pause=1000&color=66BB6A&center=true&vCenter=true&repeat=true&width=435&lines=Built+with+%E2%9D%A4%EF%B8%8F+by+Amresh+Kumar;SOC+Analyst+Portfolio+Project;August+2026" alt="Footer" />

![Views](https://komarev.com/ghpvc/?username=aksingh-splunk-ftp&label=Views&color=66BB6A&style=flat-square)

</div>

<div align="center">

[![Back to Main README](https://img.shields.io/badge/%E2%AC%85_Back_to_Main_README-000000?style=for-the-badge)](README.md)

</div>

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=3,10,16,22,28&height=80&section=footer" width="100%" />
