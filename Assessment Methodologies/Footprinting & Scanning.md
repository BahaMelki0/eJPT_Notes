
---

## Network Footprinting and Scanning

Network footprinting involves gathering publicly available information about a target network, such as IP addresses, domain names, and system configurations. The goal is to develop a detailed understanding of the network. Scanning, on the other hand, uses tools like Nmap to actively probe the network, identify open ports, services, and potential vulnerabilities.

Introduction to Network Mapping:

- A diagram titled "Scanning and network mapping" visually illustrates how network mapping tools probe a network to identify live hosts, open ports, and running services. This aids in developing a structured view of the network's topology.
    

*** Networking Primer ***

- Networking Fundamentals:
    
    - Hosts communicate using standardized network protocols.
        
    - Information is transferred between devices in packets.
        
    - The OSI (Open Systems Interconnection) model outlines seven abstraction layers that standardize the functions of communication systems.
        
- The OSI model is depicted in a chart that highlights its seven layers: physical, data link, network, transport, session, presentation, and application. Each layer’s purpose and relationship to others are summarized in this diagram.
    

N.B: The OSI model is a reference framework, not a strict blueprint for every system.

- Network Layer:
    
    - Handles logical addressing, routing, and forwarding of data packets.
        
    - Determines the best path for data travel.
        
    
    Protocols:
    
    - **IP (Internet Protocol)**:
        
        - Logical addressing, routing, fragmentation, and reassembly.
            
        - IPv4 uses 32-bit addresses; structured hierarchically with subnets and CIDR notation.
            
        - IPv6 uses 128-bit hexadecimal addresses.
            
        - Types of IP addresses: broadcast, unicast, multicast.
            
    - **ICMP (Internet Control Message Protocol)**:
        
        - Used for error reporting and diagnostics.
            
        - Common messages include echo request and reply.
            
    - **DHCP (Dynamic Host Configuration Protocol)**:
        
        - Dynamically assigns IP addresses to devices on the network.
            
- Transport Layer (Layer 4):
    
    - Ensures accurate and reliable data delivery between sender and receiver.
        
    
    Protocols:
    
    - **TCP (Transmission Control Protocol)**:
        
        - Connection-oriented and reliable.
            
        - Ensures data arrives accurately and in the correct order.
            
        - Uses a three-way handshake (SYN, SYN-ACK, ACK) to establish connections.
            
    - **UDP (User Datagram Protocol)**:
        
        - Connectionless and lightweight.
            
        - Ideal for streaming, online gaming, and VoIP.
            

** View TCP Activity **

- On Linux:
    

```
netstat -antp
```

- On Windows:
    

```
netsat -ano
```

Common TCP/UDP Ports:

- A visual chart lists common ports, their associated protocols, and typical services. It provides an at-a-glance reference for well-known port assignments, helping identify common service footprints during scanning.
    

*** Host Discovery ***

- Network Mapping:
    
    - Identifies devices, hosts, and network elements in a target network.
        
    - Results in a topology showing hosts, IP addresses, services, ports, and versions.
        
    - Commonly done with Nmap.
        
- Host Discovery Techniques:
    
    - Identifying live hosts using methods like ICMP echo requests, ARP scanning, TCP SYN ping, UDP pings, and TCP ACK ping.
        
    - The chosen method depends on the target network's security controls and pentest goals.
        
- A flowchart breaks down the considerations when using ICMP pings and TCP SYN ping for host discovery, illustrating which techniques are more reliable under various network conditions.
    
- Ping Sweeps:
    
    - Send ICMP Echo Requests to a range of IP addresses to find active hosts.
        

```
ping host
```

- Note: Windows systems often block ICMP requests.
    
- Using `ping`:
    

```
ping -b -c n hostnetwork
```

- `-c`: Number of ICMP requests to send.
    
- `-b`: Broadcast.
    
- Using `fping`:
    

```
fping -a -g hostnetwork
```

- `-a`: Show alive targets.
    
