
# Actividad 2 - Viernes 29 de Agosto de 2025

Opciones de configuración:

## **Instalación limpia del SO**
- Imagenes ISO Linux
	- [Ubuntu](https://ubuntu.com/download/desktop)
	- [Debian](https://www.debian.org/download.es.html)
	- [KaliLinux](https://www.kali.org/get-kali/#kali-installer-images)
	- [Parrot](https://parrotsec.org/download/)
- Utileras de hacer media bootable:
	- [Rufus/](https://rufus.ie/es/)
	- [Balena Etcher](https://etcher.balena.io/)
- Referencia: [Guia instalacion limpia]([https://www.linkedin.com/advice/0/how-do-you-perform-clean-install-operating-system](https://www.linkedin.com/advice/0/how-do-you-perform-clean-install-operating-system))
## **Arranque dual**
	- Referencia: [Guía Arranque dual]([https://www.freecodecamp.org/news/how-to-dual-boot-windows-10-and-ubuntu-linux-dual-booting-tutorial/](https://www.freecodecamp.org/news/how-to-dual-boot-windows-10-and-ubuntu-linux-dual-booting-tutorial/))

 ## **WSL**
- Comandos básicos
```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
wsl --list –-online
wsl --install Ubuntu
wsl --set-default-version 2
wsl --list 
wsl --unregister Ubuntu
```
- Referencia:  [Guia instalar WSL manual](https://learn.microsoft.com/es-mx/windows/wsl/install-manual)

## **Maquina Virtual**
- Hipervisores
	- [Virtual Box](https://www.virtualbox.org/wiki/Downloads)
	- [Vmware Workstation](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion) 

## USB Booteable
- Hacer una USB arrancable de Kali:
	- [Kali usb Live desde windows](https://www.kali.org/docs/usb/live-usb-install-with-windows/)
	- [Kali persistencia usb/](https://www.kali.org/docs/usb/usb-persistence/)

- Hacer una USB arrancable con Parrot:
	- [Parrato como crear usb livw](https://parrotsec.org/docs/usb/how-to-create-a-parrot-usb-drive/)
	- [Parrot persistencia usb ](https://parrotsec.org/docs/usb/persistent-usb)


## Docker
- Instalar docker
	- [Docker Windows] (https://docs.docker.com/desktop/setup/install/windows-install/)
	- [Docker Linux] (https://docs.docker.com/engine/install/)
	- [Docker Mac] (https://docs.docker.com/desktop/setup/install/mac-install/)

- Comandos básicos contenedor kali
```
docker pull kalilinux/kali-rolling
docker run -it kalilinux/kali-rolling /bin/bash

apt update && apt -y install kali-linux-headless
```
  - Comandos básicos contenedor parrot
  ```
docker pull parrotsec/security:latest
docker run -it parrotsec/security:latest /bin/bash
apt install -y parrot-tools
  ```
#### Referencias adicionales
- KaliLinux
	- [Imagenes de Docker oficiales Kali /](https://www.kali.org/docs/containers/official-kalilinux-docker-images/)
	- [Usar imagenes Docker Kali](https://www.kali.org/docs/containers/using-kali-docker-images/)
- Parrot
	- [Parrot en Docker](https://parrotsec.org/docs/cloud/parrot-on-docker/)
	- [Parrot uso general de docker](https://parrotsec.org/docs/cloud/general-usage-docker)


## VPS en la nube
- [Kali en AWS](https://www.kali.org/docs/cloud/aws/)
- [Kali en Azure](https://www.kali.org/docs/cloud/azure/)
- [Digital Ocean:](https://www.kali.org/docs/cloud/digitalocean/)
- [Kali en Linode: ](https://www.kali.org/docs/cloud/linode/)

## Instalar y Configurar Kali
- Instalar Virtual Box
	- [Virtual Box ](https://www.virtualbox.org/wiki/Downloads)
- Instalar Kali
	- [Kali Linux](https://www.kali.org/get-kali/#kali-virtual-machines)
- Contraseña y actualizar paquetes
```
passwd <Enter>

sudo apt udadate
sudo apt full-upgrade -y
```

# Actividad 3 - Viernes 29 de Agosto de 2025

## Resolver los rooms
- [How to use TryHackMe](https://tryhackme.com/room/howtousetryhackme)
- [Tutorial:](https://tryhackme.com/r/room/tutorial)  
- [OpenVPN](https://tryhackme.com/r/room/openvpn)
