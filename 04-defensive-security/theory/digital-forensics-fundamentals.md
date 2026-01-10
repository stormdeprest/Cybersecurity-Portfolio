# Digital Forensics

## What is Digital Forensics?

**Digital Forensics** is the application of investigative methods and procedures to collect, examine, analyze, and report on digital evidence from cyber crimes.

**Cyber Crime**: Criminal activity conducted on or using digital devices.

---

## Real-World Example: Bank Robbery Investigation

**Evidence Collected:**
- Digital map of bank (laptop) - robbery planning
- Document with entrance/escape routes (hard drive)
- Document listing security controls and bypass methods (hard drive)
- Photos/videos of previous robberies (laptop)
- Illegal chat groups and call records (mobile phone)

**Result**: Evidence used in legal proceedings for conviction.

---

## Four Phases of Digital Forensics (NIST Framework)

### 1. Collection

**Objective**: Identify and securely collect all relevant digital devices.

**Common Evidence Sources:**
- Personal computers
- Laptops
- Mobile phones
- Digital cameras
- USB drives
- Hard drives
- SD cards

**Critical Requirements:**
- Maintain data integrity (no tampering with original data)
- Document all collected items
- Use proper chain of custody
- Obtain proper authorization

### 2. Examination

**Objective**: Filter and extract relevant data from collected evidence.

**Process:**
- Filter large datasets to focus on relevant information
- Extract data of interest based on:
  - Specific dates/times
  - Particular users
  - File types
  - Keywords

**Example**: 
- Camera contains 1000 photos
- Only need photos from specific date/time
- Filter and extract relevant subset for analysis

### 3. Analysis

**Objective**: Correlate evidence to reconstruct criminal activity chronologically.

**Activities:**
- Connect multiple pieces of evidence
- Establish timeline of events
- Draw conclusions about suspect behavior
- Identify patterns and relationships
- Determine intent and methods

**Critical Phase**: Requires expert interpretation and correlation skills.

### 4. Reporting

**Objective**: Document findings for legal and executive audiences.

**Report Contents:**
- Investigation methodology
- Detailed findings from evidence
- Timeline of events
- Conclusions and interpretations
- Recommendations
- Executive summaries (for non-technical stakeholders)

**Audience**: Law enforcement, prosecutors, executive management

---

## Types of Digital Forensics

### Computer Forensics
- **Focus**: Desktop/laptop computers
- **Most common** type of digital forensics
- **Evidence**: Files, system logs, browsing history, installed software

### Mobile Forensics
- **Focus**: Smartphones and tablets
- **Evidence**: Call records, SMS, GPS locations, app data, contacts

### Network Forensics
- **Focus**: Network infrastructure and traffic
- **Evidence**: Network traffic logs, firewall logs, IDS/IPS alerts, packet captures

### Database Forensics
- **Focus**: Database intrusions and data breaches
- **Evidence**: Database logs, unauthorized queries, data modifications, exfiltration traces

### Cloud Forensics
- **Focus**: Cloud infrastructure (AWS, Azure, GCP)
- **Challenges**: Limited direct evidence access, jurisdiction issues, shared infrastructure
- **Evidence**: Cloud logs, API calls, storage access logs

### Email Forensics
- **Focus**: Email communications
- **Evidence**: Email headers, attachments, metadata, routing information
- **Use Cases**: Phishing investigations, fraud detection, internal investigations

---

## Evidence Acquisition Procedures

### Proper Authorization

**Requirements:**
- Obtain legal authorization before collection
- Search warrants, court orders, or written consent
- Unauthorized collection = inadmissible evidence

**Why Critical:**
- Protects privacy rights
- Ensures legal compliance
- Maintains investigation integrity

### Chain of Custody

**Definition**: Formal document tracking evidence from collection to court presentation.

**Key Information Recorded:**
- Evidence description (name, type, serial number)
- Name of collector
- Date and time of collection
- Storage location
- Access log (who, when, why)
- Transfer records

**Purpose:**
- Proves evidence integrity
- Prevents tampering allegations
- Creates accountability trail
- Ensures admissibility in court

**Example Chain of Custody Entry:**
```
Item: Laptop Dell XPS 15
Serial: ABC123456
Collected by: Detective Jane Smith
Date/Time: 2024-01-10 14:30
Location: Suspect residence
Current Storage: Evidence Locker #7
Accessed by: Forensic Analyst John Doe (2024-01-11 09:00)
Purpose: Disk imaging
```

### Use of Write Blockers

**Purpose**: Prevent any modification to original evidence during acquisition.

**Problem Without Write Blocker:**
- Forensic workstation may alter file timestamps
- Background processes can modify data
- Evidence integrity compromised

**Solution:**
- Hardware or software write blocker
- Allows read-only access
- Blocks ALL write operations
- Maintains evidence in original state

**Types:**
- **Hardware Write Blockers**: Physical devices between storage and workstation
- **Software Write Blockers**: Software-based write protection

---

## Windows Forensics

### Types of Forensic Images

#### 1. Disk Image (Non-Volatile Data)

