
# Logged

## Solucion

One of the US Cyber Games administrators forgot their password to the FTP Server a lot of times. How many times did they forget it according to the IIS Windows log file?

_The flag format is SVUSCG{number}_ (Please don't brute-force)


## Solucion

```
grep -c 530 ex250604.log     
306737

SVUSCG{306737}

```
