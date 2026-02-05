# VulnNet: Internal

VulnNet Entertainment learns from its mistakes, and now they have something new for you...

# Task 1VulnNet: Internal

Start Machine

VulnNet Entertainment is a company that learns from its mistakes. They quickly realized that they can't make a properly secured web application so they gave up on that idea. Instead, they decided to set up internal services for business purposes. As usual, you're tasked to perform a penetration test of their network and report your findings.  

- Difficulty: Easy/Medium
- Operating System: Linux

This machine was designed to be quite the opposite of the previous machines in this series and it focuses on internal services. It's supposed to show you how you can retrieve interesting information and use it to gain system access. Report your findings by submitting the correct flags.

Note: It _might_ take 3-5 minutes for all the services to boot.

Icon made by [Freepik](https://www.freepik.com/) from [www.flaticon.com](http://www.flaticon.com/)  

## Escaneo

```
vulentinternal nmap -n -Pn -sV -sC --min-rate 5000 -v -p- -oN nmap 10.82.131.187
Starting Nmap 7.93 ( https://nmap.org ) at 2026-02-01 16:10 UTC
NSE: Loaded 155 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 16:10
Completed NSE at 16:10, 0.00s elapsed
Initiating NSE at 16:10
Completed NSE at 16:10, 0.00s elapsed
Initiating NSE at 16:10
Completed NSE at 16:10, 0.00s elapsed
Initiating SYN Stealth Scan at 16:10
Scanning 10.82.131.187 [65535 ports]
Discovered open port 111/tcp on 10.82.131.187
Discovered open port 139/tcp on 10.82.131.187
Discovered open port 445/tcp on 10.82.131.187
Discovered open port 22/tcp on 10.82.131.187
Discovered open port 873/tcp on 10.82.131.187
Discovered open port 56127/tcp on 10.82.131.187
Discovered open port 2049/tcp on 10.82.131.187
Discovered open port 44491/tcp on 10.82.131.187
Discovered open port 60099/tcp on 10.82.131.187
Discovered open port 6379/tcp on 10.82.131.187
Discovered open port 34343/tcp on 10.82.131.187
Completed SYN Stealth Scan at 16:10, 14.12s elapsed (65535 total ports)
Initiating Service scan at 16:10
Scanning 11 services on 10.82.131.187
Completed Service scan at 16:10, 16.75s elapsed (11 services on 1 host)
NSE: Script scanning 10.82.131.187.
Initiating NSE at 16:10
Completed NSE at 16:10, 5.63s elapsed
Initiating NSE at 16:10
Completed NSE at 16:10, 0.77s elapsed
Initiating NSE at 16:10
Completed NSE at 16:10, 0.00s elapsed
Nmap scan report for 10.82.131.187
Host is up (0.18s latency).
Not shown: 65523 closed tcp ports (reset)
PORT      STATE    SERVICE     VERSION
22/tcp    open     ssh         OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 89de08a07e20147ab970034fd69e1d58 (RSA)
|   256 8758c5e36c7873f86841054a4e9e8c1d (ECDSA)
|_  256 b9c842fdd766d481c4854acd70e98b65 (ED25519)
111/tcp   open     rpcbind     2-4 (RPC #100000)
| rpcinfo:
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3           2049/udp   nfs
|   100003  3           2049/udp6  nfs
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      40421/udp6  mountd
|   100005  1,2,3      44487/udp   mountd
|   100005  1,2,3      51095/tcp6  mountd
|   100005  1,2,3      56127/tcp   mountd
|   100021  1,3,4      34343/tcp   nlockmgr
|   100021  1,3,4      36881/tcp6  nlockmgr
|   100021  1,3,4      39549/udp   nlockmgr
|   100021  1,3,4      49452/udp6  nlockmgr
|   100227  3           2049/tcp   nfs_acl
|   100227  3           2049/tcp6  nfs_acl
|   100227  3           2049/udp   nfs_acl
|_  100227  3           2049/udp6  nfs_acl
139/tcp   open     netbios-ssn Samba smbd 4.6.2
445/tcp   open     netbios-ssn Samba smbd 4.6.2
873/tcp   open     rsync       (protocol version 31)
2049/tcp  open     nfs_acl     3 (RPC #100227)
6379/tcp  open     redis       Redis key-value store
9090/tcp  filtered zeus-admin
34343/tcp open     nlockmgr    1-4 (RPC #100021)
44491/tcp open     mountd      1-3 (RPC #100005)
56127/tcp open     mountd      1-3 (RPC #100005)
60099/tcp open     mountd      1-3 (RPC #100005)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| nbstat: NetBIOS name: , NetBIOS user: <unknown>, NetBIOS MAC: 000000000000 (Xerox)
| Names:
|   \x01\x02__MSBROWSE__\x02<01>  Flags: <group><active>
|   <00>                 Flags: <unique><active>
|   <03>                 Flags: <unique><active>
|   <20>                 Flags: <unique><active>
|   WORKGROUP<00>        Flags: <group><active>
|   WORKGROUP<1d>        Flags: <unique><active>
|_  WORKGROUP<1e>        Flags: <group><active>
| smb2-time:
|   date: 2026-02-01T16:10:39
|_  start_date: N/A
| smb2-security-mode:
|   311:
|_    Message signing enabled but not required

NSE: Script Post-scanning.
Initiating NSE at 16:10
Completed NSE at 16:10, 0.00s elapsed
Initiating NSE at 16:10
Completed NSE at 16:10, 0.00s elapsed
Initiating NSE at 16:10
Completed NSE at 16:10, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 37.59 seconds
           Raw packets sent: 69114 (3.041MB) | Rcvd: 68831 (2.755MB)
```

## Answer the questions below

### What is the services flag? (services.txt)

```
vulentinternal smbclient -L 10.82.131.187
Password for [WORKGROUP\root]:

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        shares          Disk      VulnNet Business Shares
        IPC$            IPC       IPC Service (ip-10-82-131-187 server (Samba, Ubuntu))
SMB1 disabled -- no workgroup available
➜  vulentinternal smbclient //10.82.131.187/shares
Password for [WORKGROUP\root]:
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Tue Feb  2 09:20:09 2021
  ..                                  D        0  Tue Feb  2 09:28:11 2021
  temp                                D        0  Sat Feb  6 11:45:10 2021
  data                                D        0  Tue Feb  2 09:27:33 2021

                15376180 blocks of size 1024. 2030776 blocks available
smb: \> cd data
lsmb: \data\> ls
  .                                   D        0  Tue Feb  2 09:27:33 2021
  ..                                  D        0  Tue Feb  2 09:20:09 2021
  data.txt                            N       48  Tue Feb  2 09:21:18 2021
  business-req.txt                    N      190  Tue Feb  2 09:27:33 2021

                15376180 blocks of size 1024. 2030776 blocks available
smb: \data\> mget *txt
Get file data.txt? y
getting file \data\data.txt of size 48 as data.txt (0.1 KiloBytes/sec) (average 0.1 KiloBytes/sec)
Get file business-req.txt? y
getting file \data\business-req.txt of size 190 as business-req.txt (0.2 KiloBytes/sec) (average 0.2 KiloBytes/sec)
smb: \data\>

 vulentinternal cat *txt
We just wanted to remind you that we’re waiting for the DOCUMENT you agreed to send us so we can complete the TRANSACTION we discussed.
If you have any questions, please text or phone us.
Purge regularly data that is not needed anymore



 vulentinternal smbclient //10.82.131.187/shares
Password for [WORKGROUP\root]:
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Tue Feb  2 09:20:09 2021
  ..                                  D        0  Tue Feb  2 09:28:11 2021
  temp                                D        0  Sat Feb  6 11:45:10 2021
  data                                D        0  Tue Feb  2 09:27:33 2021
c
                15376180 blocks of size 1024. 2030776 blocks available
smb: \> cd temp
smb: \temp\> dir
  .                                   D        0  Sat Feb  6 11:45:10 2021
  ..                                  D        0  Tue Feb  2 09:20:09 2021
  services.txt                        N       38  Sat Feb  6 11:45:09 2021

                15376180 blocks of size 1024. 2030776 blocks available
smb: \temp\> get services.txt
getting file \temp\services.txt of size 38 as services.txt (0.1 KiloBytes/sec) (average 0.1 KiloBytes/sec)
smb: \temp\> quit
➜  vulentinternal cat services.txt
THM{0a09d51e488f5fa105d8d866a497440a}
```

### What is the internal flag? ("internal flag")

 

What is the user flag? (user.txt)

Check

What is the root flag? (root.txt)