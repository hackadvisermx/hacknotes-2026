
# Charlie

SIV Pipeline Forensics Group 5

 [charlie.jpg](https://ctf.uscybergames.com/files/85a24081168818b5e32f789cf30f0c8c/charlie.jpg?token=eyJ1c2VyX2lkIjoyMjEsInRlYW1faWQiOm51bGwsImZpbGVfaWQiOjE4fQ.aEeUDQ.RGqpA0ahvJK41BzqosmYnTPSTWI "charlie.jpg")


## Solucion

```
┌──(kali㉿kali)-[~/tmp/uscyber]
└─$ sudo unzip charlie.jpg
Archive:  charlie.jpg
warning [charlie.jpg]:  4477372 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: flag.txt     


┌──(root㉿kali)-[/home/kali/tmp/uscyber]
└─# cat flag.txt | base64 -d > flag.jpg 


SVBGR{B1NW4LK_F7N}

```


