# CAPA - Malware Capability Analysis Tool

## What is CAPA?

**CAPA (Common Analysis Platform for Artifacts)** is a static analysis tool developed by FireEye Mandiant that identifies capabilities in executable files without running them.

**Purpose**: Determine what malware can do (network communication, file manipulation, process injection) by analyzing code patterns.

---

## Why CAPA?

**Problem**: Dynamic analysis (running malware) risks compromising your environment.

**Solution**: Static analysis - examine code without execution.

**Advantage**: Encapsulates years of reverse engineering knowledge into automated tool - accessible to non-experts.

---

## Supported File Types

- PE (Portable Executable)
- ELF binaries
- .NET modules
- Shellcode
- Sandbox reports

---

## Basic Usage
```powershell
capa.exe cryptbot.bin
```

### Common Parameters

| Parameter | Description | Example |
|-----------|-------------|---------|
| `-h`, `--help` | Show help | `capa -h` |
| `-v`, `--verbose` | Verbose output | `capa -v malware.bin` |
| `-vv`, `--vverbose` | Very verbose output | `capa -vv malware.bin` |
| `-j` | JSON output | `capa -j -vv malware.bin > output.json` |

---

## CAPA Output Sections

### 1. File Metadata
- **Hashes**: MD5, SHA1, SHA256
- **Analysis type**: Static
- **OS**: Windows, Linux
- **Architecture**: x86, x64
- **Format**: PE, ELF

### 2. MITRE ATT&CK Mapping

**Maps malware behavior to adversary tactics/techniques.**

**Format**: `Tactic::Technique::Technique ID`

**Example**: `Defense Evasion::Obfuscated Files or Information::T1027`

### 3. MAEC (Malware Attribute Enumeration)

**Common Values:**
- **Launcher**: Drops payloads, establishes persistence, connects to C2
- **Downloader**: Downloads/executes additional files

### 4. MBC (Malware Behavior Catalogue)

**Format**: `Objective::Behavior::Method [Identifier]`

**Example**: `ANTI-STATIC ANALYSIS::Executable Code Obfuscation::Stack Strings [B0032.017]`

#### MBC Objectives

| Objective | Description |
|-----------|-------------|
| **Anti-Behavioral Analysis** | Evade sandboxes, debuggers |
| **Anti-Static Analysis** | Obstruct code analysis |
| **Collection** | Gather information |
| **Command and Control** | C2 communication |
| **Defense Evasion** | Bypass detection |
| **Discovery** | System/network reconnaissance |
| **Execution** | Execute unauthorized code |
| **Persistence** | Maintain access |

#### Micro-Objectives (Low-Level)
- **PROCESS**: Create/terminate processes
- **MEMORY**: Allocate/free memory
- **COMMUNICATION**: Network traffic
- **DATA**: String operations, encoding
- **FILE SYSTEM**: Read/write/delete files

### 5. Capability & Namespace

**Capability**: What malware can do (rule name)
**Namespace**: Categorization hierarchy

**Format**: `Capability::Top-Level Namespace/Namespace`

**Example**: `reference anti-VM strings::anti-analysis/anti-vm/vm-detection`

#### Top-Level Namespaces

| TLN | Description |
|-----|-------------|
| **anti-analysis** | Obfuscation, packing, anti-debugging |
| **communication** | Network interactions |
| **data-manipulation** | Encoding, encryption |
| **executable** | PE structure attributes |
| **host-interaction** | File/process operations |
| **impact** | Harm/consequences |
| **persistence** | Maintain access |
| **load-code** | Dynamic code loading |

---

## CAPA Web Explorer

**Purpose**: Visualize CAPA results in user-friendly interface.

### Usage

**1. Generate JSON output:**
```powershell
capa -j -vv malware.bin > output.json
```

**2. Upload to CAPA Web Explorer:**
- Online: https://mandiant.github.io/capa/
- Offline: Included in CAPA distribution

**3. Features:**
- Global search
- Filtering options
- Rule details
- Matched strings/patterns

### Example Analysis

**Capability**: Reference anti-VM strings targeting VMware

**Rule**: `reference-anti-vm-strings-targeting-vmware.yml`

**Matched Feature**: `string: /VMWare/i` (regex match)

**Meaning**: CAPA detected VMware-related strings indicating anti-VM checks

---

## Key Takeaways

- **CAPA** = static analysis tool (no execution required)
- **Rule-based detection** identifies malware capabilities
- **MITRE ATT&CK mapping** links to adversary tactics
- **MBC** provides detailed behavior classification
- **Namespaces** organize capabilities hierarchically
- **Web Explorer** enables visual analysis
- **Verbose modes** (`-v`, `-vv`) provide detailed matches