
# flag flag

Written by Thomas Raskin

It's a flag—inside a flag.

https://play.bcactf.com/files/0deefaf4236d79aaf25ebf8fc2bb2e32/flag-flag.png?token=eyJ1c2VyX2lkIjozMDYsInRlYW1faWQiOjE5NSwiZmlsZV9pZCI6NDd9.aFjCww.hFMmNX3fLGNo5EEgyBMSdVgjE2s

## Solucion

- Aquí hay una **cadena repetitiva** donde eventualmente aparece
- Esto revela una concatenación entre `"bcabcab..."` y `"ctf{...}"`, donde la bandera está construida en pedazos.
- Y recuerda la pista visual: `+7D` → `}`

```

zsteg -a flag-flag.png | grep bca   
b8,rgb,lsb,xy       .. text: "bcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcab"
b8,rgb,lsb,xy,prime .. text: "bcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcabcactfctfctfctfctfctfctfctfctfctfctfctfctfctfctfctfctfctfctfctfctf{1j{1j{1j{1j{1j{1j{1j{1j{1j{1j{1j{1j{1j{1j{1j{1jN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uYkjYkjYkjYkjYkjYkjYkjY"
b8,rgb,lsb,XY,prime .. text: "YkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjYkjN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7uN7u{1j{1j{1j{1j{1j{1j{1j{1j{1j{1j{1j{1j{1j{1j{1j{1jctfctfctfctfctfctfctfctfctfctfctfctfctfctfctfctfbcabcabcabcabcabcabcab"

bcactf{1jN7uYkj}
```

Podemos deducir que:

- `"bcabcabcabc...actf"` → contiene **"bcactf"** en alguna posición.    
- Luego se concatena: `bcactf{1jN7uYkj}` (combinando partes repetidas que simulan texto cifrado o relleno).
