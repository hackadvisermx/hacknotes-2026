_Difficulty:_ 

I'm not JJ. I like music, quantum pancakes, and social engineering. I accept AI tokens.

I just spotted a mysterious gnome - he winked and vanished, or maybe he's still here?

Things are getting strange, and I think we've wandered into a quantum conundrum!

If you help me unravel these riddles, we might just outsmart future quantum computers.

Cryptic puzzles, quirky gnomes, and post-quantum secrets—will you leap with me?


```
                                                                     +---------------------------------+
                                                                     |  "If we knew the unknown, the   |
                                                                     |  unknown wouldn't be unknown."  |
                                                                     |   — Quantum Leap (TV series)    |
                                                                     +---------------------------------+

                                                                        You observed me, the Gnome...
                                                                         ...and I observed you back.
                                                                      Did you see me? Am I here or not?
                                                                               Both? Neither?
                                                                     Am I a figment of your imagination?
                                                             Nay, I am the QuantGnome. Welcome to my challenge!
                                                                                     ***
                                                   Like me, the world of cryptography is full of mysteries and surprises.
                                                     In this challenge, you will learn about the latest advancements in 
                                                 post-quantum cryptography (PQC), and how they can help secure our digital 
                                                           future against the threats posed by quantum computers.

                                                               I am a reminder that the future is uncertain, 
                                                                   but with the right tools and knowledge,
                                                              we can navigate the unknowns and emerge stronger.

                                                                         Take the PQC leap with me!

                                                       I have created a *PQC* key generation program on this system. 
                                                                            Find and execute it.


```

```
qgnome@quantgnome_leap:/$ find / -name *pqc* 2>/dev/null
/usr/local/bin/pqc-keygen


qgnome@quantgnome_leap:/$ /usr/local/bin/pqc-keygen

— Summary -> Total algorithms = 28 | ✔ Keys generated = 28

Next, use -t to display key characteristics.

qgnome@quantgnome_leap:/$ /usr/local/bin/pqc-keygen -t
Algorithm                             Bits  NIST    Kind   
------------------------------------  ----  ----  ---------
sphincssha2128fsimple                   32   1          PQC
sphincssha2256fsimple                   64   5          PQC
ed25519                                256   0    Classical
ecdsa-nistp256-sphincssha2128fsimple   288   1       Hybrid
ecdsa-nistp521-sphincssha2256fsimple   585   5       Hybrid
falcon512                              897   1          PQC
ecdsa-nistp256-falcon512              1153   1       Hybrid
mldsa-44                              1312   0          PQC
ecdsa-nistp256-mldsa-44               1568   1       Hybrid
falcon1024                            1793   5          PQC
mldsa-65                              1952   0          PQC
rsa-2048                              2048   0    Classical
ecdsa-nistp521-falcon1024             2314   5       Hybrid
ecdsa-nistp384-mldsa-65               2336   3       Hybrid
mldsa-87                              2592   0          PQC
mayo3                                 2986   3          PQC
rsa-3072                              3072   1    Classical
rsa3072-sphincssha2128fsimple         3104   1       Hybrid
ecdsa-nistp521-mldsa-87               3113   5       Hybrid
ecdsa-nistp384-mayo3                  3370   3       Hybrid
rsa3072-falcon512                     3969   1       Hybrid
rsa-4096                              4096   1    Classical
rsa3072-mldsa-44                      4384   0       Hybrid
mayo2                                 4912   1          PQC
ecdsa-nistp256-mayo2                  5168   1       Hybrid
mayo5                                 5554   5          PQC
ecdsa-nistp521-mayo5                  6075   5       Hybrid
rsa3072-mayo2                         7984   1       Hybrid
------------------------------------  ----  ----  ---------

You can use 'ssh-keygen -l -f <private key>' to see the bit size of a key.
Next step, SSH into pqc-server.com.
```

```
qgnome@quantgnome_leap:~$ /usr/local/bin/pqc-keygen --help
usage: pqc-keygen [-h] [-p PATH] [-t] [-f]

Generate or inspect PQC / classical SSH keys

options:
  -h, --help            show this help message and exit
  -p PATH, --path PATH  Destination directory for keys
  -t, --table           Show table (requires existing keys)
  -f, --force           Overwrite existing keys without prompt
```


