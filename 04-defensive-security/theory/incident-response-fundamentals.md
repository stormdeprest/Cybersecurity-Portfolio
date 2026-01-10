# Incident Response

## What is Incident Response?

**Incident Response** is the structured approach to handling security incidents from detection through resolution, minimizing damage and recovery time.

**Analogy**: Like planning home security (guards, cameras, hidden valuables) AND having a plan for what to do if someone breaks in.

---

## Events, Alerts, and Incidents

### Events
- **Definition**: Logged actions from processes on devices
- **Volume**: Generated continuously in huge numbers
- **Examples**: File access, login attempts, network connections

### Alerts
- **Definition**: Security solution notifications of potentially harmful events
- **Types**:
  - **False Positive**: Alert appears dangerous but is benign
    - *Example*: High data transfer flagged, but it's a legitimate cloud backup
  - **True Positive**: Alert correctly identifies genuine threat
    - *Example*: Phishing email correctly detected

### Incidents
- **Definition**: Confirmed true positive alerts requiring response
- **Severity Levels**: Low → Medium → High → Critical
- **Priority**: Critical incidents responded to first

---

## Types of Security Incidents

### Malware Infections
- Malicious programs damaging systems/networks
- **Sources**: Infected files (documents, executables, scripts)
- **Most common** incident type

### Security Breaches
- Unauthorized access to confidential data
- High priority for businesses protecting sensitive information

### Data Leaks
- Confidential information exposed to unauthorized parties
- **Intentional**: Attackers exfiltrate data
- **Unintentional**: Human error, misconfigurations
- **Impact**: Reputational damage, blackmail, competitive loss

### Insider Attacks
- Threats originating from within organization
- **Example**: Disgruntled employee infecting network via USB
- **Danger**: Insiders have greater access than external attackers

### Denial of Service (DoS) Attacks
- System/network flooded with false requests
- Makes resources unavailable to legitimate users
- Attacks **availability** (one of CIA triad pillars)

**Note**: Severity varies by organization - data leak may devastate one company but barely affect another.

---

## Incident Response Frameworks

### SANS Framework (6 Phases - "PICERL")

| Phase | Description | Example |
|-------|-------------|---------|
| **1. Preparation** | Build resources, teams, plans, security solutions | Employee phishing awareness training |
| **2. Identification** | Monitor for abnormal behavior indicating incidents | Large data transfer detected from compromised host |
| **3. Containment** | Minimize attack impact by isolating affected systems | Isolate infected host from network |
| **4. Eradication** | Remove threat completely from environment | Deep malware scan removes malicious software |
| **5. Recovery** | Restore systems from backup or rebuild | Reconfigure host, restore data from backup |
| **6. Lessons Learned** | Document gaps, improve future response | Post-incident review meeting |

### NIST Framework (4 Phases)

| Phase | SANS Equivalent |
|-------|-----------------|
| **1. Preparation** | Preparation |
| **2. Detection & Analysis** | Identification |
| **3. Containment, Eradication & Recovery** | Containment + Eradication + Recovery |
| **4. Post-Incident Activity** | Lessons Learned |

---

## Incident Response Plan (IRP)

**Definition**: Formal document outlining procedures before, during, and after incidents.

**Key Components:**
- **Roles & Responsibilities** - Who does what
- **Incident Response Methodology** - Framework followed (SANS/NIST)
- **Communication Plan** - Stakeholder notifications, law enforcement contact
- **Escalation Path** - When and how to escalate incidents

**Authorization**: Approved by senior management

---

## Detection & Response Tools

### SIEM (Security Information and Event Management)
- **Function**: Centralized log collection and correlation
- **Purpose**: Identify incidents through event analysis
- **Phase**: Detection/Identification

### AV (Antivirus)
- **Function**: Detect known malware signatures
- **Method**: Regular system scans
- **Limitation**: Only detects known threats

### EDR (Endpoint Detection and Response)
- **Function**: Advanced threat detection on endpoints
- **Capability**: Detection + Containment + Eradication
- **Advantage**: Responds to threats, not just detects

---

## Playbooks vs Runbooks

### Playbooks
**Definition**: High-level guidelines for incident response.

**Example - Phishing Email Playbook:**
1. Notify stakeholders
2. Analyze email headers and body
3. Examine attachments
4. Identify affected users
5. Isolate infected systems
6. Block sender

### Runbooks
**Definition**: Detailed, step-by-step execution instructions for specific tasks.

**Difference**: Playbooks provide strategy; runbooks provide exact commands/actions.

---

## Key Takeaways

- **Incidents** = confirmed true positive alerts
- **Severity matters** - prioritize critical incidents first
- **Frameworks** (SANS/NIST) provide structured response approach
- **Preparation** is critical - build teams, plans, tools BEFORE incidents
- **Documentation** improves future response (Lessons Learned)
- **Tools** (SIEM, AV, EDR) automate detection but require human analysis
- **Playbooks** standardize response procedures