- `-g`: Generate target list based on subnet.
    
- `-S`: Set source address (useful for stealth).
    
- Host Discovery with Nmap:
    
    - **Ping Scan:**
        

```
nmap -sn NetworkIP@ --send-ip
```

- `-sn`: Disable port discovery.
    
- `--send-ip`: Bypass ARP resolution.
    
- **Specific Targets or Ranges:**
    

```
nmap options IP@1 IP@2  # Different targets
nmap options IP@1-IP@2  # Range
```

- **TCP SYN Ping Scan:**
    

```
nmap -PS TargetIP@
```

```
nmap -PSPort TargetIP@  # Specific port
```

```
nmap -PSPort1-Port2 TargetIP@  # Range of ports
```

- **TCP ACK Ping Scan:**
    

```
nmap -PA TargetIP@
```

- **ICMP Ping Scan:**
    

```
nmap -PE TargetIP@
```

- **General Approach:**
    

```
nmap -sn -PS -PU TargetIP@
```

N.B: The privileges used when running Nmap can affect results.

** Port Scanning **

- Port Scanning with Nmap:
    
    - After host discovery, scan open ports and services for potential vulnerabilities.
        

```
nmap -Pn -F -pPort1,Port2,Port3 TargetIP@
```

- `-Pn`: Skip host discovery.
    
- `-F`: Fast scan (top 100 ports).
    
- `-p`: Specify ports.
    
- `-sS`: SYN scan.
    
- `-sT`: TCP connect scan.
    
- `-sU`: UDP scan.
    

N.B: Firewalls may cause ports to appear as filtered when they’re closed.

** Service Version & OS Detection **

- **Service Version Detection:**
    

```
nmap -sS -sV --version-intensity n -O --osscan-guess -p- TargetIP@
```

- `-sV`: Service version.
    
- `-O`: OS detection.
    
- `--osscan-guess`: Aggressive OS version guessing.
    
- `--version-intensity n`: Adjust version detection intensity.
    
- **Nmap Scripting Engine (NSE):**
    
    - List all scripts:
        

```
ls -al /usr/share/nmap/scripts
```

- **Example Scan with Standard Scripts:**
    

```
nmap -sS -sV -sC -p- -T4 TargetIP@
```

- **Get Script Information:**
    

```
nmap --script-help=script
```

- **Run a Specific Script:**
    

```
nmap -sS -sV --script=script -p- -T4 TargetIP@
```

- **Aggressive Scan:**
    

```
nmap -A TargetIP@
```

** Evasion, Scan Performance & Output **

- **Firewall Detection & IDS Evasion:**
    

```
nmap -Pn -sS -sA -F TargetIP@
```

```
nmap -Pn -sS -sA -F -p80,445,3389 -f --mtu n TargetIP@
```

- `-sA`: ACK scan to detect firewalls.
    
- `-f`: Fragment packets.
    
- `--mtu n`: Set minimum fragment size.
    
- **Using Decoys & Data Length:**
    

```
nmap -Pn -sS -sV -f TargetIP@ --data-length n -D DecoyIP@1,DecoyIP@2
```

- `-D`: Decoys.
    
- `--data-length`: Max packet payload length.
    
- **Optimizing Nmap Scans:**
    

```
nmap -Pn -sS -sA -F -T0/1/2/3/4/5 --host-timeout 30s --scan-delay 5s TargetIP@
```

- `-T`: Timing templates from `0` (paranoid) to `5` (insane).
    
- `--scan-delay <time>`: Delay between packets.
    
- `--host-timeout <time>`: Skip unresponsive hosts after a timeout.
    
- **Output Formats:**
    

```
nmap -Pn -sS -F -T4 TargetIP@ -oX output
```

- `-oN`: Normal format.
    
- `-oX`: XML format.
    
- `-oG`: Grepable format.
    
- `-oA`: Output in all major formats.
    
- `-v`: Verbosity.
    
- `--reason`: Display reasons for port states.
    

---