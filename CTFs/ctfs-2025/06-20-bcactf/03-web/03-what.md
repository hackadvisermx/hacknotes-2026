

# What


Surmount the insurmountable.

[http://challs.bcactf.com:47861](http://challs.bcactf.com:47861/)


## Solve

Dos cadenas que colicionan en el mismo hash md5


https://www.johndcook.com/blog/2024/03/20/md5-hash-collision/


TEXTCOLLBYfGiJUETHQ4hAcKSMd5zYpgqf1YRDhkmxHkhPWptrkoyz28wnI9V0aHeAuaKnak
TEXTCOLLBYfGiJUETHQ4hEcKSMd5zYpgqf1YRDhkmxHkhPWptrkoyz28wnI9V0aHeAuaKnak


```
curl -X POST http://challs.bcactf.com:47861/\
  --data-urlencode "string1=TEXTCOLLBYfGiJUETHQ4hAcKSMd5zYpgqf1YRDhkmxHkhPWptrkoyz28wnI9V0aHeAuaKnak" \
  --data-urlencode "string2=TEXTCOLLBYfGiJUETHQ4hEcKSMd5zYpgqf1YRDhkmxHkhPWptrkoyz28wnI9V0aHeAuaKnak"

```

- Python
```python
import requests
import hashlib

url = 'http://challs.bcactf.com:47861/'  # Cambia esto si la URL es distinta

# Cadenas que colisionan
str1 = "TEXTCOLLBYfGiJUETHQ4hAcKSMd5zYpgqf1YRDhkmxHkhPWptrkoyz28wnI9V0aHeAuaKnak"
str2 = "TEXTCOLLBYfGiJUETHQ4hEcKSMd5zYpgqf1YRDhkmxHkhPWptrkoyz28wnI9V0aHeAuaKnak"

# Verificación opcional
print("[*] Verifying hash collision:")
print("MD5(str1):", hashlib.md5(str1.encode()).hexdigest())
print("MD5(str2):", hashlib.md5(str2.encode()).hexdigest())
print("Same hash?", hashlib.md5(str1.encode()).digest() == hashlib.md5(str2.encode()).digest())

# Enviar petición
data = {
    'string1': str1,
    'string2': str2
}

response = requests.post(url, data=data)

# Mostrar respuesta
print("\n[+] Server response:")
print(response.text.strip())

```