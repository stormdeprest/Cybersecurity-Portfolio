# Hydra - Password Brute Force Tool

## Overview
Hydra is a powerful online password cracking tool that automates brute force attacks against authentication services. It systematically tests passwords from wordlists against login services to identify valid credentials.

## Supported Protocols
Hydra supports 50+ protocols including:
- **Network Services**: SSH, FTP, RDP, Telnet, VNC
- **Web**: HTTP/HTTPS (GET/POST forms), HTTP-Proxy
- **Email**: SMTP, POP3, IMAP
- **Databases**: MySQL, MS-SQL, PostgreSQL, MongoDB
- **Other**: SMB, SNMP, LDAP, RDP, IRC

## Basic Syntax

### SSH Brute Force
```bash
hydra -l <username> -P <password_list> <target_ip> -t 4 ssh
```

**Options:**
- `-l` - Single username
- `-L` - Username list file
- `-p` - Single password
- `-P` - Password list file
- `-t` - Number of parallel threads (default: 16)

**Example:**
```bash
hydra -l root -P passwords.txt 10.10.10.10 -t 4 ssh
```

### HTTP POST Form Brute Force
```bash
hydra -l <username> -P <wordlist> <target_ip> http-post-form "<path>:<credentials>:<failure_string>" -V
```

**Format Breakdown:**
- `<path>` - Login page URL (e.g., `/login.php` or `/`)
- `<credentials>` - Form parameters: `username=^USER^&password=^PASS^`
- `<failure_string>` - Text appearing on failed login (e.g., `F=incorrect`)
- `-V` - Verbose output

**Example:**
```bash
hydra -l admin -P rockyou.txt 10.10.10.10 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V
```

## Key Takeaways
- **Default credentials** (admin:password) are extremely vulnerable
- Strong passwords should be **8+ characters** with special characters
- Common password lists contain millions of frequently-used passwords
- Always **change default credentials** on cameras, routers, and web applications
- Use browser Developer Tools (Network tab) to identify POST vs GET requests

## Security Implications
Hydra demonstrates why:
- Password complexity matters
- Account lockout policies are necessary
- Multi-factor authentication is critical
- Default credentials must be changed immediately
