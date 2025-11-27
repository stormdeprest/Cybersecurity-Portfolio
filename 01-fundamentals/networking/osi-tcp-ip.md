# OSI & TCP/IP Network Models

## OSI Model (7 Layers)

**Purpose:** Reference/theoretical model for understanding network communication, from application to physical cables.

## Layers (Top to Bottom)

**Layer 7: Application**

- **Function:** Interaction with end users. User works through a GUI (Graphical User Interface)
    
- **Examples:** HTTP, SMTP (Simple Mail Transfer Protocol), DNS
    
- **Devices/Software:** Browsers, mail clients
    

**Layer 6: Presentation**

- **Function:** Translation, encryption, compression. Ensures data is sent and read in the same format. Acts as a translator, converting data to the correct format
    
- **Examples:** SSL/TLS, ASCII, JPEG
    
- **Use Case:** Gmail and Outlook (different applications, same protocol)
    

**Layer 5: Session**

- **Function:** Establishing, managing, and terminating sessions (connections)
    
- **Examples:** NetBIOS, RPC
    

**Layer 4: Transport**

- **Function:** Reliable delivery, segmentation. Chooses how data is delivered: TCP or UDP
    
- **Examples:** TCP, UDP
    
- **Devices:** Ports, firewalls (also works as router, so operates at Layer 3 & 4)
    

**Layer 3: Network**

- **Function:** Routing (fastest and best route for data). Data (packets) are sent based on IP addresses between networks
    
- **Examples:** Packets, IP, ICMP
    
- **Devices:** Router
    

**Layer 2: Data Link**

- **Function:** Physical addressing via MAC address (data goes to correct device on same network), frames, error checking. Converts IP from network layer to MAC address
    
- **Examples:** Switch, MAC address, ARP
    
- **Process:** Converts data into frames for transmission via cable or wireless
    

**Layer 1: Physical**

- **Function:** Electrical signals, bits, cables, binary numbers
    
- **Examples:** UTP, fiber optic, radio frequency, network cable, wireless
    
- **Devices:** Hub
    

## TCP/IP Model (4 Layers)

**Purpose:** Practical model, closer to real-world protocols.

## Layers (Top to Bottom)

**Application Layer**

- Combines OSI Layers 5–7
    
- **Examples:** HTTP, FTP, DNS
    

**Transport Layer**

- Corresponds to OSI Layer 4
    
- **Examples:** TCP, UDP
    

**Internet Layer**

- Corresponds to OSI Layer 3
    
- **Examples:** IP, ICMP, packets, router
    

**Network Access Layer**

- Combines OSI Layers 1–2
    
- **Examples:** Ethernet, Wi-Fi, ARP, frames, MAC address
    

## Key Points

- **OSI** = 7 layers (theory)
    
- **TCP/IP** = 4 layers (practice)
    
- TCP/IP maps to OSI but simplified:
    
    - Application = OSI 5–7
        
    - Transport = OSI 4
        
    - Internet = OSI 3
        
    - Network Access = OSI 1–2
        

## Summary

- **OSI:** Useful for learning and discussions ("at what level is this problem?")
    
- **TCP/IP:** The actual protocols you configure daily
    
- **Memory Aid:** **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing (layers 7–1)