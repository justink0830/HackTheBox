# Initial-scan.nmap
```console
# Nmap 7.70 scan initiated Wed Jun 19 23:09:19 2019 as: nmap -sV -sC -oN initial-scan.nmap Arkham.htb
Nmap scan report for Arkham.htb (10.10.10.130)
Host is up (0.26s latency).
Not shown: 995 filtered ports
PORT     STATE SERVICE       VERSION
80/tcp   open  http          Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds?
8080/tcp open  http          Apache Tomcat 8.5.37
| http-methods: 
|_  Potentially risky methods: PUT DELETE
|_http-title: Mask Inc.
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2019-06-19 23:09:58
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Jun 19 23:10:36 2019 -- 1 IP address (1 host up) scanned in 76.97 seconds
```
# vuln-scan.nmap
```console
# Nmap 7.70 scan initiated Wed Jun 19 23:57:11 2019 as: nmap --script vuln -oN vuln-scan.nmap Arkham.htb
Nmap scan report for Arkham.htb (10.10.10.130)
Host is up (0.26s latency).
Not shown: 995 filtered ports
PORT     STATE SERVICE
80/tcp   open  http
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-dombased-xss: Couldn't find any DOM based XSS.
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
8080/tcp open  http-proxy
| http-slowloris-check: 
|   VULNERABLE:
|   Slowloris DOS attack
|     State: LIKELY VULNERABLE
|     IDs:  CVE:CVE-2007-6750
|       Slowloris tries to keep many connections to the target web server open and hold
|       them open as long as possible.  It accomplishes this by opening connections to
|       the target web server and sending a partial request. By doing so, it starves
|       the http server's resources causing Denial Of Service.
|       
|     Disclosure date: 2009-09-17
|     References:
|       http://ha.ckers.org/slowloris/
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6750

Host script results:
|_samba-vuln-cve-2012-1182: Could not negotiate a connection:SMB: ERROR: Server disconnected the connection
|_smb-vuln-ms10-054: false
|_smb-vuln-ms10-061: Could not negotiate a connection:SMB: ERROR: Server disconnected the connection

# Nmap done at Thu Jun 20 00:02:25 2019 -- 1 IP address (1 host up) scanned in 314.15 seconds
```
https://github.com/gkbrk/slowloris

