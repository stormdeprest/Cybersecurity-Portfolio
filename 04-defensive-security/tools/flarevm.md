# FlareVM - Malware Analysis Environment

## What is FlareVM?

**FlareVM** is a Windows-based malware analysis toolkit developed by FireEye's FLARE Team.

**Purpose**: Provides comprehensive collection of tools for reverse engineering, malware analysis, incident response, and forensics.

**Target Users**: Malware analysts, incident responders, forensic investigators, penetration testers

---

## Tool Categories

### Reverse Engineering & Debugging
- **Ghidra** - NSA's open-source reverse engineering suite
- **x64dbg** - Debugger for x86/x64 binaries
- **OllyDbg** - Assembly-level debugger
- **Radare2** - Advanced reverse engineering platform

### Disassemblers & Decompilers
- **CFF Explorer** - PE file analysis and editing
- **RetDec** - Machine code decompiler

### Static & Dynamic Analysis
- **Process Hacker** - Memory editor, process monitor
- **PEview** - PE file viewer
- **DIE (Detect It Easy)** - Packer/compiler detection

### Forensics & Incident Response
- **Volatility** - Memory forensics framework
- **FTK Imager** - Disk image acquisition

### Network Analysis
- **Wireshark** - Network protocol analyzer
- **Nmap** - Network mapping, vulnerability detection

### File Analysis
- **HxD** - Hex editor
- **FileInsight** - Binary file analysis

### Sysinternals Suite
- **Autoruns** - Startup program viewer
- **Process Explorer** - Process information
- **Process Monitor** - Real-time activity logging

---

## Essential Tools for Investigation

### Process Monitor (Procmon)

**Purpose**: Real-time system activity monitoring (files, registry, processes, network).

**Usage:**
1. Launch Procmon
2. Filter by process name (Ctrl+L)
3. Monitor file system, registry, network activity

**Example Filter:**
- Process Name → contains → `malware.exe`
- Click "Add" → "Apply"

**Use Case**: Track malware file creation, registry modifications, network connections

### Process Explorer (Procexp)

**Purpose**: Detailed process information (parent-child relationships, DLLs, handles).

**Key Features:**
- View process tree
- Identify parent process
- List loaded DLLs
- Check process ID (PID)

**Workflow:**
1. Open Process Explorer
2. Locate suspicious process
3. Right-click → Properties
4. Check TCP/IP tab for network connections

**Example Output:**
```
cobaltstrike.exe (PID: 4756)
Parent: Explorer.exe
TCP Connection: 47.120.46.210:443
```

### HxD (Hex Editor)

**Purpose**: Examine raw binary data in hexadecimal format.

**Key Feature**: **Data Inspector** - view bytes as different data types (int, float, ASCII).

**Use Case - Magic Number Detection:**
```
Hex: 4D 5A (Little Endian)
Meaning: MZ header = Windows PE executable
```

**Example**: File named `possible_medusa.txt` starts with `4D 5A` → actually an executable

### CFF Explorer

**Purpose**: PE file analysis, hash generation, file integrity verification.

**Key Information:**
- MD5/SHA-1 hashes
- File architecture (32-bit/64-bit)
- Compilation timestamp
- Sections, imports, exports

**Use Case**: Verify file authenticity, detect modified system files

### PEStudio

**Purpose**: Static analysis of PE files without execution.

**Key Indicators:**
- **Entropy** - High value (>7) suggests packing/encryption
- **Imports** - API functions used (blacklisted APIs highlighted)
- **Metadata** - Version info, description, company name
- **Rich Header** - Absence suggests packing/obfuscation

**Suspicious APIs:**
- `CreateRemoteThread` - Process injection
- `WriteProcessMemory` - Code injection
- `CryptoStream` - Encryption (ransomware)
- `set_UseShellExecute` - Execute additional processes

### FLOSS (FLARE Obfuscated String Solver)

**Purpose**: Extract and de-obfuscate strings from malware.

**Usage:**
```powershell
floss.exe malware.exe > output.txt
```

**Output:**
- **Static strings** - Hardcoded strings
- **Stack strings** - Built at runtime
- **Decoded strings** - De-obfuscated strings

**Extracted Artifacts:**
- URLs (C2 servers)
- IP addresses
- File paths
- Registry keys
- API calls

### Wireshark

**Purpose**: Network traffic capture and analysis.

**Use Case**: Identify suspicious connections, protocol analysis, data exfiltration detection.

**Key Info:**
- Source/Destination IPs
- Protocols (HTTP, TLS, DNS)
- Port numbers
- Encrypted traffic (TLSv1.2)

---

## Practical Analysis Workflow

### Example: Analyzing `windows.exe`

#### Step 1: PEStudio (Static Analysis)

**Findings:**
- **Hash**: MD5: `9FDD4767DE5AEC8E577C1916ECC3E1D6`
- **Description**: Claims to be "Windows Registry Editor"
- **Location**: User Downloads (not System32) → Suspicious
- **Version Info**: Russian text → Suspicious for non-Russian org
- **Rich Header**: Absent → Packed/obfuscated
- **Suspicious APIs**:
  - `set_UseShellExecute` - Spawn processes
  - `CryptoStream`, `RijndaelManaged` - AES encryption (ransomware?)

#### Step 2: FLOSS (String Extraction)
```powershell
floss.exe windows.exe > windows.txt
```

**Result**: Confirms suspicious API functions from PEStudio

#### Step 3: Process Explorer (Dynamic Analysis)

**Findings:**
- Parent Process: Explorer.exe (manual execution)
- PID: 4756
- TCP Connection: `47.120.46.210:443`

#### Step 4: Process Monitor (Verification)

**Filter Setup:**
1. Process Name → contains → `windows`
2. Add → Apply

**Confirmed**: Connection to `47.120.46.210` (unknown IP)

---

## Analysis Indicators

### File Legitimacy Red Flags
- ❌ Wrong location (System32 files in Downloads)
- ❌ Foreign language metadata (unexpected region)
- ❌ Missing Rich Header (packing)
- ❌ High entropy (>7.0)
- ❌ Suspicious description mismatch

### Behavioral Red Flags
- ❌ Spawns additional processes
- ❌ Connects to unknown IPs
- ❌ Uses crypto APIs (unexpected encryption)
- ❌ Modifies registry (Autoruns)
- ❌ Injects code (CreateRemoteThread)

---

## Key Takeaways

- **FlareVM** = Windows malware analysis toolkit
- **Process Explorer** shows process relationships + network connections
- **Process Monitor** tracks real-time file/registry/network activity
- **HxD** reveals file magic numbers (MZ header = PE executable)
- **PEStudio** identifies suspicious APIs without execution
- **FLOSS** extracts obfuscated strings from malware
- **Layered approach** = Use multiple tools to verify findings
- **Static → Dynamic** = Analyze before execution, then monitor runtime behavior