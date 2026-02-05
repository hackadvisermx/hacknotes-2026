
# W1seGuy

https://tryhackme.com/room/w1seguy

A w1se guy 0nce said, the answer is usually as plain as day.






```python
from pwn import *

conn = remote('10.82.140.31', 1337)
response = conn.recvline().decode()
print(response)

hex_encoded = response.split("flag 1: ")[1].strip()
xored_bytes = bytes.fromhex(hex_encoded)

print(f"Encoded bytes length: {len(xored_bytes)}")

# We know the flag format is THM{...}
# The flag is 40 characters, so we know positions 0-3 are "THM{" and position 39 is "}"

# Recover key using known positions
# Position 0: 'T', Position 1: 'H', Position 2: 'M', Position 3: '{'
# Position 39 % 5 = 4, so we can get key[4] from position 39

key = ['?'] * 5

# Get key[0] from position 0
key[0] = chr(ord('T') ^ xored_bytes[0])
# Get key[1] from position 1
key[1] = chr(ord('H') ^ xored_bytes[1])
# Get key[2] from position 2
key[2] = chr(ord('M') ^ xored_bytes[2])
# Get key[3] from position 3
key[3] = chr(ord('{') ^ xored_bytes[3])
# Get key[4] from position 39 (39 % 5 = 4)
key[4] = chr(ord('}') ^ xored_bytes[39])


# Usamos `repr()` para ver **exactamente** qué caracteres tiene la key, incluyendo caracteres no imprimibles o especiales.

key_str = ''.join(key)
print(f"Recovered key: {repr(key_str)}")

# Verify with other known positions
# Position 4 should give us key[4] again if we use another known char
# But we don't know position 4... let's just verify our key works

conn.recvuntil(b"What is the encryption key? ")
conn.sendline(key_str.encode())
response = conn.recvall().decode()
print(response)
```

```
[*] Closed connection to 10.82.140.31 port 1337
➜  w1seguy python rev.py
[+] Opening connection to 10.82.140.31 on port 1337: Done
This XOR encoded text has flag 1: 6c25292935090c083c317d151013314c59073926790316612454211d3a104a191d62304a152b2038

Encoded bytes length: 40
Recovered key: '8mdRE'
[+] Receiving all data: Done (89B)
[*] Closed connection to 10.82.140.31 port 1337
Congrats! That is the correct key! Here is flag 2: THM{BrUt3_ForC1nG_XOR_cAn_B3_FuN_nO?}

```

We got the flag: `THM{BrUt3_ForC1nG_XOR_cAn_B3_FuN_nO?}`

## Solution Explanation

The key insight was realizing that:

1. **The actual flag is 40 characters long**, not 20 like the fake flag shown in the code
2. We know the flag format: starts with `THM{` and ends with `}`
3. Since the key is 5 characters and repeats, we could use these known positions:
    - Position 0: `T` → gives us `key[0]`
    - Position 1: `H` → gives us `key[1]`
    - Position 2: `M` → gives us `key[2]`
    - Position 3: `{` → gives us `key[3]`
    - Position 39: `}` → gives us `key[4]` (since 39 % 5 = 4)

This is a **known-plaintext attack** on XOR encryption. The vulnerability is that we knew parts of the plaintext (the flag format), which allowed us to recover the entire key even though we didn't know the full message!

The challenge name "Brute Forcing XOR can be fun" is a bit misleading - we didn't actually need to brute force anything. We used cryptanalysis to directly recover the key



```python
from pwn import *

# From our successful run
hex_encoded = "6c25292935090c083c317d151013314c59073926790316612454211d3a104a191d62304a152b2038"
key = "8mdRE"

xored_bytes = bytes.fromhex(hex_encoded)

# Decode by XORing with the key
flag1 = ""
for i in range(len(xored_bytes)):
    flag1 += chr(xored_bytes[i] ^ ord(key[i % len(key)]))

print(f"Flag 1: {flag1}")
print(f"Flag 2: THM{{BrUt3_ForC1nG_XOR_cAn_B3_FuN_nO?}}")
```


```
➜  w1seguy python rev0.py
Flag 1: THM{p1alntExtAtt4ckcAnr3alLyhUrty0urxOr}
Flag 2: THM{BrUt3_ForC1nG_XOR_cAn_B3_FuN_nO?}
```