
# Intranet

# Task 1 - Find vulnerabilities and gain root access

The web application development company SecureSolaCoders has created their own intranet page. The developers are still very young and inexperienced, but they ensured their boss (Magnus) that the web application was secured appropriately. The developers said, "Don't worry, Magnus. We have learnt from our previous mistakes. It won't happen again". However, Magnus was not convinced, as they had introduced many strange vulnerabilities in their customers' applications earlier.

Magnus hired you as a third-party to conduct a penetration test of their web application. Can you successfully exploit the app and achieve root access?

Start the VM by pressing the green "Start Machine" button. Please allow the machine 3 - 5 minutes to fully boot.

## Scan

```
 nmap -n -Pn -sV --min-rate 1000 -v -p- -oN nmap 10.81.144.55
Starting Nmap 7.93 ( https://nmap.org ) at 2026-01-02 17:09 UTC
NSE: Loaded 45 scripts for scanning.
Initiating SYN Stealth Scan at 17:09
Scanning 10.81.144.55 [65535 ports]
Discovered open port 8080/tcp on 10.81.144.55
Discovered open port 80/tcp on 10.81.144.55
Discovered open port 21/tcp on 10.81.144.55
Discovered open port 23/tcp on 10.81.144.55
Discovered open port 22/tcp on 10.81.144.55
Increasing send delay for 10.81.144.55 from 0 to 5 due to max_successful_tryno increase to 4
SYN Stealth Scan Timing: About 43.16% done; ETC: 17:10 (0:00:41 remaining)
Discovered open port 7/tcp on 10.81.144.55
Completed SYN Stealth Scan at 17:10, 72.47s elapsed (65535 total ports)
Initiating Service scan at 17:10
Scanning 6 services on 10.81.144.55
Completed Service scan at 17:12, 99.43s elapsed (6 services on 1 host)
NSE: Script scanning 10.81.144.55.
Initiating NSE at 17:12
Completed NSE at 17:12, 0.81s elapsed
Initiating NSE at 17:12
Completed NSE at 17:12, 1.22s elapsed
Nmap scan report for 10.81.144.55
Host is up (0.18s latency).
Not shown: 65529 closed tcp ports (reset)
PORT     STATE SERVICE    VERSION
7/tcp    open  echo
21/tcp   open  ftp        vsftpd 3.0.5
22/tcp   open  ssh        OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
23/tcp   open  tcpwrapped
80/tcp   open  http       Apache httpd 2.4.41 ((Ubuntu))
8080/tcp open  http-proxy Werkzeug/2.2.2 Python/3.8.10
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port8080-TCP:V=7.93%I=7%D=1/2%Time=6957FC21%P=aarch64-unknown-linux-gnu
SF:%r(GetRequest,18A,"HTTP/1\.1\x20302\x20FOUND\r\nServer:\x20Werkzeug/2\.
SF:2\.2\x20Python/3\.8\.10\r\nDate:\x20Fri,\x2002\x20Jan\x202026\x2017:10:
SF:56\x20GMT\r\nContent-Type:\x20text/html;\x20charset=utf-8\r\nContent-Le
SF:ngth:\x20199\r\nLocation:\x20/login\r\nConnection:\x20close\r\n\r\n<!do
SF:ctype\x20html>\n<html\x20lang=en>\n<title>Redirecting\.\.\.</title>\n<h
SF:1>Redirecting\.\.\.</h1>\n<p>You\x20should\x20be\x20redirected\x20autom
SF:atically\x20to\x20the\x20target\x20URL:\x20<a\x20href=\"/login\">/login
SF:</a>\.\x20If\x20not,\x20click\x20the\x20link\.\n")%r(HTTPOptions,C7,"HT
SF:TP/1\.1\x20200\x20OK\r\nServer:\x20Werkzeug/2\.2\.2\x20Python/3\.8\.10\
SF:r\nDate:\x20Fri,\x2002\x20Jan\x202026\x2017:10:57\x20GMT\r\nContent-Typ
SF:e:\x20text/html;\x20charset=utf-8\r\nAllow:\x20GET,\x20OPTIONS,\x20HEAD
SF:\r\nContent-Length:\x200\r\nConnection:\x20close\r\n\r\n")%r(RTSPReques
SF:t,1F4,"<!DOCTYPE\x20HTML\x20PUBLIC\x20\"-//W3C//DTD\x20HTML\x204\.01//E
SF:N\"\n\x20\x20\x20\x20\x20\x20\x20\x20\"http://www\.w3\.org/TR/html4/str
SF:ict\.dtd\">\n<html>\n\x20\x20\x20\x20<head>\n\x20\x20\x20\x20\x20\x20\x
SF:20\x20<meta\x20http-equiv=\"Content-Type\"\x20content=\"text/html;chars
SF:et=utf-8\">\n\x20\x20\x20\x20\x20\x20\x20\x20<title>Error\x20response</
SF:title>\n\x20\x20\x20\x20</head>\n\x20\x20\x20\x20<body>\n\x20\x20\x20\x
SF:20\x20\x20\x20\x20<h1>Error\x20response</h1>\n\x20\x20\x20\x20\x20\x20\
SF:x20\x20<p>Error\x20code:\x20400</p>\n\x20\x20\x20\x20\x20\x20\x20\x20<p
SF:>Message:\x20Bad\x20request\x20version\x20\('RTSP/1\.0'\)\.</p>\n\x20\x
SF:20\x20\x20\x20\x20\x20\x20<p>Error\x20code\x20explanation:\x20HTTPStatu
SF:s\.BAD_REQUEST\x20-\x20Bad\x20request\x20syntax\x20or\x20unsupported\x2
SF:0method\.</p>\n\x20\x20\x20\x20</body>\n</html>\n")%r(FourOhFourRequest
SF:,184,"HTTP/1\.1\x20404\x20NOT\x20FOUND\r\nServer:\x20Werkzeug/2\.2\.2\x
SF:20Python/3\.8\.10\r\nDate:\x20Fri,\x2002\x20Jan\x202026\x2017:10:57\x20
SF:GMT\r\nContent-Type:\x20text/html;\x20charset=utf-8\r\nContent-Length:\
SF:x20207\r\nConnection:\x20close\r\n\r\n<!doctype\x20html>\n<html\x20lang
SF:=en>\n<title>404\x20Not\x20Found</title>\n<h1>Not\x20Found</h1>\n<p>The
SF:\x20requested\x20URL\x20was\x20not\x20found\x20on\x20the\x20server\.\x2
SF:0If\x20you\x20entered\x20the\x20URL\x20manually\x20please\x20check\x20y
SF:our\x20spelling\x20and\x20try\x20again\.</p>\n");
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 174.14 seconds
           Raw packets sent: 71991 (3.168MB) | Rcvd: 71233 (2.851MB)
```

