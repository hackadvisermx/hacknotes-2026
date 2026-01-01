
# Just Look At It

Hot take: they were _always_ actually pretty good

 [lookatthis.jpg](https://ctf.uscybergames.com/files/fa77a137c0da4090c7155f17a46a18c2/lookatthis.jpg?token=eyJ1c2VyX2lkIjoyMjEsInRlYW1faWQiOm51bGwsImZpbGVfaWQiOjQ5fQ.aEyzsA.LsrERVlHyUZKk4aUXTQJbV131dU "lookatthis.jpg")

## Solucion

- Algunos intentos, pero nada:

```
┌──(root㉿kali)-[/home/…/uscyber/competitive/forensic/justlook]
└─# zsteg -a lookatthis.jpg 
[!] #<ZPNG::NotSupported: Unsupported header "\xFF\xD8\xFF\xE0\x00\x10JF" in #<File:lookatthis.jpg>>
                                                                                                                                                                                                                                
┌──(root㉿kali)-[/home/…/uscyber/competitive/forensic/justlook]
└─# strings lookatthis.jpg | grep -iE "flag|uscg|svuscg"

                                                                                                                                                                                                                                
┌──(root㉿kali)-[/home/…/uscyber/competitive/forensic/justlook]
└─# 


SEASON III TEAM

SVUSCG{SEASON_III_TEAM}

SVUSCG{Eth008}


SVUSCG{Quasar}

SVUSCG{nice_nist}

SVUSCG{United_States_Cyber_Team }


SVUSCG{US_Cyber_Team}

```