# Security Principles & Models

## CIA Triad (Security Functions)

**CIA** = Confidentiality, Integrity, Availability

### Confidentiality
**Definition**: Only intended recipients can access data.

**Example - Online Shopping**: Credit card number disclosed only to payment processor
**Example - Healthcare**: Medical records kept private per legal requirements

### Integrity
**Definition**: Data cannot be altered; alterations are detectable.

**Example - Online Shopping**: Shipping address cannot be changed by attackers
**Example - Healthcare**: Patient records protected from modification (wrong treatment risk)

### Availability
**Definition**: System/service accessible when needed.

**Example - Online Shopping**: Website/app must function to place orders
**Example - Healthcare**: Medical records accessible during patient visits

---

## Beyond CIA

### Authenticity
**Definition**: Document/data is from claimed source (not fraudulent).

**Example**: Confirm customer actually placed 1000-car order.

### Nonrepudiation
**Definition**: Source cannot deny they originated document/data.

**Example**: Customer cannot deny placing order after shipment.

---

## Parkerian Hexad (6 Security Elements)

**CIA +**
- **Authenticity**
- **Utility**: Information must be in usable form (e.g., encrypted data without key = no utility)
- **Possession**: Protect from unauthorized taking/copying (e.g., ransomware = loss of possession)

---

## DAD Triad (Security Attacks)

**DAD** = Disclosure, Alteration, Destruction/Denial (opposite of CIA)

| Attack | Targets | Example |
|--------|---------|---------|
| **Disclosure** | Confidentiality | Medical records leaked online |
| **Alteration** | Integrity | Patient records modified → wrong treatment |
| **Destruction/Denial** | Availability | Database unavailable → facility cannot function |

**Balance Required**: Extreme confidentiality/integrity restricts availability; extreme availability reduces confidentiality/integrity.

---

## Security Models

### Bell-LaPadula Model (Confidentiality)

**Goal**: Prevent unauthorized information disclosure.

**Rules:**
1. **Simple Security Property** ("no read up"): Lower-level subject cannot read higher-level object
2. **Star Security Property** ("no write down"): Higher-level subject cannot write to lower-level object
3. **Discretionary-Security Property**: Access matrix controls read/write operations

**Summary**: "Write up, read down" - Share info with higher clearance, receive from lower clearance.

**Limitation**: Not designed for file-sharing.

### Biba Model (Integrity)

**Goal**: Prevent unauthorized data modification.

**Rules:**
1. **Simple Integrity Property** ("no read down"): Higher integrity subject cannot read lower integrity object
2. **Star Integrity Property** ("no write up"): Lower integrity subject cannot write to higher integrity object

**Summary**: "Read up, write down" (opposite of Bell-LaPadula).

**Limitation**: Does not handle insider threats.

### Clark-Wilson Model (Integrity)

**Goal**: Maintain data integrity through controlled procedures.

**Concepts:**
- **CDI (Constrained Data Item)**: Data whose integrity must be preserved
- **UDI (Unconstrained Data Item)**: User/system input (beyond CDI)
- **TPs (Transformation Procedures)**: Operations maintaining CDI integrity (read/write)
- **IVPs (Integrity Verification Procedures)**: Validation checks for CDIs

---

## Trust Principles

### Trust but Verify
**Approach**: Trust entities but always verify their behavior.

**Implementation:**
- Logging mechanisms
- Automated security (proxy, IDS/IPS)
- Review logs for anomalies

**Challenge**: Not feasible to verify everything manually.

### Zero Trust
**Philosophy**: "Never trust, always verify" - treat trust as vulnerability.

**Principles:**
- Every entity is adversarial until proven otherwise
- No trust based on location/ownership
- Authentication/authorization required for every resource
- Network microsegmentation (segments as small as single host)

**Benefit**: Breach damage more contained.

**Note**: Balance needed - cannot apply 100% without impacting business.

---

## ISO/IEC 19249 Principles

### Architectural Principles

| Principle | Description |
|-----------|-------------|
| **Domain Separation** | Group related components; assign security attributes per domain (e.g., x86 ring levels) |
| **Layering** | Abstract levels for security policies (e.g., OSI model layers) |
| **Encapsulation** | Hide low-level details; provide APIs (prevents invalid values) |
| **Redundancy** | Ensure availability/integrity (dual power supplies, RAID) |
| **Virtualization** | Share hardware among multiple OS; sandboxing for security |

### Design Principles

| Principle | Description | Example |
|-----------|-------------|---------|
| **Least Privilege** | Minimal permissions to perform task | User needs read → give read only (no write) |
| **Attack Surface Minimization** | Disable unnecessary services/features | Disable unused Linux services during hardening |
| **Centralized Parameter Validation** | Validate all inputs in one library/system | Prevent DoS, RCE via invalid inputs |
| **Centralized Security Services** | Single authentication server (avoid single point of failure) | Centralized auth server with redundancy |
| **Error/Exception Handling** | Design to fail safe; avoid info leakage | Firewall crash → block all traffic (not allow) |

---

## Vulnerability, Threat, Risk

### Vulnerability
**Definition**: Weakness that can be exploited.

**Example**: Database system has known security flaw.

### Threat
**Definition**: Potential danger associated with vulnerability.

**Example**: Proof-of-concept exploit code released for database vulnerability.

### Risk
**Definition**: Likelihood of threat exploiting vulnerability + business impact.

**Example**: Hospital using vulnerable database → assess probability of exploit + patient data breach consequences.

---

## Key Takeaways

- **CIA** = core security functions (Confidentiality, Integrity, Availability)
- **DAD** = attack types targeting CIA
- **Perfect security is impossible** → improve security posture to make attacks harder
- **Bell-LaPadula** focuses on confidentiality; **Biba** focuses on integrity
- **Zero Trust** treats trust as vulnerability → "never trust, always verify"
- **Least Privilege** = give minimum required permissions
- **Fail safe** = system fails securely (firewall crash → block traffic)