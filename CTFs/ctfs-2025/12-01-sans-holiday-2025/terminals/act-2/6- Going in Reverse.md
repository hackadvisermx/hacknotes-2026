_Difficulty:_ 

Hello, I'm Kevin (though past friends have referred to me as 'Heavy K'). If you ever hear any one say that philosophy is a useless college degree, don't believe them; it's not. I've arrived where I am at because of it. It just made the path more interesting. I have more hobbies than I can keep up with, including Amateur Astronomy, Shortwave Radio, and retro-gaming. Things like backyard observances of distant galaxies, non-internet involved, around the world communications, and those who program for the Atari 2600 still invoke degrees of awe for me. One of the most influential books I've read is "Godel, Escher, and Bach" by Douglas Hofstadter. I'm also a bit of a Tolkien fanatic. My wife and my daughter are everything; without them, I surely would still be kicking rusty tin cans down the lonely highways of my past.

You know, there's something beautifully nostalgic about stumbling across old computing artifacts. Just last week, I was sorting through some boxes in my garage and came across a collection of 5.25" floppies from my college days - mostly containing terrible attempts at programming assignments and a few games I'd copied from friends.

Finding an old Commodore 64 disk with a mysterious BASIC program on it? That's like discovering a digital time capsule. The C64 was an incredible machine for its time - 64KB of RAM seemed like an ocean of possibility back then. I spent countless hours as a kid typing in program listings from Compute! magazine, usually making at least a dozen typos along the way.

The thing about BASIC programs from that era is they were often written by clever programmers who knew how to hide things in plain sight. Sometimes the most interesting discoveries come from reading the code itself rather than watching it execute. It's like being a digital archaeologist - you're not just looking at what the program does, you're understanding how the programmer thought.

Take your time with this one. The beauty of reverse engineering isn't in rushing to the answer, but in appreciating the craft of whoever wrote it. Those old-school programmers had to be creative within such tight constraints.


## Solucion

```
10 REM *** COMMODORE 64 SECURITY SYSTEM ***
20 ENC_PASS$ = "D13URKBT"
30 ENC_FLAG$ = "DSA|auhts*wkfi=dhjwubtthut+dhhkfis+hnkz" ' old "DSA|qnisf`bX_huXariz"
40 INPUT "ENTER PASSWORD: "; PASS$
50 IF LEN(PASS$) <> LEN(ENC_PASS$) THEN GOTO 90
60 FOR I = 1 TO LEN(PASS$)
70 IF CHR$(ASC(MID$(PASS$,I,1)) XOR 7) <> MID$(ENC_PASS$,I,1) THEN GOTO 90
80 NEXT I
85 FLAG$ = "" : FOR I = 1 TO LEN(ENC_FLAG$) : FLAG$ = FLAG$ + CHR$(ASC(MID$(ENC_FLAG$,I,1)) XOR 7) : NEXT I : PRINT FLAG$
90 PRINT "ACCESS DENIED"
100 END
```

This is a BASIC program (specifically written for the Commodore 64 style) that implements a simple "Security System."
The logic relies on a simple **XOR Cipher**. The code iterates through the strings and applies a bitwise **XOR** operation with the key **`7`** to encrypt/decrypt characters.
Here is the decoded information:

### 1. The Password (`PASS$`)

To verify the password (lines 50-70), the program compares the user input against `ENC_PASS$` ("D13URKBT") by XORing the input with 7. To find the correct password, we reverse this process on the encrypted string.

- **Encrypted:** `D13URKBT`
- **Decoded:** **`G60RUHES`**

### 2. The Flag (`FLAG$`)

Once the password is correct, line 85 executes. It decrypts the variable `ENC_FLAG$` using the same XOR 7 key.
- **Encrypted:** `DSA|auhts*wkfi=dhjwubtthut+dhhkfis+hnkz`
- **Decoded:** **`GTF{frost-plan:compressors,coolant,oil}`**

_(Note: The comment in line 30 contains an old flag: `GTF{vintage_or_fun}`)_

### Logic Breakdown

- **Line 70:** `CHR$(ASC(MID$(PASS$,I,1)) XOR 7)`
    - This takes a character from your input.
    - Converts it to its ASCII number (`ASC`).
    - Performs a bitwise Exclusive OR (`XOR`) with the number **7**.
    - If the result matches the character in `ENC_PASS$`, you pass.
        
- **Line 85:**
    - This loop performs the exact same operation on the long string `ENC_FLAG$` to reveal the hidden text.
        
### Python Decoder Script

If you want to verify this yourself, here is a Python script that mimics the BASIC logic:


```
def decode_c64(encoded_str, key=7):
    decoded = ""
    for char in encoded_str:
        # XOR the ASCII value of the character with the key
        decoded += chr(ord(char) ^ key)
    return decoded

enc_pass = "D13URKBT"
enc_flag = "DSA|auhts*wkfi=dhjwubtthut+dhhkfis+hnkz"

print(f"Password: {decode_c64(enc_pass)}")
print(f"Flag:     {decode_c64(enc_flag)}")
```