
# USCG Admin was H@cked

One of the US Cyber Games administrators had their system hacked. There is a malicious startup Application set to run when a user logs in. Can you help find it?

 [registry.7z](https://ctf.uscybergames.com/files/b9c254f8f8ebfb7d26b8c3a5f4a642a3/registry.7z?token=eyJ1c2VyX2lkIjoyMjEsInRlYW1faWQiOm51bGwsImZpbGVfaWQiOjQwfQ.aEyM7g.QS6OtSG-aX67JW_0nIQaeA8tCEw "registry.7z")

## Solucion

```
7z x registry.7z


┌──(root㉿kali)-[/home/…/usgs-admin/registry/Users/uscgadmin]
└─# regripper -r NTUSER.DAT -f ntuser > ntuser.txt


┌──(root㉿kali)-[/home/…/usgs-admin/registry/Users/uscgadmin]
└─# cat ntuser.txt | dos2unix |  grep -i SV       
OSVersion
OSVersion value not found.
   SVUSCG{uf0undme} - C:\Users\uscgadmin\Documents\MSDCSC\msdcsc.exe
 



```