# Mind your Ps and Qs

In RSA, a small `e` value can be problematic, but what about `N`? Can you decrypt this? [values](https://mercury.picoctf.net/static/3cfeb09681369c26e3f19d886bc1e5d9/values)


## solucion
- verificar la instalacion de librerias para RSA

```bash
python3 -m pip install gmpy2
python3 -m pip install pycryptodome
```

- en nuevas versiones de cali
```bash

sudo apt install python3-gmpy2
pipx install pycryptodome

```



- formulas

n = p * q
c = m ^ e (mod n)

tn = (p-1)(q-1)
d = inv_mod[e,tn]
m = c ^ d (mod n)

- Tenemos

```bash 
┌──(kali㉿kali)-[~/picoctf/crypto/mind]
└─$ cat values 
Decrypt my super sick RSA:
c: 8533139361076999596208540806559574687666062896040360148742851107661304651861689
n: 769457290801263793712740792519696786147248001937382943813345728685422050738403253
e: 65537  
```

### way 0
- facttorizamos n 
http://factordb.com 


```python
>>> 
>>> p = 1617549722683965197900599011412144490161
>>> q = 475693130177488446807040098678772442581573
>>> n = 769457290801263793712740792519696786147248001937382943813345728685422050738403253
>>> p * q == n
True
>>> c = 8533139361076999596208540806559574687666062896040360148742851107661304651861689
>>> e = 65537
>>> 
>>> tn = (p-1)*(q-1)
>>> d = pow(e,-1, tn)
>>> m = pow(c, d, n)
>>> bytes.fromhex(hex(m)[2:])
b'picoCTF{sma11_N_n0_g0od_05012767}'
```

## El script perron

```python
'''
Dado que n es muy corta, se puede factorizar y obtener los valores de p y q
Para factorizar usamos > https://factordb.com/

'''

c = 62324783949134119159408816513334912534343517300880137691662780895409992760262021
n = 1280678415822214057864524798453297819181910621573945477544758171055968245116423923
e = 65537  

# se obtienen de la factorizacion
p = 1899107986527483535344517113948531328331
q = 674357869540600933870145899564746495319033

tn = (p-1) * (q-1)

d = pow(e, -1, tn)

m = pow(c,d,n)

flag = bytes.fromhex(hex(m)[2:]).decode()

print(flag)
```


## 2
 
```bash
RsaCtfTool \
    -n 1280678415822214057864524798453297819181910621573945477544758171055968245116423923 \
    -e 65537 \
    --decrypt 62324783949134119159408816513334912534343517300880137691662780895409992760262021 \
    --attack all     
private argument is not set, the private key will not be displayed, even if recovered.
['/tmp/tmpte0caurd']

[*] Testing key /tmp/tmpte0caurd.
attack initialized...
attack initialized...
[*] Performing rapid7primes attack on /tmp/tmpte0caurd.
[+] Time elapsed: 0.0008 sec.
[*] Performing nonRSA attack on /tmp/tmpte0caurd.
[+] Time elapsed: 0.0005 sec.
[*] Performing fibonacci_gcd attack on /tmp/tmpte0caurd.
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 9999/9999 [00:00<00:00, 285570.24it/s]
[+] Time elapsed: 0.0386 sec.
[*] Performing factordb attack on /tmp/tmpte0caurd.
[*] Attack success with factordb method !
[+] Total time elapsed min,max,avg: 0.0005/0.0386/0.0133 sec.

Results for /tmp/tmpte0caurd:

Decrypted data :
HEX : 0x007069636f4354467b736d6131315f4e5f6e305f67306f645f30353031323736377d
INT (big endian) : 13016382529449106065927291425342535437996222135352905256639555654677400177227645
INT (little endian) : 3711739942918996135095564070444078210974633154646265969428826141271237837554544640
utf-8 : picoCTF{sma11_N_n0_g0od_05012767}
utf-16 : 瀀捩䍯䙔獻慭ㄱ也湟弰で摯た〵㈱㘷紷
STR : b'\x00picoCTF{sma11_N_n0_g0od_05012767}'


```


## 3

```
RsaCtfTool \
    -n 1280678415822214057864524798453297819181910621573945477544758171055968245116423923 \
    -e 65537 \
    --decrypt 62324783949134119159408816513334912534343517300880137691662780895409992760262021 \
    --attack factordb
private argument is not set, the private key will not be displayed, even if recovered.
['/tmp/tmppu903ypz']

[*] Testing key /tmp/tmppu903ypz.
[*] Performing factordb attack on /tmp/tmppu903ypz.
[*] Attack success with factordb method !

Results for /tmp/tmppu903ypz:

Decrypted data :
HEX : 0x007069636f4354467b736d6131315f4e5f6e305f67306f645f30353031323736377d
INT (big endian) : 13016382529449106065927291425342535437996222135352905256639555654677400177227645
INT (little endian) : 3711739942918996135095564070444078210974633154646265969428826141271237837554544640
utf-8 : picoCTF{sma11_N_n0_g0od_05012767}
utf-16 : 瀀捩䍯䙔獻慭ㄱ也湟弰で摯た〵㈱㘷紷
STR : b'\x00picoCTF{sma11_N_n0_g0od_05012767}'

```


## Ligas
- factordb : http://factordb.com 
- RsaCtfTool: https://github.com/RsaCtfTool/RsaCtfTool