# Metasploit Framework

## Overview

Metasploit works via `msfconsole`, where you use different modules to scan, exploit, brute-force, or perform post-exploitation.

## Key Concepts

- **Vulnerability** - Error or flaw in a system
    
- **Exploit** - Code that abuses that flaw
    
- **Payload** - What you execute on the target (e.g., shell)
    

## Module Types

|Module Type|Description|
|---|---|
|**Auxiliary**|Scanners, fuzzers, utility tools|
|**Exploits**|Code to attack vulnerabilities|
|**Payloads**|What you execute after an exploit (singles, stagers, stages)|
|**Encoders**|Encode payloads to reduce detection|
|**Evasion**|Designed to bypass antivirus|
|**NOPs**|Padding to make payloads run stably|
|**Post**|Modules for post-exploitation|

## Payload Types

## Adapters

Adapters wrap a single payload in a different format.

Example: A normal payload converted to a single PowerShell command that performs the same action.

## Singles

Singles are standalone payloads: everything is in one piece of code.

**Examples:** Add user, open notepad.exe, simple reverse shell

They don't need to download anything extra.

## Stagers

Stagers first establish a small communication channel between you and the target.

Used for staged payloads and keep the initial payload small (useful for antivirus evasion or buffer limitations).

## Stages

Stages are downloaded after the stager.

Contains the full functionality: larger shells, advanced backdoors, Meterpreter, etc.

**Summary:**

- **Singles** = everything in one
    
- **Stagers + Stages** = small part first → large part later
    
- **Adapters** = packaging/format converters
    

## Basic Commands

## Start Metasploit

`msfconsole`

## Linux-like Commands (within msfconsole)

`ls ping -c 1 <IP> clear`

⚠️ Output redirection (>) does not work in msfconsole.

## Help & History

`help`

`help mmand>`

`history`

## Search & Select Modules

**Search modules:**

`search <term>`

**Examples:**

`search ms17-010`

`search type:auxiliary telnet`

**Select module:**

`use <module>`

`use <number>`

**Example:**

`use exploit/windows/smb/ms17_010_eternalblue`

## Module Information

`show options`

`show payloads`

`show <module_type>`

`info`

`info <module-path>`

## Module Settings

`set <option> <value>`

`setg <option> <value>`

`unset <option>`

`unsetg <option>`

**Examples:**

`set RHOSTS 192.168.1.10`

`setg LHOST 10.0.0.5`

- `set` - Sets option for current module only
    
- `setg` - Sets global option (remains active when switching modules)
    

## Execute Exploits

`run`

`exploit`

`exploit -z`

- `run` / `exploit` - Start the exploit/module
    
- `exploit -z` - Execute exploit and immediately background the session
    

## Test Vulnerability

`check`

Tests if a target is vulnerable without actually exploiting it. Only available for modules that support this.

## Exit Module

`back`

Exits current module (returns to main menu).

## Sessions Management

When an exploit succeeds, you get a **session** (e.g., Meterpreter).

A session = communication channel between Metasploit and the target.

## Background Session

**From Meterpreter:**

`background`

**Via keyboard:**

`CTRL + Z`

## View Sessions

`sessions`

`sessions -l`

Shows all active sessions with ID, type, and connection information.

## Interact with Session

`sessions -i <id>`

**Example:**

`sessions -i 2`

## Kill Session

**During interaction:**

`CTRL + C`

## Port Scanning

## Find Port Scan Modules

`search portscan`

## Use TCP Port Scanner

**Step 1: Select module**

`use auxiliary/scanner/portscan/tcp`

**Step 2: View options**

`show options`

**Step 3: Configure**

`set RHOSTS [target_ip] set PORTS 1-10000 set THREADS 10 set CONCURRENCY 10`

**Step 4: Run**

`run`

## Important Options

- **RHOSTS** - Target IP or network
    
- **PORTS** - Port range (e.g., 1-10000, 22-25,80,110-900)
    
- **THREADS** - Number of concurrent threads
    
- **CONCURRENCY** - Number of simultaneous targets
    

## Nmap from Metasploit

`nmap -sS [target_ip]`

## UDP Service Scan

`use auxiliary/scanner/discovery/udp_sweep set RHOSTS [target_ip] run`

## SMB Scanning

`use auxiliary/scanner/smb/smb_version set RHOSTS [target_ip] run`

**Other useful SMB modules:**

`auxiliary/scanner/smb/smb_enumshares`

## Common Port Scan Types

- `auxiliary/scanner/portscan/syn` - TCP SYN Scanner
    
- `auxiliary/scanner/portscan/tcp` - TCP Scanner
    
- `auxiliary/scanner/portscan/ack` - ACK Firewall Scanner
    
- `auxiliary/scanner/portscan/xmas` - XMAS Scanner
    

## Pro Tips

- Use `search` to find modules
    
- Use `info` within a module for detailed information
    
- Set global options with `setg` for values you use frequently (like LHOST)
    
- Always `show options` before running to verify settings
    
- Use `sessions` command to manage multiple compromised systems