
---

Enumeration follows host discovery and port scanning. The goal is to identify details about services running on specific hosts, such as account names, shared resources, misconfigurations, etc.

1. NMAP SCRIPTING ENGINE (NSE)
    

---

Port Scanning and Enumeration with Nmap:

- Nmap output can be imported into Metasploit (MSF) as XML for vulnerability detection and exploitation.
    

Command:

```
nmap -Pn -sV -O TargetIP@ -oX output
```

Importing Nmap Scan Results into MSF:

```
msfconsole
```

```
msf5 > workspace name    # Create a workspace
```

```
msf5 > db_import file    # Import the Nmap results file
```

```
msf5 > services          # Display discovered services
```

Initiating an Nmap Scan using MSF:

```
msfconsole
```

```
msf5 > workspace name    # Create a workspace
```

```
msf5 > db_nmap -Pn -sV -O targetIP@   # The result is automatically saved to the workspace
```

```
msf5 > services          # Display discovered services
```

Port Scanning with Auxiliary Modules:

- Auxiliary modules are used mainly for information extraction (no exploitation). They are useful during post-exploitation when Nmap is unavailable on the compromised machine.
    

Commands:

```
msf5 > search portscan   # Search for available portscan modules
```

```
msf5 > use module_name/module_id
```

```
msf5 > show options
```

```
msf5 > set option1 value
...
msf5 > set optionN value
```

```
msf5 > run
```

Adding a Route via a Compromised Machine:

- To use the compromised machine for further scans, add its route:
    

```
meterpreter > run autoroute -s CompromisedMachineIP@
```

```
meterpreter > background
```

_This allows you to execute scan auxiliaries using the compromised machine's IP._

UDP Sweep Module:

- The udp_sweep module performs a UDP scan.
    
- Lab Note: Use the meterpreter session to discover the second target's IP. Then, perform an Nmap scan from your main machine (if on the same network) or use auxiliary modules after setting the route.
    

---

2. SERVICE ENUMERATION
    

---

FTP Enumeration:

- FTP (File Transfer Protocol) typically uses port 21 and is used for file sharing between a server and client. It is also a common method for transferring files to/from a web server.
    

FTP MSF Enumeration Modules:

```
msf5 > search type:auxiliary ftp
```

```
msf5 > use scanner/ftp/ftp_version   # Check FTP version
```

```
msf5 > use scanner/ftp/ftp_login      # Brute-force FTP login
```

```
msf5 > use scanner/ftp/anonymous      # Scan for anonymous FTP login
```

_Connect to FTP:_

```
ftp TargetIP@
```

SMB Enumeration:

- SMB (Server Message Block) uses ports 445 and 139 (and relies on the NetBIOS protocol). SAMBA is the Linux version of SMB.
    

SMB MSF Enumeration Modules:

```
msf5 > use scanner/smb/smb_version      # Scan SMB version
```

```
msf5 > use scanner/smb/smb_enumusers      # Enumerate SMB users
```

```
msf5 > use scanner/smb/smb_enumshares     # Enumerate shared resources
```

```
msf5 > use scanner/smb/smb_login          # Brute-force SMB login with a user or a list
```

Web Server Enumeration:

- Web servers use HTTP (typically on TCP port 80) to serve website data. Popular examples include Apache, Nginx, and Microsoft IIS.
    

Web Server MSF Enumeration Modules:

```
msf5 > setg RHOSTS TargetIP@            # Set target IP as a global variable
```

```
msf5 > use scanner/http/http_version     # Detect HTTP version
```

```
msf5 > use scanner/http/http_header      # Display HTTP headers
```

```
msf5 > use scanner/http/robots_txt       # Display contents of robots.txt
```

```
msf5 > use scanner/http/dir_scanner       # Directory brute-force scan
```

```
msf5 > use scanner/http/files_dir         # File brute-force scan
```

```
msf5 > use scanner/http/http_login        # Brute-force login on user forms
```

```
msf5 > use scanner/http/apache_userdir_enum  # Brute-force Apache usernames
```

MySQL Enumeration:

- MySQL is an open source database management system based on SQL, using TCP port 3306.
    

MySQL MSF Enumeration Modules:

```
msf5 > use scanner/mysql/mysql_version    # Scan MySQL version
```

```
msf5 > use scanner/mysql/mysql_login      # Brute-force credentials
```

```
msf5 > use admin/mysql/mysql_enum         # Enumerate MySQL database server (with valid credentials)
```

```
msf5 > use admin/mysql/mysql_sql          # Execute SQL queries (with valid credentials)
```

```
msf5 > use scanner/mysql/mysql_schemadump   # Dump the database schema
```

```
msf5 > use auxiliary/scanner/mysql/mysql_hashdump
```

```
msf5 > use auxiliary/scanner/mysql/mysql_writable_dirs
```

SSH Enumeration:

- SSH (Secure Shell) is used for remote access (a replacement for Telnet) and typically uses TCP port 22.
    

SSH MSF Enumeration Modules:

```
msf5 > use scanner/ssh/ssh_version        # Check SSH version
```

```
msf5 > use scanner/ssh/ssh_login          # Brute-force SSH login
```

```
msf5 > use scanner/ssh/ssh_login_pubkey     # Brute-force SSH login using a public key
```

```
msf5 > use scanner/ssh/ssh_enumusers        # Enumerate SSH users using a list
```

SMTP Enumeration:

- SMTP (Simple Mail Transfer Protocol) is used for transmitting email and typically uses TCP port 25 (with alternatives like 465 and 587).
    

SMTP MSF Enumeration Modules:

```
msf5 > use scanner/smtp/smtp_version        # Check SMTP version
```

```
msf5 > use scanner/smtp/smtp_enum           # Enumerate user accounts
```

_Example command with smtp-user-enum:_

```
smtp-user-enum [options] (-u username | -U file-of-usernames) (-t host | -T file-of-targets)
```

---

## MSF TIPS & GLOBAL SETTINGS

- Set a global target IP to avoid re-entering it for each module:
    

```
msf5 > setg RHOSTS TargetIP@
```

- MSF Wordlists are typically located at:
    

```
/usr/share/metasploit-framework/data/wordlists/
```

---