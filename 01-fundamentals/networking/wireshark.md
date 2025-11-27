# Wireshark GUI Quick Reference

## Main Interface Components

**Packet List Pane (Top)**

- Shows all captured packets in chronological order
    
- Click any packet to view details below
    
- Color coding indicates packet types (green = TCP, blue = UDP, black = errors)
    

**Packet Details Pane (Middle)**

- Expandable tree view of selected packet
    
- Shows protocol layers (Ethernet → IP → TCP → Application)
    
- Click arrows to expand/collapse sections
    

**Packet Bytes Pane (Bottom)**

- Hexadecimal and ASCII view of raw packet data
    
- Clicking in details pane highlights corresponding bytes
    

## Essential Menu Options

**Capture Menu**

- Start/Stop capture
    
- Capture Options (choose interface, apply capture filters)
    
- Capture Filters (set before capturing)
    

**Analyze Menu**

- Display Filters (filter already captured packets)
    
- Follow → TCP/UDP/HTTP Stream
    
- Expert Information (warnings and errors)
    

**Statistics Menu**

- Protocol Hierarchy (traffic breakdown by protocol)
    
- Conversations (all connections between hosts)
    
- Endpoints (all communicating devices)
    
- IO Graphs (visualize traffic over time)
    

**File Menu**

- Export Objects → HTTP/SMB (extract files from capture)
    
- Export Packet Dissections (save filtered results)
    

## Toolbar Shortcuts

|Icon/Button|Function|
|---|---|
|Blue shark fin|Start capture|
|Red square|Stop capture|
|Green shark fin|Restart capture|
|Filter bar (top)|Apply display filters|
|Magnifying glass|Find packet|
|Arrows (←/→)|Navigate packet history|

## Color Rules

Default color coding helps identify packet types at a glance:

- **Light green** - HTTP traffic
    
- **Light blue** - UDP traffic
    
- **Black background** - Bad TCP packets (errors, retransmissions)
    
- **Red** - Problems/errors
    
- **Yellow** - Routing protocols
    

**Customize colors:**  
View → Coloring Rules

## Right-Click Context Menu

Right-clicking on any packet or field provides quick actions:

- Apply as Filter (creates filter based on selected field)
    
- Follow Stream (view entire conversation)
    
- Copy → as Filter/Value/Bytes
    
- Protocol Preferences
    
- Decode As (force protocol interpretation)
    

## Column Customization

**Add custom columns:**

1. Right-click packet field in details pane
    
2. Apply as Column
    
3. Common additions: HTTP Host, DNS Query Name, TCP Stream Index
    

**Reorder columns:**

- Drag column headers to rearrange
    

## Time Display Options

View → Time Display Format:

- Seconds Since Beginning of Capture
    
- Date and Time of Day
    
- Seconds Since Previous Displayed Packet
    

## Profile Management

Edit → Configuration Profiles:

- Create different profiles for different tasks
    
- Each profile has custom filters, columns, and colors
    
- Examples: Web Analysis, Network Troubleshooting, Malware Analysis
    

## Quick Keyboard Shortcuts

|Shortcut|Action|
|---|---|
|`Ctrl+E`|Start/Stop capture|
|`Ctrl+F`|Find packet|
|`Ctrl+G`|Go to packet number|
|`Ctrl+/`|Apply/clear display filter|
|`Ctrl+→`|Next packet in conversation|
|`Ctrl+←`|Previous packet in conversation|
|`Ctrl+Shift+P`|Print packets|

## Workflow Tips

**Typical analysis workflow:**

1. Start capture or open .pcap file
    
2. Use display filters to narrow down traffic
    
3. Right-click → Follow Stream for conversations
    
4. Check Statistics → Conversations for overview
    
5. Use Expert Information for automatic problem detection
    
6. Export objects or packets as needed
    

**Performance tip:**  
For large captures, use display filters rather than scrolling to improve responsiveness.