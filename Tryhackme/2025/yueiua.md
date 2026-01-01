
# yueiua


# Task 1 - U.A. High School

Join us in the mission to protect the digital world of superheroes! U.A., the most renowned Superhero Academy, is looking for a superhero to test the security of our new site.

Our site is a reflection of our school values, designed by our engineers with incredible Quirks. We have gone to great lengths to create a secure platform that reflects the exceptional education of the U.A.

Please allow the machine 3 - 5 minutes to fully boot.

## Escaneo
```
┌──(kali㉿kali)-[~/tmp/tryhackme/yueiua]
└─$ nmap -n -Pn -sV --min-rate 9000 -vv -p- -oN nmap 10.81.177.249          
Starting Nmap 7.95 ( https://nmap.org ) at 2025-12-21 09:34 CST
NSE: Loaded 47 scripts for scanning.
Initiating SYN Stealth Scan at 09:34
Scanning 10.81.177.249 [65535 ports]
Discovered open port 80/tcp on 10.81.177.249
Discovered open port 22/tcp on 10.81.177.249
Increasing send delay for 10.81.177.249 from 0 to 5 due to max_successful_tryno increase to 4
Increasing send delay for 10.81.177.249 from 5 to 10 due to max_successful_tryno increase to 5
Increasing send delay for 10.81.177.249 from 10 to 20 due to max_successful_tryno increase to 6
Increasing send delay for 10.81.177.249 from 20 to 40 due to 2927 out of 9756 dropped probes since last increase.
Increasing send delay for 10.81.177.249 from 40 to 80 due to max_successful_tryno increase to 7
Increasing send delay for 10.81.177.249 from 80 to 160 due to max_successful_tryno increase to 8
Increasing send delay for 10.81.177.249 from 160 to 320 due to 547 out of 1821 dropped probes since last increase.
Increasing send delay for 10.81.177.249 from 320 to 640 due to 6490 out of 21632 dropped probes since last increase.
Completed SYN Stealth Scan at 09:34, 13.25s elapsed (65535 total ports)
Initiating Service scan at 09:34
Scanning 2 services on 10.81.177.249
Completed Service scan at 09:34, 6.37s elapsed (2 services on 1 host)
NSE: Script scanning 10.81.177.249.
NSE: Starting runlevel 1 (of 2) scan.
Initiating NSE at 09:34
Completed NSE at 09:34, 0.79s elapsed
NSE: Starting runlevel 2 (of 2) scan.
Initiating NSE at 09:34
Completed NSE at 09:34, 0.73s elapsed
Nmap scan report for 10.81.177.249
Host is up, received user-set (0.18s latency).
Scanned at 2025-12-21 09:34:03 CST for 22s
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 62 OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    syn-ack ttl 62 Apache httpd 2.4.41 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21.39 seconds
           Raw packets sent: 110261 (4.851MB) | Rcvd: 91886 (3.676MB)

```

## directorios
```
┌──(kali㉿kali)-[~/tmp/tryhackme/yueiua]
└─$ ffuf -u http://10.81.177.249/assets/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 500 -ic -e .php,.txt,.bak

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://10.81.177.249/assets/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
 :: Extensions       : .php .txt .bak 
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 500
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
________________________________________________

index.php               [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 197ms]
images                  [Status: 301, Size: 322, Words: 20, Lines: 10, Duration: 198ms]
.php                    [Status: 403, Size: 278, Words: 20, Lines: 10, Duration: 205ms]
                        [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 219ms]
.php                    [Status: 403, Size: 278, Words: 20, Lines: 10, Duration: 185ms]
                        [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 189ms]

```

```
┌──(kali㉿kali)-[~/tmp/tryhackme/yueiua]
└─$ ffuf -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt \
     -u "http://10.81.177.249/assets/index.php?FUZZ=id"  -fs 0  

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://10.81.177.249/assets/index.php?FUZZ=id
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 0
________________________________________________

cmd                     [Status: 200, Size: 72, Words: 1, Lines: 1, Duration: 183ms]
:: Progress: [6453/6453] :: Job [1/1] :: 189 req/sec :: Duration: [0:00:33] :: Errors: 0 ::

```

