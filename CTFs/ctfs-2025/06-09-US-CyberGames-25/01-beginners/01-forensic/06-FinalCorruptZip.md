


- Corregir el encabezado del archivo .zip

```
50 4B 03 04


```

- extraemos
```
┌──(root㉿kali)-[/home/…/tmp/uscyber/forensic/finalcorrupt]
└─# unzip FinalCorruptZip.zip 
Archive:  FinalCorruptZip.zip
  inflating: CorruptPNG.png          
                                                                                                              
┌──(root㉿kali)-[/home/…/tmp/uscyber/forensic/finalcorrupt]
└─# eog CorruptPNG.png  
                                                                                                              
┌──(root㉿kali)-[/home/…/tmp/uscyber/forensic/finalcorrupt]
└─# file CorruptPNG.png     
CorruptPNG.png: data

```

- corregir el encabezado del .png
```
89 50 4E 47 0D 0A 1A 0A
```

- abrir la imagen ahi esta la flag
```
SVBGR{m4g1C_B1t3s_yUmmmmm}
```