# Firewalls

## What is a Firewall?

**Firewall** = Digital security guard that inspects incoming/outgoing network traffic and allows/denies based on rules.

**Purpose**: Prevent unauthorized access to systems and networks.

---

## Firewall Rule Components

| Component | Description | Example |
|-----------|-------------|---------|
| **Source Address** | Originating IP | 192.168.1.100 |
| **Destination Address** | Receiving IP | 10.10.10.10 |
| **Port** | Port number | 80 (HTTP), 443 (HTTPS), 22 (SSH) |
| **Protocol** | Communication protocol | TCP, UDP, ICMP |
| **Action** | What to do with traffic | Allow, Deny, Forward |
| **Direction** | Traffic direction | Inbound, Outbound |

---

## Rule Actions

### Allow
**Definition**: Permit specified traffic.

**Example**: Allow outbound HTTP traffic (port 80)
```
Action: Allow
Source: 192.168.1.0/24
Destination: Any
Protocol: TCP
Port: 80
Direction: Outbound
```

### Deny
**Definition**: Block specified traffic.

**Example**: Deny inbound SSH traffic (port 22) to critical server
```
Action: Deny
Source: Any
Destination: 192.168.1.0/24
Protocol: TCP
Port: 22
Direction: Inbound
```

### Forward
**Definition**: Redirect traffic to different network segment.

**Example**: Forward HTTP traffic to web server
```
Action: Forward
Source: Any
Destination: 192.168.1.8
Protocol: TCP
Port: 80
Direction: Inbound
```

---

## Rule Directionality

**Inbound**: Rules for incoming traffic (e.g., allow HTTP to web server)
**Outbound**: Rules for outgoing traffic (e.g., block SMTP except from mail server)
**Forward**: Rules for traffic redirection within network

---

## Types of Firewalls (OSI Layers)

### Stateless Firewall
**OSI Layers**: 3-4 (Network, Transport)

**Characteristics:**
- Filters packets based on predetermined rules only
- No memory of previous connections
- Each packet evaluated independently
- Fast processing
- Cannot apply complex policies based on connection history

**Limitation**: Denies packets but forgets - future packets from same source treated as new

### Stateful Firewall
**OSI Layers**: 3-4 (Network, Transport)

**Characteristics:**
- Tracks connection state in state table
- Remembers previous connections
- Accepts/denies based on connection history
- Auto-allows future packets from accepted connections
- Auto-denies future packets from denied connections

**Advantage**: Enhanced security through connection awareness

### Proxy Firewall (Application-Level Gateway)
**OSI Layer**: 7 (Application)

**Characteristics:**
- Acts as intermediary between private network and Internet
- Inspects packet contents (not just headers)
- Masks internal IP addresses
- Content filtering policies
- Application control

### Next-Generation Firewall (NGFW)
**OSI Layers**: 3-7 (All layers)

**Characteristics:**
- Deep packet inspection
- Intrusion Prevention System (IPS)
- Heuristic analysis (pattern-based attack blocking)
- SSL/TLS decryption and inspection
- Threat intelligence integration
- Real-time malicious activity blocking

---

## Firewall Comparison Table

| Type | Key Features |
|------|--------------|
| **Stateless** | Basic filtering, no connection tracking, high-speed networks |
| **Stateful** | Pattern recognition, complex rules, connection monitoring |
| **Proxy** | Content inspection, filtering, SSL/TLS decryption, application control |
| **NGFW** | Advanced threat protection, IPS, heuristic analysis, SSL/TLS inspection |

---

## Windows Defender Firewall

### Access
**Start → Type "Windows Defender Firewall"**

### Network Profiles

**Private Networks**: Home network settings
**Guest/Public Networks**: Untrusted networks (coffee shops, airports)
- Block all incoming connections
- Allow only essential outgoing connections

### Custom Rule Creation Example

**Objective**: Block outbound HTTP/HTTPS traffic (ports 80, 443)

**Steps:**
1. Advanced Settings → Outbound Rules → New Rule
2. Rule Type: Custom
3. Program: All programs
4. Protocol: TCP
5. Local Port: Any
6. Remote Port: Specific Ports → `80,443`
7. Action: Block the connection
8. Profile: All networks
9. Name: Block HTTP/HTTPS

**Result**: Cannot browse websites

---

## Linux Firewalls

### Netfilter Framework
**Definition**: Core Linux firewall framework providing packet filtering, NAT, connection tracking.

**Based Utilities:**
- **iptables**: Most widely used, complex syntax
- **nftables**: iptables successor, enhanced capabilities
- **firewalld**: Pre-built network zone configurations

### UFW (Uncomplicated Firewall)

**Purpose**: Beginner-friendly interface for iptables.

#### Basic UFW Commands

**Check status:**
```bash
sudo ufw status
```

**Enable firewall:**
```bash
sudo ufw enable
```

**Disable firewall:**
```bash
sudo ufw disable
```

**Allow all outbound traffic (default policy):**
```bash
sudo ufw default allow outgoing
```

**Deny inbound SSH (port 22):**
```bash
sudo ufw deny 22/tcp
```

**List all rules (numbered):**
```bash
sudo ufw status numbered
```

**Delete rule (by number):**
```bash
sudo ufw delete 2
```

#### UFW Syntax

**General format:**
```bash
sudo ufw [action] [port]/[protocol]
```

**Examples:**
- Allow: `sudo ufw allow 80/tcp`
- Deny: `sudo ufw deny 22/tcp`
- Allow from specific IP: `sudo ufw allow from 192.168.1.100`

---

## Key Takeaways

- **Firewalls** = network traffic control based on rules
- **Stateful > Stateless** for security (connection tracking)
- **NGFW** = most advanced (layers 3-7, IPS, threat intelligence)
- **Windows Defender** = built-in Windows firewall with GUI
- **UFW** = simplified Linux firewall management
- **Rule components**: Source, Destination, Port, Protocol, Action, Direction
- **Actions**: Allow, Deny, Forward