# Echo

SIV Pipeline Forensics Group 3

 [Echo.jpg](https://ctf.uscybergames.com/files/ca192acdf28c26ab8ea72b485bef1ccd/Echo.jpg?token=eyJ1c2VyX2lkIjoyMjEsInRlYW1faWQiOm51bGwsImZpbGVfaWQiOjE5fQ.aEg6wg.v9EzbPein64cn-aD1r3gnLE52Yo "Echo.jpg")
## Solucion

```
┌──(root㉿kali)-[/home/…/tmp/uscyber/forensic/echo]
└─# strings Echo.jpg -n 10 | grep SV
SVBRG{HEXEDITING}

```