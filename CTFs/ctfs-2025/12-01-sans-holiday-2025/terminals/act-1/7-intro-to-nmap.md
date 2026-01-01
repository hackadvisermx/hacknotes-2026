
1) When run without any options, nmap performs a TCP port scan of the top 1000 ports. Run a default nmap scan of 127.0.12.25 and see which port is open.
```
nmap 127.0.12.25
Starting Nmap 7.80 ( https://nmap.org ) at 2025-11-24 06:09 UTC
Nmap scan report for 127.0.12.25
Host is up (0.000066s latency).
Not shown: 999 closed ports
PORT     STATE SERVICE
8080/tcp open  http-proxy

Nmap done: 1 IP address (1 host up) scanned in 0.26 seconds
```

2) Sometimes the top 1000 ports are not enough. Run an nmap scan of all TCP ports on 127.0.12.25 and see which port is open.
```
nmap 127.0.12.25 -p-
Starting Nmap 7.80 ( https://nmap.org ) at 2025-11-24 06:10 UTC
Nmap scan report for 127.0.12.25
Host is up (0.000048s latency).
Not shown: 65534 closed ports
PORT      STATE SERVICE
24601/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 1.74 seconds
```

3) Nmap can also scan a range of IP addresses.  Scan the range 127.0.12.20 - 127.0.12.28 and see which has a port open.

```
nmap 127.0.12.20-28

Nmap scan report for 127.0.12.20
Host is up (0.00018s latency).
All 1000 scanned ports on 127.0.12.20 are closed

Nmap scan report for 127.0.12.21
Host is up (0.00019s latency).
All 1000 scanned ports on 127.0.12.21 are closed

Nmap scan report for 127.0.12.22
Host is up (0.00018s latency).
All 1000 scanned ports on 127.0.12.22 are closed

Nmap scan report for 127.0.12.23
Host is up (0.00017s latency).
All 1000 scanned ports on 127.0.12.23 are closed

Nmap scan report for 127.0.12.24
Host is up (0.00019s latency).
All 1000 scanned ports on 127.0.12.24 are closed

Nmap scan report for 127.0.12.25
Host is up (0.00019s latency).
Not shown: 999 closed ports
PORT     STATE SERVICE
8080/tcp open  http-proxy

Nmap scan report for 127.0.12.26
Host is up (0.00017s latency).
All 1000 scanned ports on 127.0.12.26 are closed

Nmap scan report for 127.0.12.27
Host is up (0.00016s latency).
All 1000 scanned ports on 127.0.12.27 are closed

Nmap scan report for 127.0.12.28
Host is up (0.00018s latency).
All 1000 scanned ports on 127.0.12.28 are closed

Nmap done: 9 IP addresses (9 hosts up) scanned in 0.71 seconds


```

4) Nmap has a version detection engine, to help determine what services are running on a given port. What service is running on 127.0.12.25 TCP port 8080?
```
 nmap -sV -p 8080 127.0.12.25
Starting Nmap 7.80 ( https://nmap.org ) at 2025-11-24 06:12 UTC
Stats: 0:00:00 elapsed; 0 hosts completed (0 up), 1 undergoing Ping Scan
Ping Scan Timing: About 100.00% done; ETC: 06:12 (0:00:00 remaining)
Nmap scan report for 127.0.12.25
Host is up (0.000067s latency).

PORT     STATE SERVICE VERSION
8080/tcp open  http    SimpleHTTPServer 0.6 (Python 3.10.12)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.66 seconds
```

5) Sometimes you just want to interact with a port, which is a perfect job for Ncat!  Use the ncat tool to connect to TCP port 24601 on 127.0.12.25 and view the banner returned.
```
nc 127.0.12.25 24601
Welcome to the WarDriver 9000!
```

Congratulations, you finished the Intro to Nmap and found the wardriving rig's service!
Type "exit" to close...