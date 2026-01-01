
The SOC team discovered a suspiciously large log file after a recent breach. When they opened it, they found an enormous block of encoded text instead of typical logs. Could there be something hidden within? Your mission is to inspect the resulting file and reveal the real purpose of it. The team is relying on your skills to uncover any concealed information within this unusual log.Download the encoded data here: [Logs Data](https://challenge-files.picoctf.net/c_amiable_citadel/53216672a2c2381d0ed77a981fbf595657b3a8be3f0e0edff71b33c1baa6c9d6/logs.txt). Be prepared—the file is large, and examining it thoroughly is crucial .

Hints>
- Use `base64` to decode the data and generate the image file.

## Solucion

- los logs estan en base64, lo grabamos en un archivo
```
cat logs.txt | base64 -d > logs
 file logs
logs: PNG image data, 896 x 1152, 8-bit/color RGB, non-interlaced
 
```
- Cambiamos la extension y lo abrimos

```
 mv logs logs.png
```
- La imagen tiene una cadena en hexadecimal, usamos cyberchef para decodificarla (From Hex)

```
7069636F4354467B666F72656E736963735F616E616C797369735F69735F616D617A696E675F35636363376362307D
```

```
picoCTF{forensics_analysis_is_amazing_5ccc7cb0}
```