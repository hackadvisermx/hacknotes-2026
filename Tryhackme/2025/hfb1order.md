
# hfb1order

#xor 

Perform a known-plaintext attack to recover a repeating-key XOR key and decrypt a hidden message.

## Solve

To solve this CTF crypto challenge, we’ll reverse the repeating-key XOR cipher, exploiting the fact that every message starts with the known plaintext header:

`ORDER:`


```python
def xor_decrypt(ciphertext_hex, known_plaintext_start_hex):
    """
    Decrypts a repeating-key XOR cipher message.

    Args:
        ciphertext_hex (str): The intercepted ciphertext in hexadecimal.
        known_plaintext_start_hex (str): The known starting plaintext in hexadecimal.

    Returns:
        str: The decrypted message in ASCII.
    """
    ciphertext_bytes = bytes.fromhex(ciphertext_hex)
    known_plaintext_start_bytes = bytes.fromhex(known_plaintext_start_hex)

    # Determine the key
    key_bytes = b''
    for i in range(len(known_plaintext_start_bytes)):
        key_bytes += bytes([ciphertext_bytes[i] ^ known_plaintext_start_bytes[i]])

    # Decrypt the full message
    decrypted_bytes = b''
    for i in range(len(ciphertext_bytes)):
        decrypted_bytes += bytes([ciphertext_bytes[i] ^ key_bytes[i % len(key_bytes)]])

    return decrypted_bytes.decode('ascii', errors='ignore')

# The intercepted messages
message1 = "1c1c01041963730f31352a3a386e24356b3d32392b6f6b0d323c22243f6373"
message2 = "1a0d0c302d3b2b1a292a3a38282c2f222d2a112d282c31202d2d2e24352e60"

# Combine messages for full decryption as per previous challenge
full_message_hex = message1 + message2

# Known header in hexadecimal
known_header_hex = "4f524445523a"  # "ORDER:" in hex

# Decrypt the full message
decrypted_full_message = xor_decrypt(full_message_hex, known_header_hex)

print(f"Decrypted Message:\n{decrypted_full_message}")
```




### Attack Plan (Known Plaintext Attack)

We took the following steps:

1. **Convert the hex string to raw bytes**
2. **XOR** the first few bytes of ciphertext with the known plaintext (`"ORDER:"`)
3. This gives us the **repeating key**
4. Then, we **cycle the key** over the entire ciphertext to recover the full plaintext message

```python
from itertools import cycle

ciphertext_hex = (
    "1c1c01041963730f31352a3a386e24356b3d32392b6f6b0d323c22243f6373"
    "1a0d0c302d3b2b1a292a3a38282c2f222d2a112d282c31202d2d2e24352e60"
)

ciphertext = bytes.fromhex(ciphertext_hex)

# Known header at start of every message
known_plaintext = b"ORDER:"

# Recover key using known plaintext XOR trick
key = bytes(c ^ p for c, p in zip(ciphertext, known_plaintext))

# Decrypt full message using repeating XOR
decrypted_message = bytes(c ^ k for c, k in zip(ciphertext, cycle(key)))


print(decrypted_message.decode())
```