# SIEM (Security Information and Event Management)

## The Log Management Problem

### Logs Everywhere
Networks generate massive volumes of logs from multiple sources:
- **Host-centric**: Windows/Linux endpoints, servers (file access, authentication, process execution)
- **Network-centric**: Firewalls, IDS/IPS, routers (SSH, FTP, web traffic, VPN)

### Analysis Challenges

| Challenge | Problem |
|-----------|---------|
| **Numerous Sources** | Hundreds of events per second from scattered devices |
| **No Centralization** | Logs stored locally - requires SSH/RDP to each device |
| **Limited Context** | Individual logs don't reveal full attack chain |
| **Manual Analysis** | Impossible to review all logs - critical events missed |
| **Format Issues** | Different log formats require specialized knowledge |

---

## What is SIEM?

**SIEM** collects logs from all sources, standardizes formats, correlates events, and detects threats using detection rules.

---

## Core SIEM Features

### 1. Centralized Log Collection
- Pulls logs from all sources via agents or APIs
- Single location for all network logs
- No need to access individual machines

### 2. Log Normalization & Parsing
- **Parsing**: Breaking logs into fields (timestamp, user, action, IP)
- **Normalization**: Converting all logs to consistent format
- Windows logs + Linux logs → standardized SIEM format

### 3. Log Correlation
**Example Attack Chain:**
1. User logs in via VPN from new IP
2. User accesses sensitive documents
3. User executes PowerShell script
4. System makes large outbound connection

**Individual assessment**: Each event looks normal
**Correlated assessment**: Potential data exfiltration from compromised credentials

### 4. Real-Time Alerting
- Rules detect malicious patterns
- Default rules + custom analyst-created rules
- Alerts trigger when conditions met
- Analysts investigate within SIEM platform

### 5. Dashboards & Reporting
**Dashboard Components:**
- Alert highlights
- System notifications
- Failed login attempts
- Events ingested count
- Triggered rules
- Top domains visited
- Health alerts

---

## Common Log Sources

### Windows Logs
**Access**: Event Viewer
**Key Feature**: Unique Event IDs for each activity type
**Forwarded to**: SIEM via agents

### Linux Logs
**Common Locations:**
- `/var/log/httpd` - HTTP requests/responses, errors
- `/var/log/cron` - Cron job events
- `/var/log/auth.log` or `/var/log/secure` - Authentication
- `/var/log/kern` - Kernel events

**Example Cron Log:**
```
May 28 13:04:20 ebr crond[2843]: /usr/sbin/crond 4.4 started
Jun 13 07:46:22 ebr crond[3592]: unable to exec /usr/sbin/sendmail
```

### Web Server Logs (Apache)
**Location**: `/var/log/apache` or `/var/log/httpd`

**Example:**
```
192.168.21.200 - - [21/March/2022:10:17:10] "GET /cgi-bin/try/ HTTP/1.0" 200 3395
```

---

## Log Ingestion Methods

| Method | Description |
|--------|-------------|
| **Agent/Forwarder** | Lightweight tool installed on endpoints to capture and send logs |
| **Syslog** | Protocol for real-time data collection from servers, databases |
| **Manual Upload** | Offline data ingestion for quick analysis (Splunk, ELK) |
| **Port Forwarding** | SIEM listens on port, endpoints forward data |

---

## Detection Rules

**Definition**: Logical expressions that trigger alerts when conditions are met.

### Example Rules

**Failed Login Detection:**
```
IF failed_logins >= 5 in 10 seconds
THEN alert "Multiple Failed Login Attempts"
```

**Brute Force Success:**
```
IF successful_login AFTER multiple failed_logins
THEN alert "Successful Login After Multiple Attempts"
```

**Data Exfiltration:**
```
IF outbound_traffic > 25 MB
THEN alert "Potential Data Exfiltration"
```

### Rule Creation Examples

#### Use Case 1: Event Log Clearing
**Scenario**: Attacker removes logs to hide tracks
**Event ID**: 104 (Event log cleared)

**Rule:**
```
IF Log_Source = WinEventLog AND EventID = 104
THEN alert "Event Log Cleared"
```

#### Use Case 2: Whoami Command Detection
**Scenario**: Attacker executes reconnaissance command
**Event ID**: 4688 (Process execution)

**Rule:**
```
IF Log_Source = WinEventLog AND EventID = 4688 AND NewProcessName CONTAINS "whoami"
THEN alert "WHOAMI Command Execution Detected"
```

---

## Alert Investigation Process

### Analyst Workflow
1. **Monitor dashboards** for triggered alerts
2. **Examine events/flows** associated with alert
3. **Check rule conditions** - which were met?
4. **Determine verdict**: True Positive or False Positive

### Post-Investigation Actions

**False Positive:**
- Tune detection rule to reduce noise
- Document exclusions

**True Positive:**
- Conduct deeper investigation
- Contact asset owner about activity
- If confirmed malicious:
  - Isolate infected host
  - Block suspicious IP
  - Escalate to incident response

---

## Key Takeaways

- **SIEM centralizes** scattered logs into single platform
- **Normalization** converts diverse formats into consistent structure
- **Correlation** reveals attack patterns invisible in individual logs
- **Detection rules** automate threat identification
- **Dashboards** provide actionable insights at a glance
- **Field-value pairs** are critical for rule triggering
- **Analysts investigate alerts** to separate true threats from false positives