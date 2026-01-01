
# hfb1cipherssecretmessage

#crypto #rot13



One of the Ciphers' secret messages was recovered from an old system alongside the encryption algorithm, but we are unable to decode it.

**Order:** Can you help void to decode the message?

**Message** : a_up4qr_kaiaf0_bujktaz_qm_su4ux_cpbq_ETZ_rhrudm

**Encryption algorithm** :

```python
from secret import FLAG

def enc(plaintext):
    return "".join(
        chr((ord(c) - (base := ord('A') if c.isupper() else ord('a')) + i) % 26 + base) 
        if c.isalpha() else c
        for i, c in enumerate(plaintext)
    )

with open("message.txt", "w") as f:
    f.write(enc(FLAG))
```

Note: Wrap the decoded message within the flag format **THM{}**

## Solve
```python
flag = 'a_up4qr_kaiaf0_bujktaz_qm_su4ux_cpbq_ETZ_rhrudm'

def denc(plaintext):
    return "".join(
        chr((ord(c) - (base := ord('A') if c.isupper() else ord('a')) - i) % 26 + base) 
        if c.isalpha() else c
        for i, c in enumerate(plaintext)
    )


print(denc(flag))
```

```bash
python exp.py
a_sm4ll_crypt0_message_to_st4rt_with_THM_cracks

THM{a_sm4ll_crypt0_message_to_st4rt_with_THM_cracks}
```

