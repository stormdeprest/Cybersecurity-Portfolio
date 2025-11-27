# Linux Command Line & Security - Powerpoint Summary

## Module 1: Introduction & Basic Steps

- `whoami` - Displays the username you are currently logged in as
    
- `pwd` - Shows the full path of your current directory (Print Working Directory)
    
- `lsb_release -a` - Displays detailed information about your Linux distribution (e.g., Ubuntu 24.04)
    
- `ls -lah` - Shows a detailed list of all files and directories (including hidden files) in the current directory
    
- `cd <directory>` - Changes your current directory to the specified one (Change Directory). Example: `cd /etc`
    
- `tree -L 2 /` - Displays the directory structure as a tree, 2 levels deep, starting from root (/)
    
- `uname -a` - Shows all system information, including kernel version and hostname
    

## Module 2: Command Line Basics (Navigation & Files)

- `mkdir <name>` - Creates a new directory with the specified name (Make Directory)
    
- `rmdir <name>` - Removes an empty directory (Remove Directory)
    
- `cp <source> <destination>` - Copies a file or directory
    
- `mv <source> <destination>` - Moves or renames a file or directory (Move)
    
- `rm -f <file>` - Deletes a file (Remove). The `-f` flag forces deletion without confirmation
    
- `cat <file>` - Displays the entire contents of a text file on your screen
    
- `grep <search_term>` - Searches within text or command output for the specified search term
    
- `less` - Allows you to scroll through long text or output page by page. Very useful!
    
- `head` - Displays the first few lines of a file
    
- `tail` - Displays the last few lines of a file
    
- `tail -f <logfile>` - A crucial command! Shows the end of a file and continues monitoring for new lines. Perfect for live logs
    
- `wc` - Counts the number of lines, words, and characters in a file (Word Count)
    
- `man mmand>` - Shows the manual page for a command
    
- `mmand> --help` - Displays brief help text for a command
    
- `apropos <search_term>` - Helps you find a command when you know what you want to do but not which command to use
    
- `echo <text>` - Prints the specified text to the screen (e.g., `echo $PATH`)
    
- `export` - Sets an environment variable (e.g., `export EDITOR=nano`)
    
- `who` - Shows who is currently logged into the system
    
- `|` (pipeline) - Combines two commands together
    
- `>` (overwrite) - Redirects command output to a file and overwrites it if it exists. Example: `echo "Hello world" > text.txt`
    
- `>>` (append) - Redirects output to a file but appends to the end instead of overwriting. Example: `echo "another line" >> text.txt`
    

## Module 3: Users & Permissions

- `chmod de/rules> <file>` - Modifies the access permissions of a file
    
    - Example (Octal): `chmod 750 script.sh`
        
    - Example (Symbolic): `chmod u+x script.sh`
        
- `sudo mmand>` - Executes a command with root (administrator) privileges
    
- `adduser <user>` - User-friendly way to create a new user
    
- `passwd <user>` - Sets or changes the password for a user
    
- `deluser <user>` - Removes a user
    
- `groupadd` - Creates a new group
    
- `usermod -aG <group> <user>` - Adds a user to an additional group (e.g., the sudo group)
    
- `visudo` - Safe way to edit the `/etc/sudoers` file, which determines who can use sudo
    
- `chown <user>:<group> <file>` - Changes the owner and group of a file
    
- `chgrp` - Changes only the group of a file
    

## Module 4: Networking

- `ip addr show` - Shows all network interfaces and their IP addresses (replaces `ifconfig`)
    
- `ip route show` - Shows the routing table (how your server knows where to send packets)
    
- `ping <host>` - Tests if you can connect to another computer (e.g., `ping 8.8.8.8`)
    
- `traceroute <host>` - Shows the route (all intermediate servers) that your packets take to reach a host
    
- `netstat` / `ss` - Show all open ports and active network connections. `ss` is the modern replacement
    
- `nslookup` / `dig` - Tools to query DNS information (e.g., convert a domain name to an IP)
    
- `ufw` - Simple tool to manage the firewall (Uncomplicated Firewall)
    
    - `sudo ufw enable` - Activates the firewall
        
    - `sudo ufw allow ssh` - Allows incoming SSH traffic
        
    - `sudo ufw status` - Shows current firewall status and rules
        
- `iptables` / `nftables` - Advanced, underlying firewall systems in Linux
    

## Module 5: Package Management (Software Installation)

- `apt` - Package management tool for Debian/Ubuntu-based systems
    
    - `sudo apt install <package>` - Installs a new package (e.g., `sudo apt install nmap`)
        
    - `sudo apt update` - Refreshes the list of available packages (always do this before installing!)
        
    - `apt search <package>` - Searches for a package in the repositories
        
    - `sudo apt remove <package>` - Removes a package (e.g., htop)
        
- `dnf` / `yum` - Package management tool for Red Hat/Fedora systems
    
- `pacman` - Package management tool for Arch systems
    

## Module 6: Processes & Services

- `ps aux` - Shows a snapshot of all processes running on the system
    
- `top` - Shows a live overview of your processes, sorted by CPU or memory usage
    
- `kill <PID>` - Stops a process based on its Process ID (PID)
    
- `systemctl` - Central tool for managing services (background processes like web servers or SSH)
    
    - `systemctl status <service>` - Checks the status (e.g., `systemctl status sshd`)
        
    - `systemctl restart <service>` - Restarts a service
        
    - `systemctl enable <service>` - Ensures a service starts automatically on boot
        
- `journalctl -u <service>` - Shows logs specific to one service (e.g., `journalctl -u sshd`)
    

## Module 7 & 8: Security & Scripts

- `nano` - Simple, beginner-friendly text editor for the terminal (e.g., `sudo nano /etc/ssh/sshd_config`)
    
- `fail2ban` - Tool that reads log files and blocks IP addresses showing suspicious behavior (like too many failed login attempts)
    
- `cron` - System service for automating tasks at scheduled times