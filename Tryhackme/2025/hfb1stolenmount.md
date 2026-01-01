

#pacap #wireshark #barcode #zbar-tools
#  Stolen Mount

Analyse network traffic related to an unauthenticated file share access attempt, focusing on potential signs of data exfiltration.

## Task 1 Forensics  Stolen Mount

An intruder has infiltrated our network and targeted the NFS server where the backup files are stored. A classified secret was accessed and stolen. The only trace left behind is a packet capture (PCAP) file recorded during the incident. Your mission, should you accept it, is to discover the contents of the stolen data.

Note: Click the **Start Machine** button to spawn the Virtual Machine.

The packet capture (**challenge.pcapng**) is stored in the **~/Desktop** directory.

#### Encontramos una cadena md5 en el flujo TCP

```
90eb7723a657b6597100aafef171d9f2 (md5)

avengers
```

#### Extraemos un archivo .zip del trafico

- establecemos un filtro en whireshark
```
frame contains "PK"
```
- seguimos el stream TCP
- cambiamos al vista a raw
- y grabanmos a un archivo

```
┌──(kali㉿kali)-[~/tmp/tryhackme/hfb1stolenmount]
└─$ unzip secret.zip
Archive:  secret.zip
warning [secret.zip]:  36452 extra bytes at beginning or within zipfile
  (attempting to process anyway)
[secret.zip] secrets.png password: 
  inflating: secrets.png             
```

#### Leer codigo de barras

```
┌──(kali㉿kali)-[~/tmp/tryhackme/hfb1stolenmount]
└─$ zbarimg secrets.png
QR-Code:THM{n0t_s3cur3_f1l3_sh4r1ng}
scanned 1 barcode symbols from 1 images in 0.01 seconds

```




