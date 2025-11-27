# Nmap Commands Cheat Sheet

|Command|Description|Example|
|---|---|---|
|`-sL`|List scan — shows targets without actually scanning them|`nmap -sL 192.168.1.0/24`|
|`-sn`|Ping scan — host discovery only|`nmap -sn 10.0.0.0/24`|
|`-sT`|TCP connect scan — completes 3-way handshake|`nmap -sT 192.168.1.15`|
|`-sS`|TCP SYN scan — half-open scan (stealth)|`nmap -sS 192.168.1.15`|
|`-sU`|UDP scan|`nmap -sU 192.168.1.15`|
|`-F`|Fast scan — scans 100 most common ports|`nmap -F scanme.nmap.org`|
|`-p [range]`|Port selection (e.g., 1-100, or `-p-` for all ports)|`nmap -p1-200 10.0.0.5`|
|`-Pn`|Treat host as online (skip ping)|`nmap -Pn 192.168.1.50`|
|`-O`|OS detection|`nmap -O 192.168.1.15`|
|`-sV`|Service and version detection|`nmap -sV 192.168.1.15`|
|`-A`|Aggressive scan: OS, services, traceroute, script scanning|`nmap -A 192.168.1.15`|
|`-T0` to `-T5`|Timing templates: 0=paranoid, 5=insane|`nmap -T4 10.0.0.0/24`|
|`--min-parallelism`|Minimum number of parallel probes|`nmap --min-parallelism 20 192.168.1.0/24`|
|`--max-parallelism`|Maximum number of parallel probes|`nmap --max-parallelism 50 192.168.1.0/24`|
|`--min-rate`|Minimum packets per second|`nmap --min-rate 100 10.0.0.5`|
|`--max-rate`|Maximum packets per second|`nmap --max-rate 500 10.0.0.5`|
|`--host-timeout`|Timeout per host|`nmap --host-timeout 30s 192.168.1.0/24`|
|`-v` / `-vv` / `-v4`|Increases verbosity of output|`nmap -vv scanme.nmap.org`|
|`-d` / `-d9`|Debug mode|`nmap -d9 192.168.1.15`|
|`-oN`|Save output in normal format|`nmap -oN scan.txt 10.0.0.5`|
|`-oX`|Output in XML format|`nmap -oX output.xml 10.0.0.5`|
|`-oG`|Greppable output|`nmap -oG grep.txt 10.0.0.5`|
|`-oA`|Output in all formats simultaneously|`nmap -oA myscan 10.0.0.5`|

## Scan Types Comparison

**Stealth vs Standard:**

- `-sS` (SYN scan) - Stealthier, requires root privileges
    
- `-sT` (TCP connect) - More detectable, works without root
    

**Speed Settings:**

- `-T0` (Paranoid) - Very slow, IDS evasion
    
- `-T3` (Normal) - Default timing
    
- `-T4` (Aggressive) - Fast, recommended for reliable networks
    
- `-T5` (Insane) - Extremely fast, may miss hosts
    

## Common Scan Combinations

**Quick network discovery:**

`nmap -sn -T4 192.168.1.0/24`

**Comprehensive host scan:**

`nmap -A -T4 -oA complete_scan 192.168.1.15`

**Scan all ports with service detection:**

`nmap -p- -sV -T4 10.0.0.5`

**Stealth scan with specific ports:**

`nmap -sS -p 22,80,443 -Pn 192.168.1.50`