# Tcpdump Commands Cheat Sheet

|Command|Description|Example|
|---|---|---|
|`tcpdump -i INTERFACE`|Captures traffic on a specific network interface|`tcpdump -i eth0`|
|`tcpdump -w FILE`|Writes captured packets to a file|`tcpdump -w capture.pcap`|
|`tcpdump -r FILE`|Reads packets from a previously saved pcap file|`tcpdump -r capture.pcap`|
|`tcpdump -c COUNT`|Captures only a specified number of packets|`tcpdump -c 20`|
|`tcpdump -n`|Does not resolve IP addresses to hostnames (faster output)|`tcpdump -n`|
|`tcpdump -nn`|Does not resolve hostnames or protocol/port names (all numeric)|`tcpdump -nn`|
|`tcpdump -v`|More detail; use `-vv` and `-vvv` for even more verbosity|`tcpdump -vv -i eth0`|
|`tcpdump host IP`|Filters traffic to or from a specific IP address|`tcpdump host 192.168.1.10`|
|`tcpdump src host IP`|Shows only traffic originating from this IP|`tcpdump src host 10.0.0.5`|
|`tcpdump dst host IP`|Shows only traffic going to this IP|`tcpdump dst host 10.0.0.5`|
|`tcpdump port PORT`|Filters traffic on a specific port (source or destination)|`tcpdump port 443`|
|`tcpdump src port PORT`|Traffic originating from a specific source port|`tcpdump src port 53`|
|`tcpdump dst port PORT`|Traffic going to a specific destination port|`tcpdump dst port 22`|
|`tcpdump PROTOCOL`|Filters by protocol, such as `ip`, `ip6`, `icmp`|`tcpdump icmp`|
|`tcpdump -q`|Provides brief, quiet output|`tcpdump -q -i eth0`|
|`tcpdump -e`|Shows MAC addresses of packets|`tcpdump -e -i eth0`|
|`tcpdump -A`|Shows packet content in ASCII (good for HTTP)|`tcpdump -A -s 0 port 80`|
|`tcpdump -xx`|Shows packet data in hexadecimal|`tcpdump -xx -i eth0`|
|`tcpdump -X`|Shows packet data in both hexadecimal and ASCII|`tcpdump -X -s 0 port 80`|

## Common Use Cases

**Capture HTTP traffic:**

`tcpdump -i eth0 -A -s 0 port 80`

**Capture all traffic from a specific host:**

`tcpdump -i eth0 host 192.168.1.100 -w output.pcap`

**Monitor DNS queries:**

`tcpdump -i eth0 -n port 53`

**Capture ICMP (ping) traffic with verbose output:**

`tcpdump -i eth0 -vv icmp`