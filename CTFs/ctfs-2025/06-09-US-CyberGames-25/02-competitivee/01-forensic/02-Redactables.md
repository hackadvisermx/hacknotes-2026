# Redactables



- crack pdf
```
┌──(root㉿kali)-[/home/…/uscyber/competitive/forensic/redactables]
└─# pdf2john redactable.pdf > hash
                                                                                                                                                                                                                                
┌──(root㉿kali)-[/home/…/uscyber/competitive/forensic/redactables]
└─# john hash -w=/usr/share/wordlists/rockyou.txt 
Using default input encoding: UTF-8
Loaded 1 password hash (PDF [MD5 SHA2 RC4/AES 32/64])
Cost 1 (revision) is 6 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
friends4eva      (redactable.pdf)     
1g 0:00:00:02 DONE (2025-06-13 09:43) 0.3508g/s 3233p/s 3233c/s 3233C/s taiwan..sassy123
Use the "--show --format=PDF" options to display all of the cracked passwords reliably
Session completed. 

```

- quitar el pass del pdf
```
┌──(root㉿kali)-[/home/…/uscyber/competitive/forensic/redactables]
└─# qpdf --password=friends4eva --decrypt redactable.pdf unlocked.pdf 

                                                                                                                                                                                                                                
┌──(root㉿kali)-[/home/…/uscyber/competitive/forensic/redactables]
└─# ls
hash  redactable2.pdf  redactable.pdf  unlocked.pdf

```

- convertir a texto
```
┌──(root㉿kali)-[/home/…/uscyber/competitive/forensic/redactables]
└─# pdfimages -all unlocked.pdf salida




SVUSCG{oops_i_did_it_again_i_didnt_redact}
 
```

### Solución técnica (con GIMP)

Puedes usar **GIMP** para invertir el filtro de distorsión:

#### 🧪 Opción A: Manual en GIMP (recomendado)

1. **Abre `salida-000.jpg` en GIMP**.
    
2. Selecciona el menú:  
    `Filters` → `Distorts` → `Whirl and Pinch…`
    
3. Ajusta el **"Whirl angle"** hacia el negativo del valor original (por ejemplo, si se ve girado a la derecha, usa un ángulo como `-120`).
    
4. Ajusta la **pinch** y el **radius** también si es necesario.
    
5. Haz clic en **OK** hasta que el texto sea legible.
    
6. **Busca el texto** tipo bandera `SVUSCG{...}`.