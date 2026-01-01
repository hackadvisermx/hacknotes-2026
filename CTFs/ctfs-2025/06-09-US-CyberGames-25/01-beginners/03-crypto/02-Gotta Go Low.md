
# Gotta Go Low

 [output.txt](https://ctf.uscybergames.com/files/c93a0e3efa80dc544570fd5f58fb0a00/output.txt?token=eyJ1c2VyX2lkIjoyMjEsInRlYW1faWQiOm51bGwsImZpbGVfaWQiOjE0fQ.aFC8jQ.VDmksO5BsXuUdGeHT-Xylpx0IhI "output.txt")

 [challenge.py](https://ctf.uscybergames.com/files/b9670324632373fcfd6f86abf6e8f6ac/challenge.py?token=eyJ1c2VyX2lkIjoyMjEsInRlYW1faWQiOm51bGwsImZpbGVfaWQiOjE1fQ.aFC8jQ.gKWobzTQX2Kl4d9ZRN5VYViRk9I "challenge.py")

## Solucion

- Los valores que dan (output.txt)

```bash
e = 3
n = 131568056653373132012174976653266884910157447726840322128654668864744046838266089026781586223439349724120314053694539817871939811571791816723493939318461523177171366268168393668921342560692769288416456729904590430725433093936110904690901655852707387030375716854722258158043345187159940346383427399753323791427
ciphertext = 898564915277349210856325643177982880844269990070750993964886895279898673815668084088711509416748167698104435154155125903563814943672577759197896689419072923530272379905743352154731864706846939063378835946564725599528080721144587149407333
```

- el código que nos dan, es el que genera esos numeros

``` python
import random
from math import gcd
import sympy

def genKeypair(p, q):
    n = p * q
    phi = (p - 1) * (q - 1)

    print(n)
    e = 3

    def modinv(a, m):
        m0, x0, x1 = m, 0, 1
        while a > 1:
            q = a // m
            m, a = a % m, m
            x0, x1 = x1 - q * x0, x0
        return x1 + m0 if x1 < 0 else x1

    d = modinv(e, phi)
    return ((e, n), (d, n))

def encrypt(pubKey, plaintext):
    e, n = pubKey

    plaintextInt = int.from_bytes(plaintext.encode(), byteorder='big')

    encrypted = pow(plaintextInt, e, n)
    return encrypted

def genPrime(bits):
    while True:
        possible = random.getrandbits(bits)
        possible |= (1 << bits - 1) | 1

        if sympy.isprime(possible):
            return possible

if __name__ == "__main__":
    while True:
        p = genPrime(512)
        q = genPrime(512)

        if gcd(3, (p - 1) * (q - 1)) == 1:
            break

    pubKey, privKey = genKeypair(p, q)

    message = "SVBGR{test_flag}"
    encrypted = encrypt(pubKey, message)

    print("Encrypted message:", encrypted)
```


```python
e = 3

n = 131568056653373132012174976653266884910157447726840322128654668864744046838266089026781586223439349724120314053694539817871939811571791816723493939318461523177171366268168393668921342560692769288416456729904590430725433093936110904690901655852707387030375716854722258158043345187159940346383427399753323791427

ciphertext = 898564915277349210856325643177982880844269990070750993964886895279898673815668084088711509416748167698104435154155125903563814943672577759197896689419072923530272379905743352154731864706846939063378835946564725599528080721144587149407333

  

# Cálculo de raíz cúbica entera

def integer_nth_root(x, n):

"""Devuelve la raíz n-ésima entera de x"""

high = 1

while high**n <= x:

high *= 2

low = high // 2

while low < high:

mid = (low + high) // 2

if mid**n < x:

low = mid + 1

else:

high = mid

return low if low**n == x else None

  

m = integer_nth_root(ciphertext, e)

if m:

print("Flag:", bytes.fromhex(hex(m)[2:]) )

else:

print("No se pudo obtener la raíz cúbica exacta.")
```

```
python3 solve2.py
Flag: b'SVBGR{l0w_3xp0n3nt5_@r3_n0t_s@fe}'
```