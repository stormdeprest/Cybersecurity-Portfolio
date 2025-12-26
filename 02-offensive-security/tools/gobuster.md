# Gobuster - Web Enumeration Tool

## Overview
Gobuster is a Go-based brute force enumeration tool used during reconnaissance and scanning phases of penetration testing. It discovers hidden resources by systematically trying wordlist entries against targets.

**Core Concepts:**
- **Enumeration**: Listing all available resources (accessible or not)
- **Brute Force**: Testing every possibility from a wordlist until matches are found

## Supported Modes
- `dir` - Directory/file enumeration
- `dns` - DNS subdomain enumeration
- `vhost` - Virtual host enumeration
- `s3` - AWS S3 bucket enumeration
- `gcs` - Google Cloud Storage enumeration
- `fuzz` - Custom fuzzing mode

## Global Flags
| Short | Long | Description |
|-------|------|-------------|
| `-t` | `--threads` | Number of concurrent threads (default: 10) |
| `-w` | `--wordlist` | Path to wordlist file |
| `-o` | `--output` | Write results to file |
| `--delay` | | Time to wait between requests (e.g., 1500ms) |
| `--debug` | | Enable debug output for troubleshooting |
| `-q` | `--quiet` | Suppress banner and noise |
| `-v` | `--verbose` | Verbose error output |

## DIR Mode - Directory & File Enumeration

### Basic Syntax
```bash
gobuster dir -u "http://example.thm" -w /path/to/wordlist
```

### Common Flags
| Short | Long | Description |
|-------|------|-------------|
| `-u` | `--url` | Target URL (must include protocol) |
| `-x` | `--extensions` | File extensions to search (e.g., `.php,.js`) |
| `-c` | `--cookies` | Cookies to include in requests |
| `-H` | `--headers` | Custom headers for requests |
| `-k` | `--no-tls-validation` | Skip TLS certificate validation |
| `-r` | `--followredirect` | Follow HTTP redirects (301/302) |
| `-s` | `--status-codes` | Display only specific status codes |
| `-b` | `--status-codes-blacklist` | Hide specific status codes |
| `-U` / `-P` | `--username` / `--password` | Credentials for authenticated scans |

### Examples
**Basic directory enumeration:**
```bash
gobuster dir -u "http://example.thm" -w /usr/share/wordlists/dirb/small.txt -t 64
```

**Enumerate with file extensions:**
```bash
gobuster dir -u "http://example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .php,.js
```

**Follow redirects:**
```bash
gobuster dir -u "http://example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r
```

### Important Notes
- **Protocol required**: URL must include `http://` or `https://`
- **IP vs Hostname**: Use hostname to avoid targeting wrong site (virtual hosting)
- **Non-recursive**: Must manually enumerate discovered subdirectories
- **Target specific paths**: Use `-u "http://example.thm/resources"` for subdirectories

## DNS Mode - Subdomain Enumeration

### Basic Syntax
```bash
gobuster dns -d example.thm -w /path/to/wordlist
```

### Common Flags
| Short | Long | Description |
|-------|------|-------------|
| `-d` | `--domain` | Target domain to enumerate |
| `-i` | `--show-ips` | Display resolved IP addresses |
| `-c` | `--show-cname` | Show CNAME records |
| `-r` | `--resolver` | Custom DNS server for resolution |

### Example
```bash
gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

**How it works:**
- Wordlist entry: `all`
- DNS query: `all.example.thm`
- Repeats for each wordlist entry

### Use Case
Subdomains may contain vulnerabilities not present in main domain (e.g., `mobile.example.thm` vs `example.thm`)

## VHOST Mode - Virtual Host Enumeration

### Basic Syntax
```bash
gobuster vhost -u "http://example.thm" -w /path/to/wordlist
```

### VHOST vs DNS
- **VHOST**: IP-based websites on same server (uses HTTP Host header)
- **DNS**: Domain name resolution via DNS lookup

### Common Flags
| Short | Long | Description |
|-------|------|-------------|
| `-u` | `--url` | Base URL/IP address |
| `--domain` | | Set top and second-level domain |
| `--append-domain` | | Append domain to wordlist entries |
| `--exclude-length` | | Filter responses by body length |
| `-r` | `--follow-redirect` | Follow HTTP redirects |
| `-m` | `--method` | HTTP method (GET, POST) |

### Example
```bash
gobuster vhost -u "http://10.10.10.10" --domain example.thm \
  -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt \
  --append-domain --exclude-length 250-320
```

### HTTP Request Breakdown
```http
GET / HTTP/1.1
Host: www.example.thm
```

**Host header components:**
- `www` - Subdomain (replaced by wordlist entries)
- `.example` - Second-level domain (set with `--domain`)
- `.thm` - Top-level domain (set with `--domain`)

### Filtering False Positives
- Use `--exclude-length` to filter responses by size
- False positives typically return similar response sizes (404 errors)
- True positives usually return 200 OK with different response size

## Key Takeaways
- **DIR mode**: Discover hidden directories and files on web servers
- **DNS mode**: Find subdomains via DNS lookups
- **VHOST mode**: Discover virtual hosts via HTTP Host header manipulation
- **Wordlists matter**: Use appropriate wordlists for target (SecLists is recommended)
- **Thread optimization**: Increase `-t` value for faster scans (balance with server load)
- **Always enumerate discovered paths**: Gobuster is non-recursive
