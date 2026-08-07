<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=2,11,20,25,30&height=180&section=header&text=Web%20Traffic%20Analysis&fontSize=32&fontColor=ffffff&animation=fadeIn&fontAlignY=35&desc=Apache%20%7C%20HTTP%20%7C%20Status%20Codes&descSize=14&descAlignY=55&descColor=F7DF1E" width="100%" />

<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=28&duration=3000&pause=1000&color=F7DF1E&center=true&vCenter=true&multiline=true&repeat=true&width=800&height=100&lines=%F0%9F%8C%90+Splunk+SIEM+Dashboard;Web+Traffic+Log+Analysis+%7C+Apache+Logs" alt="Typing SVG" />

![Splunk](https://img.shields.io/badge/Splunk-000000?style=for-the-badge&logo=splunk&logoColor=white)
![Apache](https://img.shields.io/badge/Apache-D22128?style=for-the-badge&logo=apache&logoColor=white)
![SIEM](https://img.shields.io/badge/SIEM-Dashboard-blue?style=for-the-badge)
![SOC](https://img.shields.io/badge/SOC-Analyst-red?style=for-the-badge)
![HTTP](https://img.shields.io/badge/HTTP-Traffic_Analysis-green?style=for-the-badge)

</div>

> **Project Type:** SOC Analyst Lab — SIEM Dashboard Building  
> **Platform:** Splunk Enterprise / Splunk Cloud  
> **Data Source:** `apache_mixed_access_full (1).json`  
> **Skill Level:** Beginner → Intermediate

## 📸 Completed Dashboard

![Web Traffic Analysis Dashboard](screenshots/web-traffic-dashboard.png)

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 📋 Table of Contents

| #   | Section                                                        | Status |
| --- | -------------------------------------------------------------- | ------ |
| 0   | [Lab Setup & Prerequisites](#lab-setup--prerequisites)         | ⬜      |
| 1   | [Task 0 — Time Range Input](#task-0--setting-up-time-range)    | ⬜      |
| 2   | [Task 1 — Web Activities](#task-1--web-activities)             | ⬜      |
| 3   | [Task 2 — Web Stats](#task-2--web-stats)                       | ⬜      |
| 4   | [Task 3 — Geo-Location Map](#task-3--web-traffic-by-client-ip-addresses) | ⬜      |
| 5   | [Final Dashboard Layout](#final-dashboard-layout)              | ⬜      |

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Lab Setup & Prerequisites

### What You Need

| Requirement            | Details                                                                        |
| ---------------------- | ------------------------------------------------------------------------------ |
| **Splunk Instance**    | Splunk Enterprise (local) or Splunk Cloud (free trial works)                   |
| **Data File**          | `apache_mixed_access_full (1).json` → host `webserver`                         |
| **Sourcetype**         | `_json`                                                                         |
| **Geo Lookup**         | `iplocation` command + built-in `geo_countries` lookup (ships with Splunk)      |

### Data Ingestion

1. **Upload `apache_mixed_access_full (1).json`**
   - Settings → Add Data → Upload → select the file
   - Set **Host** = `webserver`, **Sourcetype** = `_json`
   - Review & Submit

2. **Verify ingestion:**
   ```spl
   source="apache_mixed_access_full (1).json" host="webserver" | head 10
   ```

### Create the Dashboard

1. Go to **Dashboards** → **Create New Dashboard**
2. Name it **Web Traffic Analysis Dashboard**
3. Select **Classic Dashboard** (Simple XML)
4. Choose **Absolute** layout
5. Click **Create**

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/WUlplcMpOCEmTGBtBW/giphy.gif" width="30"> Task 0 — Setting Up Time Range

**Why:** A single shared time picker ensures all panels update together when the analyst changes the time window.

### Step-by-Step

#### 1. Add Time Range Input

| # | Action |
|---|--------|
| 1 | Inside the dashboard editor, click **`+ Add Input`** (top bar) |
| 2 | Select **Time** from the dropdown |
| 3 | Click the **✏️ pencil icon** on the newly added time picker |
| 4 | Set **Label** → `Time Range` |
| 5 | Set **Token** → `time_range` |
| 6 | *(Optional)* Set a **Default** value — e.g. `Last 24 hours` |
| 7 | Click **Apply** |

#### 2. Add Submit Button

| # | Action |
|---|--------|
| 1 | Click **`+ Add Input`** again |
| 2 | Select **Submit** |

> ⚠️ **Important:** For **every panel** below, set its time range to the **Shared Time Picker (`time_range`)** token.

### Resulting Simple XML (Reference)

```xml
<input type="time" token="time_range">
  <label>Time Range</label>
  <default>
    <earliest>-24h@h</earliest>
    <latest>now</latest>
  </default>
</input>
```

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/VgCDAzcKvsR6OM0uWg/giphy.gif" width="30"> Task 1 — Web Activities

**Goal:** Provide a quick, at-a-glance summary of web server activity — total requests, successes, client errors, and server errors.

> 🎯 All four panels in this task are **Single Value** visualizations.

---

### Panel 1.1 — Total Web Requests

| Setting          | Value                           |
| ---------------- | ------------------------------- |
| **Panel Type**   | Single Value                    |
| **Time Picker**  | Shared Time Picker `time_range` |
| **Content Title**| Total Web Requests              |

**Steps:**

1. Click **`+ Add Panel`**
2. Under **New**, choose **Single Value**
3. Set **Time Range** → Use Shared Time Picker (`time_range`)
4. Set **Content Title** → `Total Web Requests`
5. Paste the search string below and click **Apply**

**SPL Query:**

```spl
source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json"
| stats count AS "Total Web Requests"
```

**What this does:**  
Counts every event from the Apache access log — the baseline metric showing total HTTP request volume in the selected time window.

---

### Panel 1.2 — Successful Responses

| Setting          | Value                           |
| ---------------- | ------------------------------- |
| **Panel Type**   | Single Value                    |
| **Time Picker**  | Shared Time Picker `time_range` |
| **Content Title**| Successful Responses            |

**Steps:**

1. Click **`+ Add Panel`**
2. Under **New**, choose **Single Value**
3. Set **Time Range** → Use Shared Time Picker (`time_range`)
4. Set **Content Title** → `Successful Responses`
5. Paste the search string below and click **Apply**

**SPL Query:**

```spl
source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json" method=GET status=200
| stats count AS "Successful Responses"
```

**What this does:**  
Filters for HTTP GET requests that returned status `200 OK` — the count of successfully served pages. A sudden drop signals potential availability issues.

---

### Panel 1.3 — Client Errors (4xx)

| Setting          | Value                           |
| ---------------- | ------------------------------- |
| **Panel Type**   | Single Value                    |
| **Time Picker**  | Shared Time Picker `time_range` |
| **Content Title**| Client Errors                   |

**Steps:**

1. Click **`+ Add Panel`**
2. Under **New**, choose **Single Value**
3. Set **Time Range** → Use Shared Time Picker (`time_range`)
4. Set **Content Title** → `Client Errors`
5. Paste the search string below and click **Apply**

**SPL Query:**

```spl
source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json"
| where status>=400 AND status<500
| stats count AS "Client Errors"
```

**What this does:**  
Counts all 4xx HTTP responses (400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, etc.). High 4xx counts can indicate:
- Scanners probing for vulnerable endpoints (404s)
- Brute-force login attempts (401s)
- WAF blocks or misconfigured access controls (403s)

> 🔍 **SOC Analyst Tip:** A spike in 401/403 errors from a single IP is a strong indicator of credential stuffing or directory traversal attacks.

---

### Panel 1.4 — Server Errors (5xx)

| Setting          | Value                           |
| ---------------- | ------------------------------- |
| **Panel Type**   | Single Value                    |
| **Time Picker**  | Shared Time Picker `time_range` |
| **Content Title**| Server Errors (5xx)             |

**Steps:**

1. Click **`+ Add Panel`**
2. Under **New**, choose **Single Value**
3. Set **Time Range** → Use Shared Time Picker (`time_range`)
4. Set **Content Title** → `Server Errors (5xx)`
5. Paste the search string below and click **Apply**

**SPL Query:**

```spl
source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json"
| where status>=500
| stats count AS "Server Errors"
```

**What this does:**  
Counts all 5xx HTTP responses (500 Internal Server Error, 502 Bad Gateway, 503 Service Unavailable, etc.). These indicate server-side failures — could be caused by application crashes, resource exhaustion, or an active DDoS attack.

> ⚠️ **Note:** The original lab guide had the same `status>=400 AND status<500` filter here (copy of Client Errors). I've corrected it to `status>=500` to properly capture 5xx server errors.

> 🔍 **SOC Analyst Tip:** A sudden surge in 500/503 errors, especially combined with high traffic from few IPs, is a classic DDoS signature.

---

### ✅ Task 1 Result

After completing Task 1, your dashboard should show 4 Single Value panels in Row 1:

| Total Web Requests | Successful Responses | Client Errors (4xx) | Server Errors (5xx) |
|----|----|----|-----|

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/iY8CRBdQXODJSCERIr/giphy.gif" width="30"> Task 2 — Web Stats

**Goal:** Visualize the most requested URIs and the most active client IPs — essential for understanding traffic patterns and identifying suspicious behavior.

---

### Panel 2.1 — Top Requested URIs (Bar Chart)

| Setting          | Value                           |
| ---------------- | ------------------------------- |
| **Panel Type**   | Bar Chart                       |
| **Time Picker**  | Shared Time Picker `time_range` |
| **Content Title**| Top Requested URIs              |

**Steps:**

1. Click **`+ Add Panel`**
2. Under **New**, choose **Bar Chart**
3. Set **Time Range** → Use Shared Time Picker (`time_range`)
4. Set **Content Title** → `Top Requested URIs`
5. Paste the search string below and click **Apply**

**SPL Query:**

```spl
source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json"
| stats count AS "Hits" by uri
```

**What this does:**  
Aggregates HTTP requests by URI path and displays them as a bar chart. Lets you instantly identify:
- The most visited pages (normal traffic pattern)
- Unusual URIs being probed (e.g. `/admin`, `/wp-login.php`, `/.env`, `/phpmyadmin`)

> 🔍 **SOC Analyst Tip:** URIs like `/wp-admin`, `/shell.php`, `/../../../etc/passwd` appearing in the top list are immediate red flags for web application attacks (scanning, LFI, webshell uploads).

---

### Panel 2.2 — Top Users by IP Address (Bar Chart)

| Setting          | Value                             |
| ---------------- | --------------------------------- |
| **Panel Type**   | Bar Chart                         |
| **Time Picker**  | Shared Time Picker `time_range`   |
| **Content Title**| Top Users by IP Address           |

**Steps:**

1. Click **`+ Add Panel`**
2. Under **New**, choose **Bar Chart**
3. Set **Time Range** → Use Shared Time Picker (`time_range`)
4. Set **Content Title** → `Top Users by IP Address`
5. Paste the search string below and click **Apply**

**SPL Query:**

```spl
source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json"
| stats count AS IP by ip
```

**What this does:**  
Ranks client IP addresses by request count. A single IP generating significantly more traffic than others may indicate:
- A bot/scraper
- A DDoS source
- An attacker performing automated scanning

> 🔍 **SOC Analyst Tip:** Cross-reference top IPs with threat intelligence (AbuseIPDB, VirusTotal) and check if the request patterns are consistent with legitimate user behavior or automated tools.

---

### ✅ Task 2 Result

After completing Task 2, your dashboard should have Row 2 with two side-by-side Bar Charts:

| Top Requested URIs (Bar Chart) | Top Users by IP Address (Bar Chart) |
|---|---|

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## <img src="https://media.giphy.com/media/3oKIPEqDGUULpEU0aQ/giphy.gif" width="30"> Task 3 — Web Traffic by Client IP Addresses

**Goal:** Map web traffic origins on a world choropleth to visualize geographic distribution — critical for identifying anomalous traffic patterns and potential geo-blocking decisions.

---

### Panel 3.1 — Web Traffic by Client IP Addresses (Choropleth Map)

| Setting          | Value                                       |
| ---------------- | ------------------------------------------- |
| **Panel Type**   | Choropleth Map                              |
| **Time Picker**  | Shared Time Picker `time_range`              |
| **Content Title**| Web Traffic by Client IP Addresses          |

**Steps:**

1. Click **`+ Add Panel`**
2. Under **New**, choose **Choropleth Map**
3. Set **Time Range** → Use Shared Time Picker (`time_range`)
4. Set **Content Title** → `Web Traffic by Client IP Addresses`
5. Paste the search string below and click **Apply**

**SPL Query:**

```spl
source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json" method=GET
| table ip
| iplocation ip
| stats count by Country
| geom geo_countries featureIdField="Country"
```

**SPL Breakdown (line by line):**

| Line | Command | Purpose |
|------|---------|---------|
| 1 | `source=... method=GET` | Filter to GET requests only |
| 2 | `\| table ip` | Extract just the client IP field |
| 3 | `\| iplocation ip` | Resolve each IP to Country, City, lat/lon using Splunk's built-in MaxMind GeoIP database |
| 4 | `\| stats count by Country` | Aggregate: how many requests originated from each country |
| 5 | `\| geom geo_countries featureIdField="Country"` | Map the country names to the `geo_countries` lookup for choropleth rendering |

**What this does:**  
Creates a world heatmap where countries are shaded by web traffic volume. Darker shading = more requests from that region. This helps identify:
- Where your legitimate user base is located
- Unusual traffic from unexpected regions
- Potential geo-blocking candidates for malicious traffic

> ⚠️ **Prerequisites for this panel:**
> - Splunk's `iplocation` command requires the MaxMind GeoIP database (ships with Splunk Enterprise by default)
> - The `geo_countries` lookup must be available (built-in with Splunk)
> - Private/RFC1918 IPs (10.x, 172.16.x, 192.168.x) will return no location data

---

### ✅ Task 3 Result

After completing Task 3, your dashboard should have Row 3 with a full-width Choropleth Map showing web traffic origins by country.

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🏁 Final Dashboard Layout

### Row Structure Summary

| Row | Panels | Visualization Type |
|-----|--------|--------------------|
| **Input Bar** | Time Range + Submit | Input controls |
| **Row 1** | Total Web Requests · Successful Responses · Client Errors · Server Errors | 4× Single Value |
| **Row 2** | Top Requested URIs · Top Users by IP Address | 2× Bar Chart |
| **Row 3** | Web Traffic by Client IP Addresses | Choropleth Map (full width) |

---

## <img src="https://media2.giphy.com/media/QssGEmpkyEOhBCb7e1/giphy.gif?cid=ecf05e47a0n3gi1bfqntqmob8g9aid1oyj2wr3ds3mg700bl&rid=giphy.gif" width="25"> Complete Simple XML Reference

Below is the full dashboard XML you can import directly into Splunk:

```xml
<form>
  <label>Web Traffic Analysis Dashboard</label>
  <description>SOC Analyst Dashboard — Apache Web Traffic Monitoring &amp; Analysis</description>

  <!-- ==================== INPUT: Time Range ==================== -->
  <fieldset submitButton="true">
    <input type="time" token="time_range">
      <label>Time Range</label>
      <default>
        <earliest>-24h@h</earliest>
        <latest>now</latest>
      </default>
    </input>
  </fieldset>

  <!-- ==================== ROW 1: Web Activities ==================== -->
  <row>
    <panel>
      <title>Total Web Requests</title>
      <single>
        <search>
          <query>source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json"
| stats count AS "Total Web Requests"</query>
          <earliest>$time_range.earliest$</earliest>
          <latest>$time_range.latest$</latest>
        </search>
      </single>
    </panel>

    <panel>
      <title>Successful Responses</title>
      <single>
        <search>
          <query>source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json" method=GET status=200
| stats count AS "Successful Responses"</query>
          <earliest>$time_range.earliest$</earliest>
          <latest>$time_range.latest$</latest>
        </search>
      </single>
    </panel>

    <panel>
      <title>Client Errors</title>
      <single>
        <search>
          <query>source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json"
| where status&gt;=400 AND status&lt;500
| stats count AS "Client Errors"</query>
          <earliest>$time_range.earliest$</earliest>
          <latest>$time_range.latest$</latest>
        </search>
      </single>
    </panel>

    <panel>
      <title>Server Errors (5xx)</title>
      <single>
        <search>
          <query>source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json"
| where status&gt;=500
| stats count AS "Server Errors"</query>
          <earliest>$time_range.earliest$</earliest>
          <latest>$time_range.latest$</latest>
        </search>
      </single>
    </panel>
  </row>

  <!-- ==================== ROW 2: Web Stats ==================== -->
  <row>
    <panel>
      <title>Top Requested URIs</title>
      <chart>
        <search>
          <query>source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json"
| stats count AS "Hits" by uri</query>
          <earliest>$time_range.earliest$</earliest>
          <latest>$time_range.latest$</latest>
        </search>
        <option name="charting.chart">bar</option>
      </chart>
    </panel>

    <panel>
      <title>Top Users by IP Address</title>
      <chart>
        <search>
          <query>source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json"
| stats count AS IP by ip</query>
          <earliest>$time_range.earliest$</earliest>
          <latest>$time_range.latest$</latest>
        </search>
        <option name="charting.chart">bar</option>
      </chart>
    </panel>
  </row>

  <!-- ==================== ROW 3: Geo-Location Visualization ==================== -->
  <row>
    <panel>
      <title>Web Traffic by Client IP Addresses</title>
      <map>
        <search>
          <query>source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json" method=GET
| table ip
| iplocation ip
| stats count by Country
| geom geo_countries featureIdField="Country"</query>
          <earliest>$time_range.earliest$</earliest>
          <latest>$time_range.latest$</latest>
        </search>
        <option name="mapping.type">choropleth</option>
        <option name="mapping.choroplethLayer.colorMode">auto</option>
      </map>
    </panel>
  </row>

</form>
```

### How to Import This XML

1. Go to **Dashboards** → **Create New Dashboard**
2. Name it → Click **Create**
3. Click **Edit** → Click **Source** (top-left toggle)
4. Replace all existing XML with the XML block above
5. Click **Save**
6. Done ✅ — all 7 panels + time picker are ready

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🔑 Key Takeaways for SOC Analysts

| Concept | What You Practiced |
|---------|--------------------|
| **HTTP Status Code Analysis** | Categorizing traffic by 2xx (success), 4xx (client errors), 5xx (server errors) |
| **URI Pattern Analysis** | Identifying most-requested endpoints to spot scanning/attack patterns |
| **IP-Based Attribution** | Ranking client IPs by request volume to detect bots/scanners |
| **Geo-Intelligence** | Mapping traffic origins to countries for anomaly detection |
| **SPL Commands** | `stats count`, `where`, `table`, `iplocation`, `geom` |

---

## 📂 Project Structure

```
splunk-soc-project/
├── README.md                              ← SSH Logs Dashboard guide
├── WEB_TRAFFIC_DASHBOARD.md               ← This file (Web Traffic guide)
├── screenshots/
│   ├── dashboard-complete.png             ← SSH dashboard screenshot
│   └── web-traffic-dashboard.png          ← Web Traffic dashboard screenshot
├── data/
│   ├── ssh_logs_new.json                  ← SSH log data (1,201 events)
│   └── apache_logs.json                   ← Apache web traffic data (2,000 events)
└── xml/
    ├── ssh_dashboard.xml                  ← SSH dashboard XML
    └── web_traffic_dashboard.xml          ← Web Traffic dashboard XML
```

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=14&duration=4000&pause=1000&color=F7DF1E&center=true&vCenter=true&repeat=true&width=435&lines=Built+with+%E2%9D%A4%EF%B8%8F+by+Amresh;SOC+Analyst+Portfolio+Project;July+2026" alt="Footer" />

![Views](https://komarev.com/ghpvc/?username=aksingh-splunk-web&label=Views&color=F7DF1E&style=flat-square)

</div>

<div align="center">

[![Back to Main README](https://img.shields.io/badge/%E2%AC%85_Back_to_Main_README-000000?style=for-the-badge)](README.md)

</div>

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=2,11,20,25,30&height=80&section=footer" width="100%" />
