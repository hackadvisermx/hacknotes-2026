
# expletive


Written by Sylvia Lee

oh no! it seems like only some of the characters on my keyboard are working...

`nc challs.bcactf.com 38421`

## Solucion

## Analisis

Este reto **`expletive`** es un clásico de evasión de filtros. Aquí está el análisis del código `expletive.py`:

```python
blacklist = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"

def security_check(s):
    return any(c in blacklist for c in s) or s.count('_') > 50

BUFFER_SIZE = 36

while True:
    cmds = input("> ")

    if security_check(cmds):
        print("invalid input")
    else:
        if len(cmds) > BUFFER_SIZE:
            print(open("flag.txt", "r").read())
            break
        else:
            print("nope")
```

### Restricciones

- No puedes usar:    
    - Letras (`a-zA-Z`)        
    - Números (`0-9`)        
    - Más de 50 guiones bajos (`_`)
        
- Solo imprime la bandera si:    
    - `len(cmds) > 36`        
    - **Y** no contiene letras, números, ni más de 50 `_`

```
❯ nc challs.bcactf.com 38421
> !"#$%&'()*+,-./:;<=>?@[\]^`{|}~
nope
> !"#$%&'()*+,-./:;<=>?@[\]^`{|}~!"#$%&'()*+,-./:;<=>?@[\]^`{|}~
bcactf{fudG3_5hOo7_d4rn100}
```