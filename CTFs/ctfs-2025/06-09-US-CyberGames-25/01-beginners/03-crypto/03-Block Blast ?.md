
# Block Blast

Encryption can be powerful, but it often can be misused. Are you clever enough to unlock a secret and score the ultimate combo?

`nc crypto.ctf.uscybergames.com 5001`

 [challenge.py](https://ctf.uscybergames.com/files/ac2f5ccea0fd37311719c0867aa0327f/challenge.py?token=eyJ1c2VyX2lkIjoyMjEsInRlYW1faWQiOm51bGwsImZpbGVfaWQiOjIwfQ.aFDLmA.i9ZI3Iju-ND07dv6UeAgKo8yKkI "challenge.py")

## Solucion

``` python
#!/usr/bin/env python3
import os
import sys
import socket
import binascii
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad

BLOCK_SIZE = 16
FLAG_PATH = "./flag.txt"

try:
    with open(FLAG_PATH, "rb") as f:
        FLAG = f.read().strip()
except FileNotFoundError:
    print(f"[!] {FLAG_PATH} missing — create the file with your real flag.")
    sys.exit(1)

KEY = os.urandom(16)

def encrypt_oracle(user_bytes: bytes) -> bytes:
    plaintext = user_bytes + FLAG
    padded = pad(plaintext, BLOCK_SIZE)
    cipher = AES.new(KEY, AES.MODE_ECB)
    return cipher.encrypt(padded)


print("=== AES-ECB Byte-at-a-Time Oracle ===")
print("Send hex-encoded bytes. Empty line or 'exit' quits.")

while True:
    data = input("> ")

    line = data.strip()
    if not line or line.lower() == 'exit':
        print("Bye!")
        break

    try:
        user_bytes = binascii.unhexlify(line)
    except (binascii.Error, ValueError):
        print("[!] That doesn't seem like a proper spell.")
        continue

    ct = encrypt_oracle(user_bytes)
    print(binascii.hexlify(ct).decode())

```

## Analisis
Este reto es un clásico **"byte-at-a-time ECB decryption"**, basado en un **oracle de cifrado AES en modo ECB**.

### 🔍 Análisis del código (`challenge.py`)

- Usa `AES.new(KEY, AES.MODE_ECB)` con una clave **aleatoria y secreta** (`os.urandom(16)`).    
- El texto plano cifrado es: `user_input + FLAG`, **rellenado** (padding PKCS#7).   
- Se nos permite enviar **cadenas codificadas en hexadecimal**, y nos devuelve el resultado del cifrado de esa entrada concatenada con la flag.
    
### 💡 Qué significa esto
Este es un típico **oracle de cifrado en modo ECB**, lo que significa que si repetimos bloques de texto plano, obtendremos bloques cifrados repetidos. Como el texto cifrado incluye `user_input + FLAG`, podemos usar un ataque "byte a byte" para revelar el contenido de la FLAG sin conocer la clave.

### Script de la solución

```python
from pwn import *
import binascii

context.log_level = 'error'  # silenciar logs, cambia a 'debug' si quieres más detalles

HOST = 'crypto.ctf.uscybergames.com'
PORT = 5001
BLOCK_SIZE = 16

def start_connection():
    return remote(HOST, PORT)

def encrypt_block(r, hex_input):
    """Envía input codificado en hex y recibe el resultado cifrado en binario."""
    r.recvuntil(b'> ')
    r.sendline(hex_input.encode())
    response = r.recvline().strip()
    try:
        return binascii.unhexlify(response)
    except:
        return None

def detect_block_size(r):
    initial_len = len(encrypt_block(r, "41"))  # 'A'
    i = 2
    while True:
        test_input = "41" * i
        new_len = len(encrypt_block(r, test_input))
        if new_len > initial_len:
            return new_len - initial_len
        i += 1

def is_ecb_mode(r, block_size):
    data = "41" * (block_size * 3)
    ct = encrypt_block(r, data)
    blocks = [ct[i:i+block_size] for i in range(0, len(ct), block_size)]
    return len(blocks) != len(set(blocks))

def byte_at_a_time_ecb(r, block_size):
    known_bytes = b""
    print("[*] Starting byte-at-a-time ECB attack...")

    while True:
        block_index = len(known_bytes) // block_size
        pad_len = block_size - (len(known_bytes) % block_size) - 1
        pad = b"A" * pad_len
        ct = encrypt_block(r, binascii.hexlify(pad).decode())

        if ct is None:
            break

        target_block = ct[block_index*block_size:(block_index+1)*block_size]

        found = False
        for i in range(256):
            guess = pad + known_bytes + bytes([i])
            guess_hex = binascii.hexlify(guess).decode()
            test_ct = encrypt_block(r, guess_hex)
            if test_ct and test_ct[block_index*block_size:(block_index+1)*block_size] == target_block:
                known_bytes += bytes([i])
                print(f"[+] Byte found: {bytes([i])!r} | So far: {known_bytes!r}")
                found = True
                break

        if not found:
            print("[!] No matching byte found. Likely end of secret.")
            break

    return known_bytes

if __name__ == "__main__":
    r = start_connection()
    r.recvuntil(b'=== AES-ECB Byte-at-a-Time Oracle ===')
    r.recvline()  # banner line 2

    block_size = detect_block_size(r)
    print(f"[*] Detected block size: {block_size}")

    if not is_ecb_mode(r, block_size):
        print("[!] Not ECB mode — attack won't work.")
        r.close()
        exit(1)

    flag = byte_at_a_time_ecb(r, block_size)
    print(f"\n🏁 FLAG found: {flag.decode(errors='replace')}")
    r.close()


```