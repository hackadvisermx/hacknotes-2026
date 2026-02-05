
# TryHack3M: Bricks Heist
Crack the code, command the exploit! Dive into the heart of the system with just an RCE CVE as your key.
https://tryhackme.com/room/tryhack3mbricksheist


# Task 1 Challenge

Start Machine

From Three Million Bricks to Three Million Transactions!  

Brick Press Media Co. was working on creating a brand-new web theme that represents a renowned wall using three million byte bricks. Agent Murphy comes with a streak of bad luck. And here we go again: the server is compromised, and they've lost access.  
  
Can you hack back the server and identify what happened there?

## Escaneo

```
 nmap -n -Pn -sV -sC --min-rate 5000 -v -p- -oN nmap 10.80.153.210
Starting Nmap 7.93 ( https://nmap.org ) at 2026-01-30 00:16 UTC
NSE: Loaded 155 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 00:16
Completed NSE at 00:16, 0.00s elapsed
Initiating NSE at 00:16
Completed NSE at 00:16, 0.00s elapsed
Initiating NSE at 00:16
Completed NSE at 00:16, 0.00s elapsed
Initiating SYN Stealth Scan at 00:16
Scanning 10.80.153.210 [65535 ports]
Discovered open port 80/tcp on 10.80.153.210
Discovered open port 3306/tcp on 10.80.153.210
Discovered open port 443/tcp on 10.80.153.210
Discovered open port 22/tcp on 10.80.153.210
Increasing send delay for 10.80.153.210 from 0 to 5 due to max_successful_tryno increase to 4
Increasing send delay for 10.80.153.210 from 5 to 10 due to max_successful_tryno increase to 5
Increasing send delay for 10.80.153.210 from 10 to 20 due to 535 out of 1781 dropped probes since last increase.
Increasing send delay for 10.80.153.210 from 20 to 40 due to max_successful_tryno increase to 6
Increasing send delay for 10.80.153.210 from 40 to 80 due to 4183 out of 13941 dropped probes since last increase.
Completed SYN Stealth Scan at 00:17, 18.68s elapsed (65535 total ports)
Initiating Service scan at 00:17
Scanning 4 services on 10.80.153.210
Completed Service scan at 00:18, 87.59s elapsed (4 services on 1 host)
NSE: Script scanning 10.80.153.210.
Initiating NSE at 00:18
Completed NSE at 00:18, 9.70s elapsed
Initiating NSE at 00:18
Completed NSE at 00:18, 3.34s elapsed
Initiating NSE at 00:18
Completed NSE at 00:18, 0.00s elapsed
Nmap scan report for 10.80.153.210
Host is up (0.19s latency).
Not shown: 65531 closed tcp ports (reset)
PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 71b70ccf2c32f560a3653561a263e558 (RSA)
|   256 9fd3d36f893820a97c35e3e3d76f3874 (ECDSA)
|_  256 0ec276a0cd3a9b36b15c784f6199f847 (ED25519)
80/tcp   open  http     WebSockify Python/3.8.10
|_http-server-header: WebSockify Python/3.8.10
| fingerprint-strings:
|   GetRequest:
|     HTTP/1.1 405 Method Not Allowed
|     Server: WebSockify Python/3.8.10
|     Date: Fri, 30 Jan 2026 00:17:09 GMT
|     Connection: close
|     Content-Type: text/html;charset=utf-8
|     Content-Length: 472
|     <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
|     "http://www.w3.org/TR/html4/strict.dtd">
|     <html>
|     <head>
|     <meta http-equiv="Content-Type" content="text/html;charset=utf-8">
|     <title>Error response</title>
|     </head>
|     <body>
|     <h1>Error response</h1>
|     <p>Error code: 405</p>
|     <p>Message: Method Not Allowed.</p>
|     <p>Error code explanation: 405 - Specified method is invalid for this resource.</p>
|     </body>
|     </html>
|   HTTPOptions:
|     HTTP/1.1 501 Unsupported method ('OPTIONS')
|     Server: WebSockify Python/3.8.10
|     Date: Fri, 30 Jan 2026 00:17:09 GMT
|     Connection: close
|     Content-Type: text/html;charset=utf-8
|     Content-Length: 500
|     <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
|     "http://www.w3.org/TR/html4/strict.dtd">
|     <html>
|     <head>
|     <meta http-equiv="Content-Type" content="text/html;charset=utf-8">
|     <title>Error response</title>
|     </head>
|     <body>
|     <h1>Error response</h1>
|     <p>Error code: 501</p>
|     <p>Message: Unsupported method ('OPTIONS').</p>
|     <p>Error code explanation: HTTPStatus.NOT_IMPLEMENTED - Server does not support this operation.</p>
|     </body>
|_    </html>
|_http-title: Error response
443/tcp  open  ssl/http Apache httpd
|_http-server-header: Apache
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: organizationName=Internet Widgits Pty Ltd/stateOrProvinceName=Some-State/countryName=US
| Issuer: organizationName=Internet Widgits Pty Ltd/stateOrProvinceName=Some-State/countryName=US
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2024-04-02T11:59:14
| Not valid after:  2025-04-02T11:59:14
| MD5:   f1df99bcd5ab5a5a570950994adda385
|_SHA-1: 1f2654bbe2c5b4a11f625ea0af00026135da23c3
|_http-title: Brick by Brick
|_http-generator: WordPress 6.5
| tls-alpn:
|   h2
|_  http/1.1
| http-robots.txt: 1 disallowed entry
|_/wp-admin/
| http-methods:
|_  Supported Methods: GET HEAD POST OPTIONS
3306/tcp open  mysql    MySQL (unauthorized)
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port80-TCP:V=7.93%I=7%D=1/30%Time=697BF885%P=aarch64-unknown-linux-gnu%
SF:r(GetRequest,291,"HTTP/1\.1\x20405\x20Method\x20Not\x20Allowed\r\nServe
SF:r:\x20WebSockify\x20Python/3\.8\.10\r\nDate:\x20Fri,\x2030\x20Jan\x2020
SF:26\x2000:17:09\x20GMT\r\nConnection:\x20close\r\nContent-Type:\x20text/
SF:html;charset=utf-8\r\nContent-Length:\x20472\r\n\r\n<!DOCTYPE\x20HTML\x
SF:20PUBLIC\x20\"-//W3C//DTD\x20HTML\x204\.01//EN\"\n\x20\x20\x20\x20\x20\
SF:x20\x20\x20\"http://www\.w3\.org/TR/html4/strict\.dtd\">\n<html>\n\x20\
SF:x20\x20\x20<head>\n\x20\x20\x20\x20\x20\x20\x20\x20<meta\x20http-equiv=
SF:\"Content-Type\"\x20content=\"text/html;charset=utf-8\">\n\x20\x20\x20\
SF:x20\x20\x20\x20\x20<title>Error\x20response</title>\n\x20\x20\x20\x20</
SF:head>\n\x20\x20\x20\x20<body>\n\x20\x20\x20\x20\x20\x20\x20\x20<h1>Erro
SF:r\x20response</h1>\n\x20\x20\x20\x20\x20\x20\x20\x20<p>Error\x20code:\x
SF:20405</p>\n\x20\x20\x20\x20\x20\x20\x20\x20<p>Message:\x20Method\x20Not
SF:\x20Allowed\.</p>\n\x20\x20\x20\x20\x20\x20\x20\x20<p>Error\x20code\x20
SF:explanation:\x20405\x20-\x20Specified\x20method\x20is\x20invalid\x20for
SF:\x20this\x20resource\.</p>\n\x20\x20\x20\x20</body>\n</html>\n")%r(HTTP
SF:Options,2B9,"HTTP/1\.1\x20501\x20Unsupported\x20method\x20\('OPTIONS'\)
SF:\r\nServer:\x20WebSockify\x20Python/3\.8\.10\r\nDate:\x20Fri,\x2030\x20
SF:Jan\x202026\x2000:17:09\x20GMT\r\nConnection:\x20close\r\nContent-Type:
SF:\x20text/html;charset=utf-8\r\nContent-Length:\x20500\r\n\r\n<!DOCTYPE\
SF:x20HTML\x20PUBLIC\x20\"-//W3C//DTD\x20HTML\x204\.01//EN\"\n\x20\x20\x20
SF:\x20\x20\x20\x20\x20\"http://www\.w3\.org/TR/html4/strict\.dtd\">\n<htm
SF:l>\n\x20\x20\x20\x20<head>\n\x20\x20\x20\x20\x20\x20\x20\x20<meta\x20ht
SF:tp-equiv=\"Content-Type\"\x20content=\"text/html;charset=utf-8\">\n\x20
SF:\x20\x20\x20\x20\x20\x20\x20<title>Error\x20response</title>\n\x20\x20\
SF:x20\x20</head>\n\x20\x20\x20\x20<body>\n\x20\x20\x20\x20\x20\x20\x20\x2
SF:0<h1>Error\x20response</h1>\n\x20\x20\x20\x20\x20\x20\x20\x20<p>Error\x
SF:20code:\x20501</p>\n\x20\x20\x20\x20\x20\x20\x20\x20<p>Message:\x20Unsu
SF:pported\x20method\x20\('OPTIONS'\)\.</p>\n\x20\x20\x20\x20\x20\x20\x20\
SF:x20<p>Error\x20code\x20explanation:\x20HTTPStatus\.NOT_IMPLEMENTED\x20-
SF:\x20Server\x20does\x20not\x20support\x20this\x20operation\.</p>\n\x20\x
SF:20\x20\x20</body>\n</html>\n");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
Initiating NSE at 00:18
Completed NSE at 00:18, 0.00s elapsed
Initiating NSE at 00:18
Completed NSE at 00:18, 0.00s elapsed
Initiating NSE at 00:18
Completed NSE at 00:18, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 119.59 seconds
```





## Answer the questions below

What is the content of the hidden .txt file in the web folder?

```

```



What is the name of the suspicious process?  

Check

What is the service name affiliated with the suspicious process?  

Check

What is the log file name of the miner instance?  

Check

What is the wallet address of the miner instance?  

Check

The wallet address used has been involved in transactions between wallets belonging to which threat group?
