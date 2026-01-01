[https://drive.google.com/file/d/1VzbyG0MDP21HUGj07dBkFW3Sncqz3xG1/view?usp=sharing](https://drive.google.com/file/d/1VzbyG0MDP21HUGj07dBkFW3Sncqz3xG1/view?usp=sharing)

Mandatory RSA challenge

**Flag format: deadsec{}**

## Solve
```python

#!/usr/bin/env python3

from Crypto.Util.number import getPrime, bytes_to_long
from secret import flag

p, q = getPrime(512), getPrime(512)
n = p * q
e = 65537
phi = (p-1) * (q-1)
hint = phi & ((1 << 500)-1)

m = bytes_to_long(flag)
c = pow(m, e, n)

print(f'{n=}')
print(f'{c=}')
print(f'{hint=}')
#n=144984891276196734965453594256209014778963203195049670355310962211566848427398797530783430323749867255090629853380209396636638745366963860490911853783867871911069083374020499249275237733775351499948258100804272648855792462742236340233585752087494417128391287812954224836118997290379527266500377253541233541409
#c=120266872496180344790010286239079096230140095285248849852750641721628852518691698502144313546787272303406150072162647947041382841125823152331376276591975923978272581846998438986804573581487790011219372437422499974314459242841101560412534631063203123729213333507900106440128936135803619578547409588712629485231
#hint=867001369103284883200353678854849752814597815663813166812753132472401652940053476516493313874282097709359168310718974981469532463276979975446490353988
 .
```

### Solucion

```python
import gmpy2
from Crypto.Util.number import long_to_bytes

n = 144984891276196734965453594256209014778963203195049670355310962211566848427398797530783430323749867255090629853380209396636638745366963860490911853783867871911069083374020499249275237733775351499948258100804272648855792462742236340233585752087494417128391287812954224836118997290379527266500377253541233541409
c = 120266872496180344790010286239079096230140095285248849852750641721628852518691698502144313546787272303406150072162647947041382841125823152331376276591975923978272581846998438986804573581487790011219372437422499974314459242841101560412534631063203123729213333507900106440128936135803619578547409588712629485231
hint = 867001369103284883200353678854849752814597815663813166812753132472401652940053476516493313874282097709359168310718974981469532463276979975446490353988
e = 65537

# The hint is the lower 500 bits of phi.
# This means phi = k * 2^500 + hint for some integer k.
# p and q are 512-bit primes, so n is ~1024-bit.
# phi is also ~1024-bit and very close to n.
# So (n - hint) / (2^500) will give us an approximate value for k.
# We'll search in a small range around this approximation.

# Initial estimate for k
k_approx = (n - hint) // (1 << 500)

# The search range for k might need to be adjusted if it doesn't find it quickly.
# A range of a few hundred around k_approx should be sufficient.
search_range = 10000  # Adjust as needed

for k_offset in range(-search_range, search_range + 1):
    k = k_approx + k_offset
    phi_candidate = (k << 500) | hint

    # Check if phi_candidate has the correct hint part
    if (phi_candidate & ((1 << 500) - 1)) != hint:
        continue # Should not happen if k_offset is small, but good for robustness

    # p + q = n - phi + 1
    sum_pq = n - phi_candidate + 1

    # Solve the quadratic equation: x^2 - (p+q)x + n = 0
    # Discriminant delta = (p+q)^2 - 4n
    delta = gmpy2.square(sum_pq) - 4 * n

    if gmpy2.is_square(delta):
        sqrt_delta = gmpy2.isqrt(delta)
        p = (sum_pq - sqrt_delta) // 2
        q = (sum_pq + sqrt_delta) // 2

        if p * q == n:
            print(f"Found p: {p}")
            print(f"Found q: {q}")
            print(f"Found phi: {phi_candidate}")

            # Calculate the private exponent d
            d = gmpy2.invert(e, phi_candidate)
            print(f"Calculated d: {d}")

            # Decrypt the message
            m = pow(c, d, n)
            flag = long_to_bytes(m)
            print(f"Decrypted flag: {flag.decode()}")
            break
```




```
deadsec{1_w0nd3r_1f_7h15_p40bl3m_c0u1d_b3_s0lv3d_1f_m0r3_b1t7_w343_unKn0wn}
```