**Definition**: Bit-by-bit copy of entire storage device.

**Contents:**
- All files (documents, media, applications)
- Deleted files (unallocated space)
- File system metadata
- Internet browsing history
- Registry hives
- System logs

**Persistence**: Data survives system restarts/shutdowns.

#### 2. Memory Image (Volatile Data)

**Definition**: Snapshot of system RAM.

**Contents:**
- Running processes
- Open files
- Network connections
- Encryption keys in memory
- Clipboard contents
- Command history

**Critical**: Must be acquired FIRST before shutdown (data lost on power off).

---

## Windows Forensics Tools

### Acquisition Tools

#### FTK Imager
- **Purpose**: Disk image acquisition and analysis
- **Features**:
  - User-friendly GUI
  - Multiple image formats
  - Preview capabilities
  - Hash verification
- **Use**: Both acquisition and basic analysis

#### DumpIt
- **Purpose**: Memory image acquisition
- **Interface**: Command-line
- **Features**:
  - Fast memory capture
  - Multiple output formats
  - Minimal footprint
- **Use**: Live memory capture

### Analysis Tools

#### Autopsy
- **Type**: Open-source digital forensics platform
- **Purpose**: Comprehensive disk image analysis
- **Features**:
  - Keyword search
  - Deleted file recovery
  - File metadata extraction
  - Extension mismatch detection
  - Timeline analysis
  - Hash database lookups
  - Registry parsing
- **Use**: Primary disk forensics tool

#### Volatility
- **Type**: Open-source memory forensics framework
- **Purpose**: Memory dump analysis
- **Features**:
  - Plugin-based architecture
  - Process analysis
  - Network connection extraction
  - Malware detection
  - Password extraction
- **Supported OS**: Windows, Linux, macOS, Android
- **Use**: Advanced memory forensics

---

## File Metadata Analysis

### PDF Metadata Analysis

**Tool**: `pdfinfo`

**Install (Kali)**: `sudo apt install poppler-utils`

**Example:**
```bash
pdfinfo DOCUMENT.pdf
```

**Metadata Extracted:**
- Creator (application used)
- Producer (PDF generator)
- Creation date/time
- Modification date/time
- Author information
- Page count
- PDF version

**Example Output:**
```
Creator:        Microsoft® Word for Office 365
Producer:       Microsoft® Word for Office 365
CreationDate:   Wed Oct 10 21:47:53 2018 EEST
ModDate:        Wed Oct 10 21:47:53 2018 EEST
Pages:          20
```

**Forensic Value:**
- Identifies software used
- Establishes timeline
- Can reveal author identity
- Detects document manipulation

### Image EXIF Data Analysis

**EXIF**: Exchangeable Image File Format - standard for embedding metadata in images.

**Tool**: `exiftool`

**Install (Kali)**: `sudo apt install libimage-exiftool-perl`

**Example:**
```bash
exiftool IMAGE.jpg
```

**Metadata Extracted:**
- Camera/smartphone model
- Date and time of capture
- GPS coordinates (latitude/longitude)
- Camera settings:
  - Focal length
  - Aperture
  - Shutter speed
  - ISO
- Image dimensions
- Software used for editing

**Example Output:**
```
Camera Model Name: iPhone 13 Pro
Date/Time Original: 2024:01:10 14:30:25
GPS Position: 51 deg 31' 4.00" N, 0 deg 5' 48.30" W
```

**Forensic Value:**
- **Geolocation**: Where photo was taken
- **Timeline**: When photo was taken
- **Device identification**: What device was used
- **Authenticity**: Detect edited/manipulated images

**GPS Coordinate Conversion:**
- Original: `51 deg 31' 4.00" N, 0 deg 5' 48.30" W`
- Map search format: `51°31'4.0"N 0°05'48.3"W`
- Use: Google Maps, Bing Maps for location identification

---

## Key Forensics Principles

### Evidence Integrity
- **Never work on original evidence** - always use copies
- Use write blockers during acquisition
- Generate and verify cryptographic hashes (MD5, SHA-256)
- Document all actions taken

### Legal Admissibility
- Proper authorization required
- Maintain chain of custody
- Follow standard procedures
- Expert testimony may be required

### Volatile vs Non-Volatile Data
- **Volatile**: Memory (RAM) - acquire FIRST
- **Non-Volatile**: Storage devices - acquire after memory

### Order of Volatility (Most to Least Volatile)
1. CPU registers and cache
2. RAM (memory dump)
3. Network connections
4. Running processes
5. Hard disk
6. Backup media
7. Archived data

---

## Best Practices Summary

✅ **Always obtain proper authorization**
✅ **Maintain detailed chain of custody**
✅ **Use write blockers during acquisition**
✅ **Prioritize volatile data (memory first)**
✅ **Create forensic images, not copies**
✅ **Verify integrity with hashes**
✅ **Document every action taken**
✅ **Work on copies, never originals**
✅ **Follow NIST four-phase framework**
✅ **Prepare reports for both technical and non-technical audiences**