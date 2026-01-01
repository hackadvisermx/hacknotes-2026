
# Silent Signal

SIV Pipeline Forensics Group 4

 [SilentSignal.pcap](https://ctf.uscybergames.com/files/0d72e6f28e13f1b39e89c7cbed0a8597/SilentSignal.pcap?token=eyJ1c2VyX2lkIjoyMjEsInRlYW1faWQiOm51bGwsImZpbGVfaWQiOjh9.aEeWOw.0utykTH-pVI5CM10pK_cL8spqzM "SilentSignal.pcap")

## Solucion

```
┌──(root㉿kali)-[/home/kali/tmp/uscyber]
└─# tshark -r SilentSignal.pcap -Y "icmp" -T fields -e frame.time_delta > deltas.txt

```


```python
with open("deltas.txt") as f:
    deltas = [float(line.strip()) for line in f if line.strip()]

#print(deltas)
# Suponiendo milisegundos y que cada delta representa un carácter
ascii_flag = ''.join(chr(int(d)) for d in deltas if 32 <= int(d) <= 126)
print(ascii_flag)

```


```
┌──(kali㉿kali)-[~/tmp/uscyber]
└─$ python exp.py
[0.0, 83.0, 86.0, 66.0, 82.0, 71.0, 123.0, 116.0, 105.0, 109.0, 51.0, 95.0, 116.0, 114.0, 52.0, 118.0, 51.0, 108.0, 95.0, 118.0, 49.0, 97.0, 95.0, 112.0, 49.0, 110.0, 103.0, 125.0]
SVBRG{tim3_tr4v3l_v1a_p1ng}

```