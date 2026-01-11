# IDS (Intrusion Detection System)

## What is IDS?

**IDS** monitors network traffic *after* it passes through the firewall, detecting malicious activities inside the network.

**Analogy**: 
- **Firewall** = Gatekeeper checking people entering building
- **IDS** = Surveillance cameras monitoring activity inside building

**Key Difference from Firewall**: IDS **detects and alerts** but does NOT block traffic.

---

## IDS Deployment Modes

### HIDS (Host-Based IDS)
- **Scope**: Single host
- **Installation**: Individual endpoint
- **Visibility**: Detailed host activity
- **Challenge**: Resource-intensive, difficult to manage at scale

### NIDS (Network-Based IDS)
- **Scope**: Entire network
- **Monitoring**: All network traffic
- **Visibility**: Centralized view of detections
- **Advantage**: Easier management, broader coverage

---

## IDS Detection Modes

### Signature-Based IDS
**Method**: Matches traffic against known attack patterns (signatures) in database.

**Strengths:**
- Detects known threats quickly
- Low false positives
- Fast processing

**Weaknesses:**
- Cannot detect zero-day attacks (no existing signature)
- Only identifies previously seen attacks
- Requires regular signature updates

### Anomaly-Based IDS
**Method**: Learns normal behavior baseline, alerts on deviations.

**Strengths:**
- Detects zero-day attacks
- Identifies novel threats
- No signature database required

**Weaknesses:**
- High false positives (benign unusual activity flagged)
- Requires baseline training period
- Needs fine-tuning to reduce noise

### Hybrid IDS
**Method**: Combines signature-based and anomaly-based detection.

**Approach:**
- Known threats → signature-based detection
- Unknown threats → anomaly-based detection
- Best of both worlds

---

## Snort - Open-Source IDS

**Released**: 1998
**Type**: Signature-based and anomaly-based detection
**License**: Open-source

### Snort Operating Modes

| Mode | Purpose | Use Case |
|------|---------|----------|
| **Packet Sniffer** | Read/display packets without analysis | Network troubleshooting, traffic monitoring |
| **Packet Logging** | Log traffic to PCAP file | Forensic investigation, historical analysis |
| **NIDS** | Real-time intrusion detection | Proactive threat monitoring |

---

## Snort Directory Structure

**Location**: `/etc/snort`

**Key Files:**
- `snort.conf` - Main configuration file
- `rules/` - Rule files directory
- `local.rules` - Custom rules file

**View Snort directory:**
```bash
ls /etc/snort
```

---

## Snort Rule Format

### Rule Structure
```
alert icmp any any -> $HOME_NET any (msg:"Ping Detected"; sid:10001; rev:1;)
```

### Rule Components

| Component | Description | Example |
|-----------|-------------|---------|
| **Action** | What to do when rule triggers | `alert`, `log`, `pass`, `drop` |
| **Protocol** | Protocol to match | `icmp`, `tcp`, `udp`, `ip` |
| **Source IP** | Traffic origin IP | `any`, `192.168.1.0/24`, specific IP |
| **Source Port** | Traffic origin port | `any`, `80`, `1024:65535` |
| **Direction** | Traffic direction | `->` (to), `<>` (bidirectional) |
| **Destination IP** | Traffic destination | `$HOME_NET`, `any`, specific IP |
| **Destination Port** | Target port | `any`, `443`, `1:1024` |
| **Rule Metadata** | Rule details in parentheses | `(msg:"..."; sid:...; rev:...;)` |

### Rule Metadata Fields

**msg**: Alert message displayed when triggered
**sid**: Signature ID (unique identifier)
**rev**: Revision number (increments with each modification)

---

## Snort Usage

### Creating Custom Rules

**Edit local rules file:**
```bash
sudo nano /etc/snort/rules/local.rules
```

**Example rule (detect loopback ping):**
```
alert icmp any any -> 127.0.0.1 any (msg:"Loopback Ping Detected"; sid:10003; rev:1;)
```

**Save**: `Ctrl+X` → `Y`

### Running Snort (Real-Time Detection)
```bash
sudo snort -q -l /var/log/snort -i lo -A console -c /etc/snort/snort.conf
```

**Flags:**
- `-q` - Quiet mode (suppress startup messages)
- `-l` - Log directory
- `-i` - Network interface to monitor
- `-A console` - Alert mode (display to console)
- `-c` - Configuration file

**Test detection:**
```bash
ping 127.0.0.1
```

**Alert output:**
```
07/24-10:46:52.401504 [**] [1:10003:1] Loopback Ping Detected [**] [Priority: 0] {ICMP} 127.0.0.1 -> 127.0.0.1
```

### Analyzing PCAP Files (Forensic Mode)
```bash
sudo snort -q -l /var/log/snort -r /path/to/file.pcap -A console -c /etc/snort/snort.conf
```

**Use Case**: Historical traffic analysis, incident response, forensics

---

## Promiscuous Mode

**Purpose**: Capture all network traffic, not just traffic destined for the host.

**Requirement**: Monitoring entire network (not just local host)

**Note**: Must be enabled on network interface before running Snort for network-wide monitoring.

---

## Key Takeaways

- **IDS detects** (alerts), **firewall blocks** (prevents)
- **NIDS** monitors entire network; **HIDS** monitors single host
- **Signature-based** = known attacks; **Anomaly-based** = zero-days
- **Snort** = most widely used open-source IDS
- **Rules** define what traffic patterns trigger alerts
- **PCAP analysis** enables forensic investigation
- **Custom rules** extend detection beyond defaults