
# The Elf's Wager

Category: Reverse engineering

## Description

The break room buzzes with energy when you walk in. A crowd of elves has gathered around Jingle McSnark's desk, where a holographic scoreboard floats above a plate of half-eaten gingerbread.

"Ah, the human!" Jingle spins around, candy cane tucked behind one pointed ear. "Perfect timing. We were just discussing how long it would take you to fail today's challenge."

He gestures dramatically at his terminal, where green text scrolls across a black screen.

"Every week, I post a little puzzle for the SOC team. Keeps us sharp, you know? Last week, Snowdrift over there" he points at a sheepish-looking elf "took **three days** to crack my binary. _THREE. DAYS._"

Snowdrift mutters something about "unfair obfuscation" into his hot cocoa.

"But you," Jingle continues, leaning forward with a grin that's equal parts challenge and condescension, "you're supposed to be some kind of _specialist_, right? Santa's new secret weapon against the Krampus Syndicate?"

He slides a USB drive across the desk. It's shaped like a tiny Christmas tree.

"Prove it. My mainframe authentication module. Figure out what gets you in. No debuggers and I've made sure of that. **Static analysis only**, human."

The elves exchange glances. Someone starts a betting pool on a napkin.

"Oh, and one more thing," Jingle adds, spinning back to his monitors. "The Syndicate's been probing our mainframe access systems all week. If you _can't_ figure out how authentication works at the North Pole... well, let's hope they can't either."

The room falls silent, waiting.

# Solve

### saque 1

```
castr@lima-x86-emulation-vm:/tmp$ ./day4
NPLD Mainframe Authentication
Enter access code: hola_mundo
Jingle laughs. Wrong credential length!
```

### saque 2

```
strings -n 10 day4
/lib64/ld-linux-x86-64.so.2
__stack_chk_fail
__printf_chk
__libc_start_main
__cxa_finalize
GLIBC_2.3.4
GLIBC_2.2.5
GLIBC_2.34
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
Nice try, but Santa sees when you're peeking!
Coal for you! Tampering detected.
NPLD Mainframe Authentication
Enter access code:
Jingle laughs. Wrong credential length!
Welcome to the mainframe, Operative. Jingle owes the elves a round.
Access Denied. Jingle smirks.
/vs,$0v/q?
GCC: (Ubuntu 13.3.0-6ubuntu2~24.04) 13.3.0
.note.gnu.property
.note.gnu.build-id
.note.ABI-tag
.gnu.version
.gnu.version_r
.eh_frame_hdr
.init_array
.fini_array
```

### saque3

```
checksec --file=day4
RELRO           STACK CANARY      NX            PIE             RPATH      RUNPATH	Symbols		FORTIFY	Fortified	Fortifiable	FILE
Full RELRO      Canary found      NX enabled    PIE enabled     No RPATH   No RUNPATH   No Symbols	  Yes	1		2		day4
```


## Solution Gemini

Based on the static analysis of the provided binary dump, the flag is:

**`csd{1nt0_th3_m41nfr4m3}`**

### Analysis Walkthrough

1. Identification of the Main Function
The entry point entry calls __libc_start_main with a pointer to the main function at 001011711. This function (FUN_00101171) contains the primary logic for the authentication wager.

2. Anti-Debugging and Input Handling
The binary employs anti-debugging techniques, such as a ptrace call in the initialization phase (_INIT_1) to detect if a debugger is attached2. If detected, it exits early.

Inside the main function:

- It prints "NPLD Mainframe Authentication" and "Enter access code: "3.
- It accepts user input via `fgets`4.
- It calculates the string length and compares it to `0x17` (23 decimal). If the length is not exactly 23, it fails immediately5.
    

3. The Verification Logic

After passing the length check, the code calls the verification function FUN_001013626666.

This function loops through the input string and performs a simple XOR comparison:

- **Data Source:** It loads a byte array starting at `DAT_00102110`7.
- **The Operation:** It takes each character of the user input (`param_1`) and XORs it with the key `0x42`8.
- **The Comparison:** It compares the result of the XOR operation with the byte from `DAT_00102110`9.
    

To reverse this and find the flag, we simply need to take the bytes from `DAT_00102110` and XOR them with `0x42`.

### Decryption

Target Data (DAT_00102110):

Retrieved from the data section of the dump 10:

21, 31, 26, 39, 73, 2c, 36, 72, 1d, 36, 2a, 71, 1d, 2f, 76, 73, 2c, 24, 30, 76, 2f, 71, 3f

**Calculation:**

|**Hex Byte**|**XOR Key**|**Result (Hex)**|**Character**|
|---|---|---|---|
|`0x21`|`0x42`|`0x63`|**c**|
|`0x31`|`0x42`|`0x73`|**s**|
|`0x26`|`0x42`|`0x64`|**d**|
|`0x39`|`0x42`|`0x7b`|**{**|
|`0x73`|`0x42`|`0x31`|**1**|
|`0x2c`|`0x42`|`0x6e`|**n**|
|`0x36`|`0x42`|`0x74`|**t**|
|`0x72`|`0x42`|`0x30`|**0**|
|`0x1d`|`0x42`|`0x5f`|**_**|
|`0x36`|`0x42`|`0x74`|**t**|
|`0x2a`|`0x42`|`0x68`|**h**|
|`0x71`|`0x42`|`0x33`|**3**|
|`0x1d`|`0x42`|`0x5f`|**_**|
|`0x2f`|`0x42`|`0x6d`|**m**|
|`0x76`|`0x42`|`0x34`|**4**|
|`0x73`|`0x42`|`0x31`|**1**|
|`0x2c`|`0x42`|`0x6e`|**n**|
|`0x24`|`0x42`|`0x66`|**f**|
|`0x30`|`0x42`|`0x72`|**r**|
|`0x76`|`0x42`|`0x34`|**4**|
|`0x2f`|`0x42`|`0x6d`|**m**|
|`0x71`|`0x42`|`0x33`|**3**|
|`0x3f`|`0x42`|`0x7d`|**}**|

**Final Flag:** `csd{1nt0_th3_m41nfr4m3}`

Would you like me to explain any specific part of the assembly code, such as how the loop structure in `FUN_00101362` operates?


```python
# Encrypted bytes from DAT_00102110
encrypted_bytes = [
    0x21, 0x31, 0x26, 0x39, 0x73, 0x2c, 0x36, 0x72, 0x1d, 0x36, 0x2a, 0x71, 
    0x1d, 0x2f, 0x76, 0x73, 0x2c, 0x24, 0x30, 0x76, 0x2f, 0x71, 0x3f
]

# The XOR key found in FUN_00101362
key = 0x42

# Decrypt
flag = ''.join(chr(b ^ key) for b in encrypted_bytes)
print(f"Flag: {flag}")
```