### Port 80
```
curl -I 10.81.144.55
HTTP/1.1 200 OK
Date: Fri, 02 Jan 2026 17:19:09 GMT
Server: Apache/2.4.41 (Ubuntu)
Last-Modified: Mon, 07 Nov 2022 09:35:16 GMT
ETag: "6f-5ecde2421fe3a"
Accept-Ranges: bytes
Content-Length: 111
Vary: Accept-Encoding
Content-Type: text/html
```


### Port 8080

```
curl -I 10.81.144.55:8080/login
HTTP/1.1 200 OK
Server: Werkzeug/2.2.2 Python/3.8.10
Date: Fri, 02 Jan 2026 17:20:16 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 2154
Connection: close
```


#### Directorios en 8080

```
 ffuf -u http://10.81.144.55:8080/FUZZ  -w /usr/share/wordlists/directory-list-2.3-medium.txt -ic -t 500 -e .php,.txt

        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://10.81.144.55:8080/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory-list-2.3-medium.txt
 :: Extensions       : .php .txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 500
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
________________________________________________
                        [Status: 302, Size: 199, Words: 18, Lines: 6, Duration: 188ms]
home                    [Status: 302, Size: 199, Words: 18, Lines: 6, Duration: 322ms]
admin                   [Status: 302, Size: 199, Words: 18, Lines: 6, Duration: 188ms]
login                   [Status: 200, Size: 2154, Words: 285, Lines: 107, Duration: 986ms]
external                [Status: 302, Size: 199, Words: 18, Lines: 6, Duration: 321ms]
sms                     [Status: 302, Size: 199, Words: 18, Lines: 6, Duration: 333ms]
logout                  [Status: 302, Size: 199, Words: 18, Lines: 6, Duration: 274ms]
application             [Status: 403, Size: 213, Words: 23, Lines: 6, Duration: 253ms]
internal                [Status: 302, Size: 199, Words: 18, Lines: 6, Duration: 281ms]
                        [Status: 302, Size: 199, Words: 18, Lines: 6, Duration: 317ms]
temporary               [Status: 403, Size: 213, Words: 23, Lines: 6, Duration: 312ms]
:: Progress: [95088/220547] :: Job [1/1] :: 706 req/sec :: Duration: [0:02:23] :: Errors: 0 ::

```
#### /robots.txt
```
http://10.81.144.55:8080/robots.txt
<!-- Try harder --!>

```

#### /login
- si intentamos sqli con: ' en user o password
```
**Error:** Hacking attempt detected! You have been logged as 192.168.216.31. (Detected illegal chars in username).

<!--- Any bugs? Please report them to our developer team. We have an open bug bounty program! For any inquiries, contact devops@securesolacoders.no. Sincerely, anders (Senior Developer) -->
```



## Answer the questions below

### What is the first web application flag?  

 Think about the information you have gathered so far from the web application - usernames, company name, etc. You might want to generate a password list or make educated guesses.

 ```
users.txt

admin@securesolacoders.no
devops@securesolacoders.no
anders@securesolacoders.no
x magnus@securesolacoders.no


baselist.txt

sms
securesolacoders
devops
anders
admin
SecureSolaCoders
magnus




tail /etc/john/john.conf

[List.Rules:TryHackMe-Intranet]
Az"[0-9]"
Az"[0-9][0-9]"
Az"[0-9][0-9][0-9]"
Az"[0-9][0-9][0-9][0-9]"
Az"[0-9]" $[!$§$%/()=?*@]






 
 ```

```
cewl -w baselist.txt -d 5 -m4 http://10.80.157.114:8080/login

CeWL 5.5.2 (Grouping) Robin Wood (robin@digi.ninja) (https://digi.ninja/)
➜  securesolacodersintra cat baselist.txt
Intranet
login
mail
Password
Proudly
hosted
maintained
developed
SecureSolaCoders
bugs
Please
report
them
developer
team
have
open
bounty
program
inquiries
contact
devops
securesolacoders
Sincerely
anders
Senior
Developer



cat baselist.txt
anders
devops
securesolacoders
ssc
sr
senior
developer

```

```
john -wordlist:baselist.txt -rules:TryHackMe-Intranet -stdout > wordlist.txt   
Using default input encoding: UTF-8
Press 'q' or Ctrl-C to abort, almost any other key for status
303210p 0:00:00:00 100.00% (2026-01-02 22:47) 1684Kp/s Developer9@

```


### What is the second web application flag?  

 

### What is the third web application flag?  

 

### What is the fourth web application flag?  

 

### What is the user.txt flag?  

 

### What is the user2.txt flag?  

 

### What is the root.txt flag?