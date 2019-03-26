## NMAP
```console
root@kali:/mnt/hgfs/HackTheBox/Machines/124# nmap -A 10.10.10.124
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-26 04:16 EDT
Nmap scan report for 10.10.10.124
Host is up (0.26s latency).
Not shown: 996 closed ports
PORT     STATE SERVICE   VERSION
22/tcp   open  ssh?
80/tcp   open  http      nginx
|_http-server-header: ClownWare Proxy
|_http-title: Did not follow redirect to https://10.10.10.124/
443/tcp  open  ssl/https ClownWare Proxy
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 200 OK
|     Date: Tue, 26 Mar 2019 08:17:01 GMT
|     Content-Type: text/html; charset=UTF-8
|     Connection: close
|     Server: ClownWare Proxy
|     <!DOCTYPE html>
|     <!--[if lt IE 7]> <html class="no-js ie6 oldie" lang="en-US"> <![endif]-->
|     <!--[if IE 7]> <html class="no-js ie7 oldie" lang="en-US"> <![endif]-->
|     <!--[if IE 8]> <html class="no-js ie8 oldie" lang="en-US"> <![endif]-->
|     <!--[if gt IE 8]><!-->
|     <html class="js" style="opacity: 1; visibility: visible;" lang="en-US"><!--<![endif]--><head>
|     <title>Direct IP access not allowed | ClownWare</title>
|     <meta charset="UTF-8">
|     <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
|     <meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
|     <meta name="robots" content="noindex, nofollow">
|     <meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1">
|_    <link rel="stylesheet" id="cf_styles-css" href="index_files
|_http-server-header: ClownWare Proxy
|_http-title: Direct IP access not allowed | ClownWare
| ssl-cert: Subject: commonName=ClownWare.htb/organizationName=ClownWare Ltd/stateOrProvinceName=LON/countryName=UK
| Subject Alternative Name: DNS:clownware.htb, DNS:sni147831.clownware.htb, DNS:*.clownware.htb, DNS:proxy.clownware.htb, DNS:console.flujab.htb, DNS:sys.flujab.htb, DNS:smtp.flujab.htb, DNS:vaccine4flu.htb, DNS:bestmedsupply.htb, DNS:custoomercare.megabank.htb, DNS:flowerzrus.htb, DNS:chocolateriver.htb, DNS:meetspinz.htb, DNS:rubberlove.htb, DNS:freeflujab.htb, DNS:flujab.htb
| Not valid before: 2018-11-28T14:57:03
|_Not valid after:  2023-11-27T14:57:03
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1
| tls-nextprotoneg: 
|_  http/1.1
8080/tcp open  ssl/http  nginx
|_http-server-header: ClownWare Proxy
|_http-title: Direct IP access not allowed | ClownWare
| ssl-cert: Subject: commonName=ClownWare.htb/organizationName=ClownWare Ltd/stateOrProvinceName=LON/countryName=UK
| Subject Alternative Name: DNS:clownware.htb, DNS:sni147831.clownware.htb, DNS:*.clownware.htb, DNS:proxy.clownware.htb, DNS:console.flujab.htb, DNS:sys.flujab.htb, DNS:smtp.flujab.htb, DNS:vaccine4flu.htb, DNS:bestmedsupply.htb, DNS:custoomercare.megabank.htb, DNS:flowerzrus.htb, DNS:chocolateriver.htb, DNS:meetspinz.htb, DNS:rubberlove.htb, DNS:freeflujab.htb, DNS:flujab.htb
| Not valid before: 2018-11-28T14:57:03
|_Not valid after:  2023-11-27T14:57:03
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1
| tls-nextprotoneg: 
|_  http/1.1
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port443-TCP:V=7.70%T=SSL%I=7%D=3/26%Time=5C99DFFC%P=x86_64-pc-linux-gnu
SF:%r(GetRequest,E20,"HTTP/1\.1\x20200\x20OK\r\nDate:\x20Tue,\x2026\x20Mar
SF:\x202019\x2008:17:01\x20GMT\r\nContent-Type:\x20text/html;\x20charset=U
SF:TF-8\r\nConnection:\x20close\r\nServer:\x20ClownWare\x20Proxy\r\n\r\n<!
SF:DOCTYPE\x20html>\n<!--\[if\x20lt\x20IE\x207\]>\x20<html\x20class=\"no-j
SF:s\x20ie6\x20oldie\"\x20lang=\"en-US\">\x20<!\[endif\]-->\n<!--\[if\x20I
SF:E\x207\]>\x20\x20\x20\x20<html\x20class=\"no-js\x20ie7\x20oldie\"\x20la
SF:ng=\"en-US\">\x20<!\[endif\]-->\n<!--\[if\x20IE\x208\]>\x20\x20\x20\x20
SF:<html\x20class=\"no-js\x20ie8\x20oldie\"\x20lang=\"en-US\">\x20<!\[endi
SF:f\]-->\n<!--\[if\x20gt\x20IE\x208\]><!-->\n<html\x20class=\"js\"\x20sty
SF:le=\"opacity:\x201;\x20visibility:\x20visible;\"\x20lang=\"en-US\"><!--
SF:<!\[endif\]--><head>\n<title>Direct\x20IP\x20access\x20not\x20allowed\x
SF:20\|\x20ClownWare</title>\n<meta\x20charset=\"UTF-8\">\n<meta\x20http-e
SF:quiv=\"Content-Type\"\x20content=\"text/html;\x20charset=UTF-8\">\n<met
SF:a\x20http-equiv=\"X-UA-Compatible\"\x20content=\"IE=Edge,chrome=1\">\n<
SF:meta\x20name=\"robots\"\x20content=\"noindex,\x20nofollow\">\n<meta\x20
SF:name=\"viewport\"\x20content=\"width=device-width,initial-scale=1,maxim
SF:um-scale=1\">\n<link\x20rel=\"stylesheet\"\x20id=\"cf_styles-css\"\x20h
SF:ref=\"index_files");
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.70%E=4%D=3/26%OT=22%CT=1%CU=39076%PV=Y%DS=2%DC=T%G=Y%TM=5C99E0A
OS:7%P=x86_64-pc-linux-gnu)SEQ(SP=106%GCD=1%ISR=10D%TI=Z%CI=Z%II=I%TS=8)OPS
OS:(O1=M54DST11NW7%O2=M54DST11NW7%O3=M54DNNT11NW7%O4=M54DST11NW7%O5=M54DST1
OS:1NW7%O6=M54DST11)WIN(W1=7120%W2=7120%W3=7120%W4=7120%W5=7120%W6=7120)ECN
OS:(R=Y%DF=Y%T=40%W=7210%O=M54DNNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=A
OS:S%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R
OS:=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F
OS:=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%
OS:T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD
OS:=S)

Network Distance: 2 hops

TRACEROUTE (using port 25/tcp)
HOP RTT       ADDRESS
1   259.63 ms 10.10.12.1
2   259.70 ms 10.10.10.124

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 190.18 seconds
```
## Openport
```text
22/tcp   open  ssh?
80/tcp   open  http      nginx
443/tcp  open  ssl/https ClownWare Proxy
```

## DNS List
```text
DNS:clownware.htb
DNS:sni147831.clownware.htb
DNS:*.clownware.htb
DNS:proxy.clownware.htb
DNS:console.flujab.htb
DNS:sys.flujab.htb
DNS:smtp.flujab.htb
DNS:vaccine4flu.htb
DNS:bestmedsupply.htb
DNS:custoomercare.megabank.htb
DNS:flowerzrus.htb
DNS:chocolateriver.htb
DNS:meetspinz.htb
DNS:rubberlove.htb
DNS:freeflujab.htb
DNS:flujab.htb
```

