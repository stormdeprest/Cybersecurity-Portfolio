# SOC (Security Operations Center)

## What is a SOC?

A **Security Operations Center (SOC)** is a dedicated facility operated by a specialized security team that continuously monitors an organization's network and resources to identify suspicious activity and prevent damage.

**Key Characteristics:**
- **24/7/365 operation** - Continuous monitoring
- **Centralized security** - Single location for threat detection
- **Proactive defense** - Prevents threats before damage occurs
- **Specialized team** - Dedicated security professionals

---

## Core SOC Functions

### Detection

**1. Detect Vulnerabilities**
- Identify weaknesses in systems, software, or configurations
- Example: Unpatched Windows systems vulnerable to known exploits
- Note: While not always SOC's primary responsibility, vulnerabilities affect overall security posture

**2. Detect Unauthorized Activity**
- Identify compromised accounts or insider threats
- Example: Employee credentials used from unusual geographic location
- Key indicators: login times, locations, behavioral patterns

**3. Detect Policy Violations**
- Monitor compliance with security policies
- Examples:
  - Downloading pirated software
  - Sending confidential data insecurely
  - Visiting prohibited websites

**4. Detect Intrusions**
- Identify unauthorized system/network access
- Examples:
  - Successful web application exploitation
  - Malware infection from malicious sites
  - Lateral movement within network

### Response

**Incident Response Support:**
- **Minimize impact** - Contain threats quickly
- **Root cause analysis** - Determine how breach occurred
- **Remediation** - Eradicate threats and restore systems
- **Documentation** - Record incidents for future prevention

---

## Three Pillars of SOC

A mature SOC environment requires balance between:
```
┌─────────────────────────────────────┐
│  People + Process + Technology = SOC │
└─────────────────────────────────────┘
```

**People**: Skilled security professionals
**Process**: Structured workflows and procedures
**Technology**: Security tools and solutions

---

## Pillar 1: People (SOC Team Roles)

### SOC Analyst Level 1 (First Responders)
- **Primary function**: First-level alert triage
- **Responsibilities**:
  - Initial analysis of security alerts
  - Determine if detections are harmful
  - Report findings through proper channels
  - Filter false positives

### SOC Analyst Level 2 (Deep Investigation)
- **Primary function**: In-depth analysis
- **Responsibilities**:
  - Detailed investigation of escalated alerts
  - Correlate data from multiple sources
  - Perform advanced threat analysis
  - Support Level 1 with complex cases

### SOC Analyst Level 3 (Threat Hunting & IR)
- **Primary function**: Proactive threat hunting and incident response
- **Responsibilities**:
  - Proactively search for threat indicators
  - Lead incident response activities (containment, eradication, recovery)
  - Handle critical severity incidents
  - Mentor junior analysts

### Security Engineer
- **Primary function**: Tool deployment and maintenance
- **Responsibilities**:
  - Deploy security solutions
  - Configure monitoring tools
  - Ensure smooth operation of security infrastructure
  - Maintain system integrations

### Detection Engineer
- **Primary function**: Rule creation and tuning
- **Responsibilities**:
  - Develop detection rules and logic
  - Fine-tune security solution alerts
  - Reduce false positives
  - Enhance detection capabilities

### SOC Manager
- **Primary function**: Team and process management
- **Responsibilities**:
  - Manage SOC processes and workflows
  - Support team members
  - Report to CISO (Chief Information Security Officer)
  - Communicate security posture updates

**Note**: Team size and roles vary based on organization size and criticality.

---

## Pillar 2: Process (SOC Workflows)

### Alert Triage (The 5 Ws Framework)

**Purpose**: Analyze alerts to determine severity and prioritize response.

**Example Alert**: "Malware detected on Host: GEORGE PC"

| W | Question | Answer |
|---|----------|--------|
| **What?** | What happened? | Malicious file detected on organizational host |
| **When?** | When did it occur? | June 5, 2024 at 13:20 |
| **Where?** | Where did it happen? | Host "GEORGE PC" - specific directory |
| **Who?** | Who was involved? | User: George |
| **Why?** | Why did it happen? | User downloaded pirated software from malicious website |