```
ssh -i id_rsa gnome1@pqc-server.com

###############################################################################################################################################################################

Welcome, gnome1 user! You made the first leap!

You authenticated with an RSA key, but that isn't very secure in a post-quantum world. RSA depends on large prime numbers, which a quantum computer can easily solve with 
something like Shor's algorithm.

Take a look around and see if you can find a way to login to the gnome2 account.

###############################################################################################################################################################################
gnome1@pqc-server:~$ 
```



```
gnome1@pqc-server:~/.ssh$ ssh -i id_ed25519 gnome2@pqc-server.com
###############################################################################################################################################################################

Welcome, gnome2 user! You made the second leap!

You authenticated with an ED25519 key, smaller than an RSA key, but still not secure in a post-quantum world due to Shor's algorithm.

Take a look around and see if you can find a way to login to the gnome3 account.

###############################################################################################################################################################################
gnome2@pqc-server:~$ 
```

```
gnome2@pqc-server:~/.ssh$ ssh -i id_mayo2 gnome3@pqc-server.com
###############################################################################################################################################################################

Welcome, gnome3 user! You made the third leap!

You authenticated with a MAYO post-quantum key. 
A post-quantum cryptographic algorithm with promising results for embedded systems. HOWEVER, use MAYO with caution! Wait for a standardized implementation (if/when 
that happens).

Take a look around and see if you can find a way to login to the gnome4 account.

###############################################################################################################################################################################
gnome3@pqc-server:~$ 
```


```
gnome3@pqc-server:~/.ssh$ ssh -i id_ecdsa_nistp256_sphincssha2128fsimple gnome4@pqc-server.com
###############################################################################################################################################################################

Welcome, gnome4 user! You made the fourth leap!

You authenticated with a post-quantum hybrid key! What does that mean? A blended approach with proven classical cryptography and post-quantum cryptography.

In this case, you authenticated with a NIST P-256 ECDSA key (a classical elliptic curve) that also uses post-quantum SPHINCS+ (standardized by NIST in FIPS 205 as SLH-DSA). 
That makes this key extremely robust. According to NIST, this is a security level 1 key, which means this key is at least as strong as AES128.

Instead of a single exchange/signature (as with RSA or ED25519), this key produces two (one classical and one post-quantum) that are both checked together. If one fails, 
authentication fails. A hybrid approach is a great first step when testing and implementing post-quantum cryptography, giving organizations 'Quantum Agility'.

Take a look around and see if you can find a way to login to the admin account.

########################################
```

```
gnome4@pqc-server:~/.ssh$ ssh -i id_ecdsa_nistp521_mldsa87 admin@pqc-server.com
###############################################################################################################################################################################

You made the QuantGnome Leap! Your final stop.

You authenticated with another hybrid post-quantum key. What is different about this key? It uses the NIST P-521 elliptic curve (roughly equivalent to a 15360-bit RSA key) 
paired with ML-DSA-87. According to NIST, ML-DSA-87 is a security level 5 algorithm, which provides the highest security level and is meant for the most secure environments. 
NIST standardized CRYSTALS-Dilithium as ML-DSA in FIPS 204 with three defined security levels:

- ML-DSA-44: Security Level 2 - At least as strong as SHA256/SHA3-256
- ML-DSA-65: Security Level 3 - At least as strong as AES192
- ML-DSA-87: Security Level 5 - At least as strong as AES256

This is one of the strongest hybrid keys available in post-quantum cryptography. The other extremely strong security level 5 algorithms all use a combination of 
the NIST P-521 elliptic curve and one of the following PQC algorithms:

- falcon1024: Falcon (FN-DSA) with a 1024 lattice dimensional size
- sphincssha2256fsimple: SLH-DSA (SPHINCS+) using SHA2 256 and fast signature generation (hence the 'f' in the algorithm name)
- mayo5: MAYO-5 is the highest of the four MAYO security levels

This entire build/system is based off of the Linux Foundation's Open Quantum Safe (OQS) initiative. It uses the OQS liboqs library which provides PQC algorithm support.
You can find out more about the OQS initiative at https://openquantumsafe.org/.

Next Step: You now have access to a directory in the same location as the SSH daemon. Time to look around for your final flag.
######################################################################################################################
```

```

dmin@quantgnome_leap:/opt/oqs-ssh/flag$ cat flag 
HHC{L3aping_0v3r_Quantum_Crypt0}
admin@quantgnome_leap:/opt/oqs-ssh/flag$ 
```