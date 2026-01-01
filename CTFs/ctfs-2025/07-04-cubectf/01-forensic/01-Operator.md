
# Operator

I think someone has been hiding secrets on my server. Can you find them?

Author: @B00TK1D

```
id

uid=0(root) gid=0(root) groups=0(root)

nc -lvp 2025 > /tmp/xcat
chmod +x /tmp/xcat
/tmp/xcat -l 2025 > /tmp/supersecret



GET / HTTP/1.1
Host: betplay.io
```



## Esto se probo pero el elf resultante no funcionaba
- extraer con binwalk

```
┌──(root㉿kali)-[/home/…/tmp/cubectf/forensic/operator]
└─# binwalk operator.pcap                          

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             Libpcap capture file, little-endian, version 2.4, Ethernet, snaplen: 262144
2135          0x857           ELF, 64-bit LSB shared object, AMD x86-64, version 1 (SYSV)

┌──(root㉿kali)-[/home/…/tmp/cubectf/forensic/operator]
└─# dd if=operator.pcap of=embedded_elf bs=1 skip=2135




```

## Examinamos las estadisticas 

- esto para ver que onda con la comunicación por los puertos 25
```
id

uid=0(root) gid=0(root) groups=0(root)

nc -lvp 2025 > /tmp/xcat
chmod +x /tmp/xcat
/tmp/xcat -l 2025 > /tmp/supersecret

```
- statistics →Conversations → TCP, y buscar puertos 25
- luego seguir los streams con la opcion del lado izquierd
- los streams son: 7 y 29
####  Vaciamos los streams a un archivo:

- el primero parece ser un ELF valido
```
tshark -r operator.pcap -Y "tcp.stream == 7" -T fields -e data | xxd -p -r > xcat

file xcat 
xcat: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=39c1cfbc24813f83ac8727de31c7c04e59fbab92, for GNU/Linux 3.2.0, not stripped
      
```
- el segundo no parece tener sentido
```
┌──(root㉿kali)-[/home/…/tmp/cubectf/forensic/operator]
└─# tshark -r operator.pcap -Y "tcp.stream == 29" -T fields -e data | xxd -p -r > other  

Running as user "root" and group "root". This could be dangerous.
tshark: The file "operator.pcap" appears to have been cut short in the middle of a packet.
                                                                                                                                                                                                                                            
┌──(root㉿kali)-[/home/…/tmp/cubectf/forensic/operator]
└─# file other
other: data
                                                                                                                                                                                                                                            
┌──(root㉿kali)-[/home/…/tmp/cubectf/forensic/operator]
└─# cat other            
Ln;V+▒��qP�greb�e�')M'd0
                        �c�hFm��Por'I�y�8PMs���aunV1
                                                    �x�lJT{�pbdV1�B�oBLj�$erV1�n�lKGgʅ�$ixb
                                                                                           �{�kFFEin#�+�}QG9���}'c2I�n�jFV>���kuz6�e�gru9
�;�GR-���4ud)7▒�T�mOV/���0`$)2]�g�,GQAՖ�0>$Ez�M'2
(                                                     
```

### Le aplicamos ghidra al primero

- vamos a la funcion
```

void xor_encrypt(long param_1,long param_2)

{
  long lVar1;
  
  if (param_2 != 0) {
    lVar1 = 0;
    do {
      *(byte *)(param_1 + lVar1) = *(byte *)(param_1 + lVar1) ^ (&key)[(uint)lVar1 & 0xf];
      lVar1 = lVar1 + 1;
    } while (param_2 != lVar1);
  }
  return;
}


```

- localizamos la Key de encripción XOR
- derecho , Copy especial Data, o Byte Strings

```
04h
07h
17h
76h    v
42h    B
69h    i
B0h
0Bh
DEh
18h
23h    #
22h    "
1Eh
EDh
F7h
AEh

04 07 17 76 42 69 b0 0b de 18 23 22 1e ed f7 ae
```

- sacamos el otro stream
```
tshark -r operator.pcap -Y "tcp.stream == 29" -T fields -e data                     
Running as user "root" and group "root". This could be dangerous.



4c6e3b562b1a907fb67150027fcd84cb677265136205d965bb2729

4d276403300c9063b16846026d82fd

506f72052749d179bb38504d7388d7d861756e56310cde78b76c4a547bcd99c17062645631069042fe6f424c6acd83c124657256311cc26efe6c4b4767ca85cb24697802620cc87bb16b464614

45696e0123109c2bb67d5147399ed7c37d2763193249c36ebd6a46563e8499c86b757a173600df65e412

67727513390a803bb24713522d9fc3da34756429371a8354b36d4f562fb284da30602429325dc967ee2c475141d596cc303e24457a14ba

4d277f19320c9065b17a4c4667cd91c76a6364563601d17ff0360d28



```

```python
from itertools import cycle

# Clave proporcionada (hexadecimal)
key_hex = "04 07 17 76 42 69 b0 0b de 18 23 22 1e ed f7 ae"
key = bytes.fromhex(key_hex)

# Cadenas cifradas (en hexadecimal)
ciphertexts_hex = [
    "4c6e3b562b1a907fb67150027fcd84cb677265136205d965bb2729",
    "4d276403300c9063b16846026d82fd",
    "506f72052749d179bb38504d7388d7d861756e56310cde78b76c4a547bcd99c17062645631069042fe6f424c6acd83c124657256311cc26efe6c4b4767ca85cb24697802620cc87bb16b464614",
    "45696e0123109c2bb67d5147399ed7c37d2763193249c36ebd6a46563e8499c86b757a173600df65e412",
    "67727513390a803bb24713522d9fc3da34756429371a8354b36d4f562fb284da30602429325dc967ee2c475141d596cc303e24457a14ba",
    "4d277f19320c9065b17a4c4667cd91c76a6364563601d17ff0360d28"
]

# Descifrado e impresión
for i, ct_hex in enumerate(ciphertexts_hex, 1):
    ct_bytes = bytes.fromhex(ct_hex)
    decrypted = bytes(c ^ k for c, k in zip(ct_bytes, cycle(key)))
    print(f"[{i}] {decrypted.decode('utf-8', errors='replace')}")

```

```bash
 python dec.py
[1] Hi, is this a secure line?

[2] I sure hope so

[3] These are some very sensitive notes so I want to be sure they're not exposed

[4] Anyway, here's my top secret information:

[5] cube{c00l_0p3r4t0rs_us3_mult1_st4g3_p4yl04ds_8ab49338}

[6] I hope nobody finds that...
```