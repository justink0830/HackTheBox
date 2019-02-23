
```console
root@kali:~/HTB/Machines/119# nmap -sS -sV -p- -T4 10.10.10.119
Starting Nmap 7.70 ( https://nmap.org ) at 2019-02-23 03:49 EST
Nmap scan report for 10.10.10.119
Host is up (0.26s latency).
Not shown: 65532 filtered ports
PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 7.4 (protocol 2.0)
80/tcp  open  http    Apache httpd 2.4.6 ((CentOS) OpenSSL/1.0.2k-fips mod_fcgid/2.3.9 PHP/5.4.16)
389/tcp open  ldap    OpenLDAP 2.2.X - 2.3.X

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 298.40 seconds
```
