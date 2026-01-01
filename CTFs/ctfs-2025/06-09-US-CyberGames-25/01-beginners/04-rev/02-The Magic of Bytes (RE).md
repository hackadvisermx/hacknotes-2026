
# The Magic of Bytes (RE)

I heard my friend wants to prepare for the new AP Cybersecurity CollegeBoard is adding soon, so I prepared a challenge with two python reverse engineering techniques. He insisted on it having an ELF binary though, so I also included it. Can you solve the challenge?

 [chall.py](https://ctf.uscybergames.com/files/b75ab3ca86cd787cb18f8acf7a0cb336/chall.py?token=eyJ1c2VyX2lkIjoyMjEsInRlYW1faWQiOm51bGwsImZpbGVfaWQiOjE2fQ.aFNSJw.RdfAUR1zfsKA5vTnIwefpXDVJVk "chall.py")

 [bytes.txt](https://ctf.uscybergames.com/files/b35426bf7bb7efbaab0d116abd1e4a6f/bytes.txt?token=eyJ1c2VyX2lkIjoyMjEsInRlYW1faWQiOm51bGwsImZpbGVfaWQiOjE3fQ.aFNSJw.v19021n-TPLyr_NYls1dBtt5paI "bytes.txt")

## Solucion

Es un archivo de texto donde al parecer hay un binario pero se hizo un shift a los bytes

- Nos dan un chall.py
```python
ELF_bytes = '' #"REDACTED"
key = '' #REDACTED
def not_so_fast(ELF_bytes,key):
    message = ""
    for i in range(len(ELF_bytes)):
        message += chr(ord(ELF_bytes[i]) + key)
    return message

with open("bytes.txt","a") as file:
    file.write("You want your ELF challenge so bad? Well here it is!\n")
    file.write(not_so_fast(ELF_bytes,key))
```

- Primero encontrar e


```python

def find_elf_offset(path="bytes.txt"):
    with open(path, "r") as f:
        data = f.read()

    data = data[:6] # tomamos 3 bytes

    for offset in range(1, 10):
        decoded = bytes([(ord(c) - offset) % 256 for c in data])
        if decoded.startswith(b"7F454C"):
            print(decoded)
            print(f"[+] ELF header found with offset: {offset}")
            return offset
    print("[-] No valid ELF header found.")
    return None


def not_so_fast(ELF_bytes,key):
    message = ""
    for i in range(len(ELF_bytes)):
        message += chr(ord(ELF_bytes[i]) - key)
    return message


with open("bytes.txt", "r") as f:
    data = f.read()

offset = find_elf_offset()


ds = not_so_fast(data,offset) 

#print(ds)

b = bytes.fromhex(ds)

with open("elf.out", "wb") as f:
    f.write(b)  
    





```

- ejecutamos el elf
```
root@fed658bd2bb1:/ctf# chmod +x elf.out
root@fed658bd2bb1:/ctf# ./elf.out
Alright, here's your ELF that you wanted so badly
Now use these bytes for the other python reverse engineering I mentioned
550D0D0A 00000000 41322968 48010000 E3000000 00000000 00000000 00000000 00030000 00400000 00738E00 00006400 64016C00 5A006402 64038400 5A016404 64058400 5A026406 64078400 5A036408 64098400 5A04640A 640B8400 5A05640C 640D8400 5A06640E 640F8400 5A076410 64118400 5A086412 64138400 5A09650A 65068300 65038300 17006502 83001700 65048300 17006501 83001700 65058300 17006508 83001700 65098300 17006507 83001700 83010100 64015300 2914E900 0000004E 63000000 00000000 00000000 00000000 00010000 00430000 00730400 00006401 53002902 4E5A0335 5F49A900 72020000 00720200 00007202 000000FA 0677696E 2E7079DA 02733103 00000073 02000000 00017204 00000063 00000000 00000000 00000000 00000000 01000000 43000000 73040000 00640153 0029024E 5A033331 31720200 00007202 00000072 02000000 72020000 00720300 0000DA02 73320600 00007302 00000000 01720500 00006300 00000000 00000000 00000000 00000001 00000043 00000073 04000000 64015300 29024E7A 027B5772 02000000 72020000 00720200 00007202 00000072 03000000 DA027333 09000000 73020000 00000172 06000000 63000000 00000000 00000000 00000000 00010000 00430000 00730400 00006401 53002902 4E5A045F 54683172 02000000 72020000 00720200 00007202 00000072 03000000 DA027334 0C000000 73020000 00000172 07000000 63000000 00000000 00000000 00000000 00010000 00430000 00730400 00006401 53002902 4E5A0435 5F416E72 02000000 72020000 00720200 00007202 00000072 03000000 DA027335 0F000000 73020000 00000172 08000000 63000000 00000000 00000000 00000000 00010000 00430000 00730400 00006401 53002902 4E5A0553 56424752 72020000 00720200 00007202 00000072 02000000 72030000 00DA0273 36120000 00730200 00000001 72090000 00630000 00000000 00000000 00000000 00000100 00004300 00007304 00000064 01530029 024E7A03 31317D72 02000000 72020000 00720200 00007202 00000072 03000000 DA027337 15000000 73020000 00000172 0A000000 63000000 00000000 00000000 00000000 00010000 00430000 00730400 00006401 53002902 4E5A055F 354C465F 72020000 00720200 00007202 00000072 02000000 72030000 00DA0273 38180000 00730200 00000001 720B0000 00630000 00000000 00000000 00000000 00000100 00004300 00007304 00000064 01530029 024E5A03 43484172 02000000 72020000 00720200 00007202 00000072 03000000 DA027339 1B000000 73020000 00000172 0C000000 290B5A0A 70795F63 6F6D7069 6C657204 00000072 05000000 72060000 00720700 00007208 00000072 09000000 720A0000 00720B00 0000720C 000000DA 05707269 6E747202 00000072 02000000 72020000 00720300 0000DA08 3C6D6F64 756C653E 01000000 73140000 00080208 03080308 03080308 03080308 03080308 03root@fed658bd2bb1:/ctf#
```

- convertilos a py binario
```python
with open("pbytes.txt", "r") as f:
    data = f.read()


# Limpiar el string
data_clean = data.replace("\n", "").replace(" ", "")

print(data_clean)

# Convertir a bytes binarios
binary_data = bytes.fromhex(data_clean)

# Guardar en archivo
with open("output.bin", "wb") as f:
    f.write(binary_data)
    

```

- uncompyle
```python
┌──(kali㉿kali)-[~/…/uscyber/beginner/rev/magicbytes]
└─$ uncompyle6 output.pyc 
# uncompyle6 version 3.9.2
# Python bytecode version base 3.8.0 (3413)
# Decompiled from: Python 2.7.18 (default, Aug  1 2022, 06:23:55) 
# [GCC 12.1.0]
# Embedded file name: win.py
# Compiled at: 2025-05-17 20:05:05
# Size of source mod 2**32: 328 bytes
import py_compile

def s1():
    return "5_I"


def s2():
    return "311"


def s3():
    return "{W"


def s4():
    return "_Th1"


def s5():
    return "5_An"


def s6():
    return "SVBGR"


def s7():
    return "11}"


def s8():
    return "_5LF_"


def s9():
    return "CHA"


print(s6() + s3() + s2() + s4() + s1() + s5() + s8() + s9() + s7())

# okay decompiling output.pyc
                                                                                                                                                                                                                               
┌──(kali㉿kali)-[~/…/uscyber/beginner/rev/magicbytes]

```

- ejecutamos 
```
uncompyle6 output.pyc | sudo tee flag.py

python flag.py  
SVBGR{W311_Th15_I5_An_5LF_CHA11}

```