### Reporting Process

**Requirements:**
- Answer all 5 Ws thoroughly
- Include detailed analysis
- Provide screenshots as evidence
- Escalate via ticketing system
- Assign to appropriate team member

**Purpose:**
- Ensure timely response
- Document incidents
- Enable knowledge sharing
- Support incident tracking

### Incident Response & Forensics

**Incident Response:**
- Triggered for critical/malicious activities
- Structured approach to threat containment
- Involves multiple team levels
- Documented in detailed incident reports

**Digital Forensics:**
- Determine root cause of incidents
- Analyze system/network artifacts
- Collect and preserve evidence
- Support legal proceedings if needed

---

## Pillar 3: Technology (Security Solutions)

### SIEM (Security Information and Event Management)

**Purpose**: Centralized log collection and correlation for threat detection.

**Key Features:**
- Collects logs from multiple sources (firewalls, servers, endpoints)
- Detection rules with logical conditions
- Correlates events across log sources
- Generates alerts based on rule matches
- User Behavior Analytics (UBA)
- Threat intelligence integration
- Machine learning-enhanced detection

**Limitation**: **Detection only** - does not provide automated response

**Examples**: Splunk, IBM QRadar, LogRhythm, Microsoft Sentinel

### EDR (Endpoint Detection and Response)

**Purpose**: Real-time endpoint monitoring with automated response capabilities.

**Key Features:**
- Real-time and historical endpoint visibility
- Detailed activity monitoring per device
- Automated response actions
- Extensive detection capabilities
- Forensic investigation tools
- Process and file analysis

**Advantage**: Combines detection AND response at endpoint level

**Examples**: CrowdStrike Falcon, Carbon Black, SentinelOne

### Firewall

**Purpose**: Network security barrier between internal and external networks.

**Key Features:**
- Monitors incoming/outgoing traffic
- Filters unauthorized connections
- Rule-based traffic blocking
- Intrusion detection capabilities
- Network segmentation
- VPN support

**Function**: First line of defense at network perimeter

### Other Security Solutions

**Antivirus**: Signature-based malware detection
**EPP (Endpoint Protection Platform)**: Comprehensive endpoint security
**IDS/IPS (Intrusion Detection/Prevention System)**: Network-level threat detection
**XDR (Extended Detection and Response)**: Cross-layer threat detection
**SOAR (Security Orchestration, Automation and Response)**: Automated playbook execution

---

## Why Human Analysts Are Essential

Despite automation, human analysts are critical because:

### False Positive Problem

**Scenario**: Fire brigade with centralized alarm system
- Multiple fire alarms trigger simultaneously
- Most caused by cooking smoke (false positives)
- Without human judgment: wasted time and resources
- **Lesson**: Security solutions generate noise - humans filter true threats

### Human Value in SOC:
- **Context understanding** - Distinguish real threats from noise
- **Critical thinking** - Analyze complex scenarios
- **Decision making** - Determine appropriate response
- **Adaptation** - Respond to novel attack techniques
- **Correlation** - Connect seemingly unrelated events

---

## SOC Maturity Model

A mature SOC balances all three pillars:

**Immature SOC:**
- ❌ Tools without skilled operators
- ❌ People without proper processes
- ❌ Processes without supporting technology

**Mature SOC:**
- ✅ Skilled analysts (People)
- ✅ Structured workflows (Process)
- ✅ Integrated security tools (Technology)
- ✅ Continuous improvement culture
- ✅ Proactive threat hunting
- ✅ Efficient incident response

---

## Key Takeaways

- SOC is **24/7 defensive security operation**
- **Detection + Response** are core functions
- **Three pillars** must work together: People, Process, Technology
- **Human analysts** are irreplaceable despite automation
- **Alert triage** uses 5 Ws framework
- **SIEM** provides detection; **EDR** provides detection + response
- **Maturity** comes from balanced pillar development
- SOC protects **confidential data** (secrets) in digital age