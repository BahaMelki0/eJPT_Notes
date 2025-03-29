
---

Information gathering is the first step of any penetration test and it involves collecting information about the target, whether it’s a company or an individual.

** Passive Information Gathering **

Passive information gathering focuses on finding publicly available details about the target without direct interaction. Common approaches include:

- **Website Recon and Footprinting:**
    
    - Identifying IP addresses, hidden directories, user information, and web technologies used.
        
- **Determining a Server’s IP Address:**
    

```
host example.com
```

- **Analyzing robots.txt:**
    
    - This file uses the Robots Exclusion Protocol to define which parts of a website web crawlers can access.
        
- **Examining sitemap_index.xml:**
    
    - A structured XML file listing website directories, commonly found in applications like WordPress.
        
- **Using whatweb:**
    
    - Sends requests to gather information about a web domain.
        
- **Utilizing httrack:**
    
    - A website copier that downloads website files, estimating the site’s structure for offline analysis.
        
- **Running WHOIS lookups:**
    
    - Queries databases to find registrant details and other administrative information about internet domains and IP addresses.
        
- **Checking Netcraft:**
    
    - An online service that helps enumerate web properties and technologies.
        
- **DNS Reconnaissance:**
    
    - Tools like DNSRecon and services like DNSDumpster allow you to:
        
        - Check NS records for zone transfers.
            
        - Enumerate MX, SOA, NS, A, AAAA, SPF, and TXT records.
            
        - Discover service (SRV) records.
            
        - Expand top-level domains (TLDs).
            
- **Detecting Web Application Firewalls (WAF):**
    
    - Tools like WAFW00F identify the presence and type of a WAF.
        
- **Subdomain Enumeration:**
    
    - Sublist3r lists subdomains for a given domain.
        
- **Using Google Dorks:**
    
    - Search operators like `site:`, `filetype:`, `intitle:`, `inurl:` combined with entries from the Google Hacking Database can reveal sensitive or hidden information.
        
- **Finding Publicly Available Emails:**
    
    - TheHarvester automates email searches from public data sources.
        
- **Checking for Leaked Passwords:**
    
    - Have I Been Pwned? can reveal if a target’s credentials are part of known data breaches.
        

** Active Information Gathering **

Active information gathering involves direct interaction with the target’s network, systems, and devices to collect data. This approach includes:

- **DNS Zone Transfers:**
    
    - DNS servers store records that help identify associated IP addresses, mail servers, service aliases, and more. Common record types:
        
        - **A:** Maps a hostname to an IPv4 address.
            
        - **AAAA:** Maps a hostname to an IPv6 address.
            
        - **NS:** Points to the domain’s authoritative nameservers.
            
        - **MX:** Identifies mail servers for the domain.
            
        - **CNAME:** Provides domain aliases.
            
        - **TXT:** Stores arbitrary text, often for configuration or verification.
            
        - **HINFO:** Host information records.
            
        - **SOA:** Start of Authority, specifying zone ownership.
            
        - **SRV:** Identifies specific services.
            
        - **PTR:** Resolves an IP address back to a hostname.
            
- **DNS Tools:**
    
    - **dnsenum:** Enumerates public DNS records and performs tasks like zone transfers and brute-forcing.
        
    - **dig:** Another tool capable of performing zone transfers.
        
    - **fierce:** A lightweight DNS scanner.
        
- **Nmap Scanning:**
    
    - **Host Discovery:**
        
        - Network discovery identifies active hosts on the network.
            

```
nmap -sn networkIP
```

```
- `-sn`: Disable port scanning.
```

- **Using Netdiscover:**
    

```
netdiscover -i eth0 -r networkIP
```

- **Port Scanning with Nmap:**
    
    - By default, Nmap performs a TCP SYN scan on the most commonly used ports.
        

```
nmap hostIP
```

```
- Common options:
  - `-Pn`: Skip host discovery.
  - `-p-`: Scan all ports.
  - `-F`: Fast scan (100 ports).
  - `-sU`: UDP scan.
  - `-v`: Increase verbosity.
  - `-sV`: Service version detection.
  - `-O`: Operating system detection.
  - `-sC`: Run standard scripts.
  - `-A`: Aggressive scan (includes OS detection and default scripts).
  - `-T`: Adjust timing to speed up or slow down the scan.
  - `-oX`: Output results in XML format.
```

---