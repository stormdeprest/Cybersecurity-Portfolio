# Log Analysis

## What are Logs?

**Logs** are digital footprints recording all system and application activities - both normal and malicious.

**Analogy**: Like physical traces at a crime scene (footprints, damaged door, CCTV footage), logs help investigators reconstruct digital attacks.

---

## Use Cases of Logs

| Use Case | Purpose |
|----------|---------|
| **Security Event Monitoring** | Detect anomalous behavior in real-time |
| **Incident Investigation & Forensics** | Root cause analysis of security incidents |
| **Troubleshooting** | Diagnose and fix system/application errors |
| **Performance Monitoring** | Analyze application performance metrics |
| **Auditing & Compliance** | Establish activity trails for regulatory requirements |

---

## Types of Logs

| Log Type | Purpose | Examples |
|----------|---------|----------|
| **System Logs** | OS troubleshooting | Startup/shutdown, driver loading, hardware errors |
| **Security Logs** | Incident detection & investigation | Authentication, authorization, policy changes, abnormal activity |
| **Application Logs** | Application-specific events | User interactions, updates, errors |
| **Audit Logs** | Compliance & security monitoring | Data access, system changes, user activity |
| **Network Logs** | Network troubleshooting & security | Traffic (incoming/outgoing), connections, firewall logs |
| **Access Logs** | Resource access tracking | Web server, database, API access |

---

## Windows Event Logs

### Log Categories

**Application**: Application errors, warnings, compatibility issues
**System**: Driver issues, hardware events, startup/shutdown, services
**Security**: Authentication, account changes, security policy modifications (most critical for security)

### Event Viewer Tool

**Access**: Start → Type "Event Viewer"

**Key Fields:**
- **Description** - Detailed activity information
- **Log Name** - Log file identifier
- **Logged** - Timestamp
- **Event ID** - Unique identifier for specific activity type

### Important Event IDs

| Event ID | Description |
|----------|-------------|
| 4624 | Successful login |
| 4625 | Failed login attempt |
| 4634 | Successful logoff |
| 4720 | User account created |
| 4724 | Password reset attempt |
| 4722 | User account enabled |
| 4725 | User account disabled |
| 4726 | User account deleted |

### Filtering Logs

**Steps:**
1. Select log file (Windows Logs → Security)
2. Click "Filter Current Log"
3. Enter Event ID (e.g., 4624)
4. View filtered results

---

## Web Server Access Logs

### Log Location (Apache)
```
/var/log/apache2/access.log
```

### Log Fields

**Example Log Entry:**
```
172.16.0.1 - - [06/Jun/2024:13:58:44] "GET / HTTP/1.1" 200 "-" "Mozilla/5.0..."
```

**Field Breakdown:**
- **IP Address**: `172.16.0.1` - User making request
- **Timestamp**: `[06/Jun/2024:13:58:44]` - Request time
- **HTTP Method**: `GET` - Action type
- **URL**: `/` - Requested resource
- **Status Code**: `200` - Server response (200=success, 404=not found, 500=error)
- **User-Agent**: Browser/OS information

---

## Linux Log Analysis Commands

### cat - Display File Contents
```bash
cat access.log
```

**Combine multiple logs:**
```bash
cat access1.log access2.log > combined_access.log
```

### grep - Search for Patterns
```bash
grep "192.168.1.1" access.log
```

**Output**: All lines containing the searched IP address

### less - Page-by-Page Viewing
```bash
less access.log
```

**Navigation:**
- `Space` - Next page
- `b` - Previous page
- `/pattern` - Search for pattern
- `n` - Next occurrence
- `N` - Previous occurrence

---

## Log Analysis Approach

**Challenge**: Logs contain enormous amounts of data - manual review is impractical

**Solution**: Segregate logs by category, then filter/search

**Example Workflow:**
1. Identify relevant log type (Security logs for logins)
2. Filter by Event ID or pattern
3. Focus on specific timeframe
4. Correlate multiple log sources

---

## Key Takeaways

- **Logs = digital crime scene evidence**
- **Segregation** by type enables efficient analysis
- **Event IDs** (Windows) identify specific activities
- **Manual analysis** uses command-line tools (cat, grep, less)
- **Filtering** is essential due to log volume
- **Security logs** are most critical for incident investigation