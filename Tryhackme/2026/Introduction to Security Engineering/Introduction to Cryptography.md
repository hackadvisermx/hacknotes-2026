#gpg #openssl

# Introduction to Cryptography

Learn about encryption algorithms such as AES, Diffie-Hellman key exchange, hashing, PKI, and TLS.

# Task 1 Introduction

The purpose of this room is to introduce users to basic cryptography concepts such as:

- Symmetric encryption, such as AES
- Asymmetric encryption, such as RSA
- Diffie-Hellman Key Exchange
- Hashing
- PKI

Suppose you want to send a message that no one can understand except the intended recipient. How would you do that?

One of the simplest ciphers is the Caesar cipher, used more than 2000 years ago. Caesar Cipher shifts the letter by a fixed number of places to the left or to the right. Consider the case of shifting by 3 to the right to encrypt, as shown in the figure below.

The recipient needs to know that the text was shifted by 3 to the right to recover the original message.

Using the same key to encrypt “TRY HACK ME”, we get “WUB KDFN PH”.

The Caesar Cipher that we have described above can use a key between 1 and 25. With a key of 1, each letter is shifted by one position, where A becomes B, and Z becomes A. With a key of 25, each letter is shifted by 25 positions, where A becomes Z, and B becomes A. A key of 0 means no change; moreover, a key of 26 will also lead to no change as it would lead to a full rotation. Consequently, we conclude that Caesar Cipher has a keyspace of 25; there are 25 different keys that the user can choose from.

Consider the case where you have intercepted a message encrypted using Caesar Cipher: “YMNX NX FQUMF GWFAT HTSYFHYNSL YFSLT MTYJQ RNPJ”. We are asked to decrypt it without knowledge of the key. We can attempt this by using brute force, i.e., we can try all the possible keys and see which one makes the most sense. In the following figure, we noticed that key being 5 makes the most sense, “THIS IS ALPHA BRAVO CONTACTING TANGO HOTEL MIKE.”

Caesar cipher is considered a **substitution cipher** because each letter in the alphabet is substituted with another.

Another type of cipher is called **transposition cipher**, which encrypts the message by changing the order of the letters. Let’s consider a simple transposition cipher in the figure below. We start with the message, “THIS IS ALPHA BRAVO CONTACTING TANGO HOTEL MIKE”, and the key `42351`. After we write the letters of our message by filling one column after the other, we rearrange the columns based on the key and then read the rows. In other words, we write by columns and we read by rows. Also notice that we ignored all the space in the plaintext in this example.  The resulting ciphertext “NPCOTGHOTH…” is read one row after the other. In other words, a transposition cipher simply rearranges the order of the letters, unlike the substitution cipher, which substitutes the letters without changing their order.


This task introduced simple substitution and transposition ciphers and applied them to messages made of alphabetic characters. For an encryption algorithm to be considered **secure**, it should be infeasible to recover the original message, i.e., plaintext. (In mathematical terms, we need a **hard** problem, i.e., a problem that cannot be solved in polynomial time. A problem that we can solve in polynomial time is a problem that’s feasible to solve even for large input, although it might take the computer quite some time to finish.)

If the encrypted message can be broken in one week, the encryption used would be considered insecure. However, if the encrypted message can be broken in 1 million years, the encryption would be considered practically secure.

Consider the mono-alphabetic substitution cipher, where each letter is mapped to a new letter. For example, in English, you would map “a” to one of the 26 English letters, then you would map “b” to one of the remaining 25 English letters, and then map “c” to one of the remaining 24 English letters, and so on.

For example, we might choose the letters in the alphabet “abcdefghijklmnopqrstuvwxyz” to be mapped to “xpatvrzyjhecsdikbfwunqgmol” respectively. In other words, “a” becomes “x”, “b” becomes “p”, and so on. The recipient needs to know the key, “xpatvrzyjhecsdikbfwunqgmol”, to decrypt the encrypted messages successfully.

This algorithm might look very secure, especially since trying all the possible keys is not feasible. However, different techniques can be used to break a ciphertext using such an encryption algorithm. One weakness of such an algorithm is letter frequency. In English texts, the most common letters are ‘e’, ‘t’, and ‘a’, as they appear at a frequency of 13%, 9.1%, and 8.2%, respectively. Moreover, in English texts, the most common first letters are ‘t’, ‘a’, and ‘o’, as they appear at 16%, 11.7% and 7.6%, respectively. Add to this the fact that most of the message words are dictionary words, and you will be able to break an encrypted text with the alphabetic substitution cipher in no time.

We don’t really need to use the encryption key to decrypt the received ciphertext, “Uyv sxd gyi siqvw x sinduxjd pvzjdw po axffojdz xgxo wsxcc wuidvw.” As shown in the figure below, using a website such as [quipqiup](https://www.quipqiup.com/), it will take a moment to discover that the original text was “The man who moves a mountain begins by carrying away small stones.” This example clearly indicates that this algorithm is broken and should not be used for confidential communication.

## Answer the questions below

You have received the following encrypted message:

_“Xjnvw lc sluxjmw jsqm wjpmcqbg jg wqcxqmnvw; xjzjmmjd lc wjpm sluxjmw jsqm bqccqm zqy.” Zlwvzjxj Zpcvcol_

You can guess that it is a quote. Who said it?

Miyamoto Musashi

# Task 2 Symmetric Encryption

Let’s review some terminology:

- **Cryptographic Algorithm** or **Cipher**: This algorithm defines the encryption and decryption processes.
- **Key**: The cryptographic algorithm needs a key to convert the plaintext into ciphertext and vice versa.
- **plaintext** is the original message that we want to encrypt
- **ciphertext** is the message in its encrypted form

A symmetric encryption algorithm uses the same key for encryption and decryption. Consequently, the communicating parties need to agree on a secret key before being able to exchange any messages.

In the following figure, the sender provides the _encrypt_ process with the plaintext and the key to get the ciphertext. The ciphertext is usually sent over some communication channel.

On the other end, the recipient provides the _decrypt_ process with the same key used by the sender to recover the original plaintext from the received ciphertext. Without knowledge of the key, the recipient won’t be able to recover the plaintext.

National Institute of Standard and Technology (NIST) published the Data Encryption Standard (DES) in 1977. DES is a symmetric encryption algorithm that uses a key size of 56 bits. In 1997, a challenge to break a message encrypted using DES was solved. Consequently, it was demonstrated that it had become feasible to use a brute-force search to find the key and break a message encrypted using DES. In 1998, a DES key was broken in 56 hours. These cases indicated that DES could no longer be considered secure.

NIST published the Advanced Encryption Standard (AES) in 2001. Like DES, it is a symmetric encryption algorithm; however, it uses a key size of 128, 192, or 256 bits, and it is still considered secure and in use today. AES repeats the following four transformations multiple times:

1. `SubBytes(state)`: This transformation looks up each byte in a given substitution table (S-box) and substitutes it with the respective value. The `state` is 16 bytes, i.e., 128 bits, saved in a 4 by 4 array.
2. `ShiftRows(state)`: The second row is shifted by one place, the third row is shifted by two places, and the fourth row is shifted by three places. This is shown in the figure below.
3. `MixColumns(state)`: Each column is multiplied by a fixed matrix (4 by 4 array).
4. `AddRoundKey(state)`: A round key is added to the state using the XOR operation.

The total number of transformation rounds depends on the key size.  

Don’t worry if you find this cryptic because it is! Our purpose is not to learn the details of how AES works nor to implement it as a programming library; the purpose is to appreciate the difference in complexity between ancient encryption algorithms and modern ones. If you are curious to dive into details, you can check the AES specifications, including pseudocode and examples in its published standard, [FIPS PUB 197](https://csrc.nist.gov/publications/detail/fips/197/final).

In addition to AES, many other symmetric encryption algorithms are considered secure. Here is a list of symmetric encryption algorithms supported by GPG (GnuPG) 2.37.7, for example:

|Encryption Algorithm|Notes|
|---|---|
|AES, AES192, and AES256|AES with a key size of 128, 192, and 256 bits|
|IDEA|International Data Encryption Algorithm (IDEA)|
|3DES|Triple DES (Data Encryption Standard) and is based on DES. We should note that 3DES will be deprecated in 2023 and disallowed in 2024.|
|CAST5|Also known as CAST-128. Some sources state that CAST stands for the names of its authors: Carlisle Adams and Stafford Tavares.|
|BLOWFISH|Designed by Bruce Schneier|
|TWOFISH|Designed by Bruce Schneier and derived from Blowfish|
|CAMELLIA128, CAMELLIA192, and CAMELLIA256|Designed by Mitsubishi Electric and NTT in Japan. Its name is derived from the flower camellia japonica.|

All the algorithms mentioned so far are block cipher symmetric encryption algorithms. A block cipher algorithm converts the input (plaintext) into blocks and encrypts each block. A block is usually 128 bits. In the figure below, we want to encrypt the plaintext “TANGO HOTEL MIKE”, a total of 16 characters. The first step is to represent it in binary. If we use ASCII, “T” is `0x54` in hexadecimal format, “A” is `0x41`, and so on. Every two hexadecimal digits constitute 8 bits and represent one byte. A block of 128 bits is practically 16 bytes and is represented in a 4 by 4 array. The 128-bit block is fed as one unit to the encryption method.

The other type of symmetric encryption algorithm is stream ciphers, which encrypt the plaintext byte by byte. Consider the case where we want to encrypt the message “TANGO HOTEL MIKE”; each character needs to be converted to its binary representation. If we use ASCII, “T” is `0x54` in hexadecimal, while “A” is `0x41`, and so on. The encryption method will process one byte at a time. This is represented in the figure below.

Symmetric encryption solves many security problems discussed in the [Security Principles](https://tryhackme.com/room/securityprinciples) room. Let’s say that Alice and Bob met and chose an encryption algorithm and agreed on a specific key. We assume that the selected encryption algorithm is secure and that the secret key is kept safe. Let’s take a look at what we can achieve:

- **Confidentiality**: If Eve intercepted the encrypted message, she wouldn’t be able to recover the plaintext. Consequently, all messages exchanged between Alice and Bob are confidential as long as they are sent encrypted.
- **Integrity**: When Bob receives an encrypted message and decrypts it successfully using the key he agreed upon with Alice, Bob can be sure that no one could tamper with the message across the channel. When using secure modern encryption algorithms, any minor modification to the ciphertext would prevent successful decryption or would lead to gibberish as plaintext.
- **Authenticity**: Being able to decrypt the ciphertext using the secret key also proves the authenticity of the message because only Alice and Bob know the secret key.

We are just getting started, and we know how to maintain confidentiality, check the integrity and ensure the authenticity of the exchanged messages. More practical and efficient approaches will be presented in later tasks. The question, for now, is whether this is scalable.

With Alice and Bob, we needed one key. If we have Alice, Bob, and Charlie, we need three keys: one for Alice and Bob, another for Alice and Charlie, and a third for Bob and Charlie. However, the number of keys grows quickly; communication between 100 users requires almost 5000 different secret keys. (If you are curious about the mathematics behind it, that’s 99 + 98 + 97 + … + 1 = 4950).

Moreover, if one system gets compromised, they need to create new keys to be used with the other 99 users. Another problem would be finding a secure channel to exchange the keys with all the other users. Obviously, this quickly grows out of hand.

In the next task, we will cover asymmetric encryption. One of the problems solved with asymmetric encryption is when 100 users only need to share a total of 100 keys to communicate securely. (As explained earlier, symmetric encryption would require around 5000 keys to secure the communications for 100 users.)

There are many programs available for symmetric encryption. We will focus on two, which are widely used for asymmetric encryption as well:

- GNU Privacy Guard
- OpenSSL Project

### GNU Privacy Guard

The [GNU Privacy Guard](https://gnupg.org/), also known as GnuPG or GPG, implements the OpenPGP standard.

We can encrypt a file using GnuPG (GPG) using the following command:

`gpg --symmetric --cipher-algo CIPHER message.txt`, where CIPHER is the name of the encryption algorithm. You can check supported ciphers using the command `gpg --version`. The encrypted file will be saved as `message.txt.gpg`.

The default output is in the binary OpenPGP format; however, if you prefer to create an ASCII armoured output, which can be opened in any text editor, you should add the option `--armor`. For example, `gpg --armor --symmetric --cipher-algo CIPHER message.txt`.

You can decrypt using the following command:

`gpg --output original_message.txt --decrypt message.gpg`


### OpenSSL Project

The [OpenSSL Project](https://www.openssl.org/) maintains the OpenSSL software.

We can encrypt a file using OpenSSL using the following command:

`openssl aes-256-cbc -e -in message.txt -out encrypted_message`

We can decrypt the resulting file using the following command:

`openssl aes-256-cbc -d -in encrypted_message -out original_message.txt`

To make the encryption more secure and resilient against brute-force attacks, we can add `-pbkdf2` to use the Password-Based Key Derivation Function 2 (PBKDF2); moreover, we can specify the number of iterations on the password to derive the encryption key using `-iter NUMBER`. To iterate 10,000 times, the previous command would become:

`openssl aes-256-cbc -pbkdf2 -iter 10000 -e -in message.txt -out encrypted_message`

Consequently, the decryption command becomes:

`openssl aes-256-cbc -pbkdf2 -iter 10000 -d -in encrypted_message -out original_message.txt`

In the following questions, we will use `gpg` and `openssl` on the AttackBox to carry out symmetric encryption.

The necessary files for this task are located under `/root/Rooms/cryptographyintro/task02`. **The zip file attached to this task can be used to tackle the questions of tasks 2, 3, 4, 5, and 6**.

## Answer the questions below

Decrypt the file `quote01` encrypted (using AES256) with the key `s!kR3T55` using `gpg`. What is the third word in the file?

 ```
 gpg --output text.txt --decrypt quote01.txt.gpg
 
cat text.txt
Do not waste time idling or thinking after you have set your goals.
Miyamoto Musashi

waste
 
 ```

Decrypt the file `quote02` encrypted (using AES256-CBC) with the key `s!kR3T55` using `openssl`. What is the third word in the file?

```
openssl aes-256-cbc -pbkdf2 -iter 10000 -d -in quote02  -out text2.txt
FALLO




 task02 openssl aes-256-cbc -d -in quote02  -out text2.txt
enter AES-256-CBC decryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
➜  task02 cat text2.txt
The true science of martial arts means practicing them in such a way that they will be useful at any time, and to teach them in such a way that they will be useful in all things.
Miyamoto Musashi
➜  task02


```

Decrypt the file `quote03` encrypted (using CAMELLIA256) with the key `s!kR3T55` using `gpg`. What is the third word in the file?

```
gpg --batch --passphrase 's!kR3T55' --output text3.txt --decrypt quote03.txt.gpg
gpg: CAMELLIA256.CFB encrypted data
gpg: encrypted with 1 passphrase

cat text3.txt
You must understand that there is more than one path to the top of the mountain.
Miyamoto Musashi


```


# Task 3 Asymmetric Encryption

Symmetric encryption requires the users to find a secure channel to exchange keys. By secure channel, we are mainly concerned with confidentiality and integrity. In other words, we need a channel where no third party can eavesdrop and read the traffic; moreover, no one can change the sent messages and data.

Asymmetric encryption makes it possible to exchange encrypted messages without a secure channel; we just need a reliable channel. By reliable channel, we mean that we are mainly concerned with the channel’s integrity and not confidentiality.

When using an asymmetric encryption algorithm, we would generate a key pair: a public key and a private key. The public key is shared with the world, or more specifically, with the people who want to communicate with us securely. The private key must be saved securely, and we must never let anyone access it. Moreover, it is not feasible to derive the private key despite the knowledge of the public key.

How does this key pair work?

If a message is encrypted with one key, it can be decrypted with the other. In other words:

- If Alice encrypts a message using Bob’s public key, it can be decrypted only using Bob’s private key.
- Reversely, if Bob encrypts a message using his private key, it can only be decrypted using Bob’s public key.

### Confidentiality

We can use asymmetric encryption to achieve confidentiality by encrypting the messages using the recipient’s public key. In the following two figures, we can see that:

Alice wants to ensure confidentiality in her communication with Bob. She encrypts the message using Bob’s public key, and Bob decrypts them using his private key. Bob’s public key is expected to be published on a public database or on his website, for instance.


When Bob wants to reply to Alice, he encrypts his messages using Alice’s public key, and Alice can decrypt them using her private key.

We executed three commands:

- `openssl genrsa -out private-key.pem 2048`: With `openssl`, we used `genrsa` to generate an RSA private key. Using `-out`, we specified that the resulting private key is saved as `private-key.pem`. We added `2048` to specify a key size of 2048 bits.
- `openssl rsa -in private-key.pem -pubout -out public-key.pem`: Using `openssl`, we specified that we are using the RSA algorithm with the `rsa` option. We specified that we wanted to get the public key using `-pubout`. Finally, we set the private key as input using `-in private-key.pem` and saved the output using `-out public-key.pem`.
- `openssl rsa -in private-key.pem -text -noout`: We are curious to see real RSA variables, so we used `-text -noout`. The values of _p_, _q_, _N_, _e_, and _d_ are `prime1`, `prime2`, `modulus`, `publicExponent`, and `privateExponent`, respectively.

If we already have the recipient’s public key, we can encrypt it with the command `openssl pkeyutl -encrypt -in plaintext.txt -out ciphertext -inkey public-key.pem -pubin`

The recipient can decrypt it using the command `openssl pkeyutl -decrypt -in ciphertext -inkey private-key.pem -out decrypted.txt`

## Answer the questions below

On the AttackBox, you can find the directory for this task located at `/root/Rooms/cryptographyintro/task03`; alternatively, you can use the task file from Task 2 to work on your own machine.

### Bob has received the file `ciphertext_message` sent to him from Alice. You can find the key you need in the same folder. What is the first word of the original plaintext?

 ```
 
➜  task03 openssl pkeyutl -decrypt -in ciphertext_message -inkey private-key-bob.pem -out decrypted1.txt
➜  task03 cat decrypted1.txt
"Perception is strong and sight weak. In strategy it is important to see distant things as if they were close and to take a distanced view of close things."
Miyamoto Musashi
➜  task03
 
 
 ```

### Take a look at Bob’s private RSA key. What is the last byte of _p_?

```
openssl rsa -in private-key-bob.pem -text -noout
Private-Key: (2048 bit, 2 primes)
modulus:
    00:e8:5e:73:7d:54:55:0a:cc:56:64:87:b3:4b:8e:
    24:df:96:b8:b9:5f:19:d4:71:a5:b9:5a:a8:d9:ab:
    b4:7b:7f:59:08:c5:9c:47:0d:73:92:97:b8:ef:67:
    b7:a6:5a:59:2c:e3:4c:ca:7f:53:1c:9e:34:32:0e:
    c6:7c:60:b2:d6:1f:30:b2:ed:da:14:e9:15:78:80:
    71:92:3c:26:32:a9:2b:3a:15:4e:48:2d:93:04:a5:
    21:c7:da:15:6c:dd:bc:89:0e:cc:54:be:84:d6:40:
    b8:47:59:d1:b2:27:c9:0d:43:55:de:33:dd:01:8f:
    bf:6c:3e:79:31:dd:e4:90:8d:c3:35:72:31:85:15:
    ae:ac:5a:96:c8:34:90:0e:32:4e:86:45:55:78:fb:
    13:ed:a4:fb:f0:64:b4:61:04:f6:7c:e3:56:aa:03:
    a3:43:1e:40:0b:98:1f:73:66:4a:5c:3a:25:69:2c:
    d9:92:f8:69:c1:5b:61:b7:f2:3a:68:28:e9:2b:75:
    08:9c:a4:63:9e:71:2b:63:aa:99:75:cf:78:00:23:
    fc:5a:df:2d:95:14:2f:e6:10:5d:a0:ff:4d:07:c8:
    d3:bb:2d:8f:0d:8a:fc:ab:43:5d:35:53:dc:72:a2:
    74:5b:c0:88:0d:ee:c3:1f:7b:1c:74:1a:5e:e1:c1:
    88:31
publicExponent: 65537 (0x10001)
privateExponent:
    02:3b:3b:4b:58:ce:a2:eb:e8:bd:ce:65:1f:b4:9d:
    bb:5d:41:d3:85:e0:ee:f3:fd:c3:69:e6:1f:db:a6:
    40:09:59:06:dc:89:98:fa:68:17:0a:f3:46:59:43:
    4a:35:a9:3a:e5:1e:8c:fd:ec:03:ba:56:85:f9:de:
    58:be:14:f9:8e:bd:c8:fa:15:13:5e:54:4b:c9:45:
    4d:ec:db:46:61:44:28:ff:f6:0b:26:0f:8e:06:87:
    ec:83:60:f1:4a:af:cf:76:74:ea:86:14:80:7a:33:
    f5:7b:71:fd:63:f9:bf:9c:30:96:e6:fd:ed:a5:e9:
    10:ab:b3:93:91:ad:ea:e0:17:99:e8:7b:3d:64:58:
    b1:74:3e:0e:81:5b:6d:fa:41:7a:23:26:4f:f1:24:
    a8:73:f3:36:24:a2:65:17:7d:5b:52:8e:1f:fc:b7:
    e6:53:bc:89:b0:e5:18:65:71:29:34:cb:f7:65:51:
    39:0c:62:33:24:b8:60:bf:89:8b:c8:f5:0d:7d:e5:
    85:cf:57:cf:c3:d8:44:10:8f:54:6c:04:99:8d:d7:
    fd:e2:74:18:7b:5c:6c:3c:e1:30:0a:8b:8b:55:70:
    88:8a:67:64:63:5c:65:8f:fa:92:cf:94:04:b9:8d:
    53:28:bb:31:d8:31:3c:4c:06:cd:b6:17:e9:51:d8:
    81
prime1:
    00:ff:ea:65:3e:e5:96:96:0b:66:55:f1:f9:d0:37:
    66:e9:35:a5:c3:43:ca:66:75:40:49:46:8d:85:a7:
    ff:f4:73:97:69:11:a1:1e:37:f9:e3:38:cb:c0:5e:
    56:e9:1a:0d:f2:9f:80:56:87:2a:99:bb:88:8e:93:
    35:5a:9a:c6:f7:99:44:90:88:09:33:a6:0d:ea:b4:
    56:98:66:20:9c:34:e7:b9:33:64:4f:08:01:08:62:
    44:68:8f:df:79:0d:84:2b:77:e7:03:8b:3c:7a:e3:
    e0:e0:ee:23:64:22:51:ed:dd:b8:1c:b3:75:c4:3f:
    4a:cf:fc:7c:57:0b:95:75:e7
prime2:
    00:e8:72:11:5c:b5:5c:14:19:85:ce:e7:d2:e9:54:
    7b:58:ae:32:e9:e6:39:a7:65:b4:90:2f:53:b5:9d:
    22:62:84:fe:52:86:f5:01:a2:9c:b0:4f:80:ee:d4:
    07:27:3b:69:02:70:33:da:7d:97:56:b9:3e:f3:a1:
    84:9e:73:6a:47:e5:99:8c:44:86:75:c1:bf:71:89:
    06:b0:ee:dd:16:45:e7:05:fa:02:bd:e6:3e:b7:f2:
    fe:e7:22:0b:ed:ca:23:a0:68:0b:fe:fb:c3:57:19:
    21:58:6e:73:1d:9d:3c:2a:8a:c1:7e:ea:73:67:5a:
    cb:3d:a8:9b:be:50:08:9e:27
exponent1:
    1e:20:56:c8:df:b8:29:73:b0:19:60:01:fb:8b:fa:
    16:6c:15:56:76:4d:86:60:39:30:27:19:13:e9:e2:
    0c:c1:ea:ca:18:a4:31:ed:7f:02:4b:b6:58:b0:02:
    65:30:87:01:cf:db:08:d4:a2:a4:34:5a:70:06:4e:
    5a:9b:2b:df:0b:f0:f1:5e:c2:4e:8d:36:c8:31:70:
    9c:42:31:86:92:07:d1:5a:86:6d:73:50:c3:ce:e5:
    a4:b5:83:26:39:fc:1c:2d:e2:49:1d:84:02:27:7f:
    5a:9b:4e:19:44:9d:06:76:7a:6d:0e:87:47:91:f7:
    d9:a2:2c:75:06:cd:12:73
exponent2:
    28:a9:f3:e1:9d:14:9b:ab:8f:5e:0f:ee:34:c5:83:
    c2:92:ce:f3:5e:44:4d:c5:9c:1d:f1:39:9a:b6:ff:
    91:ee:a4:33:39:ca:d8:db:62:bf:f1:58:a3:ef:51:
    c5:0a:3e:a7:9f:8b:62:b8:bf:e5:fb:08:49:44:c3:
    57:98:e7:49:e6:9f:c3:0b:25:de:a9:e3:5c:f0:54:
    cc:55:2d:36:3d:4a:5a:20:4f:a4:7b:08:13:d4:1d:
    c5:bf:8e:08:ae:69:27:21:ac:9f:91:d9:ad:7e:06:
    f8:5a:72:27:07:1f:c4:6d:7b:c6:41:2b:a9:34:18:
    04:14:60:12:9e:1b:b3:d7
coefficient:
    6e:69:83:47:fb:63:da:cc:a5:bb:98:e6:ff:a5:18:
    06:d2:7d:17:19:26:d7:bc:7a:72:13:5a:e3:7e:bc:
    e4:6b:ba:5c:ad:fd:b5:df:73:a0:2f:53:c4:70:f0:
    21:5b:86:13:46:96:ab:2e:4c:e1:c9:63:d0:13:73:
    9f:90:d8:20:59:3a:23:86:cf:1a:03:3b:4a:21:da:
    e8:77:28:3e:41:70:df:07:6e:7f:c0:25:6d:84:26:
    18:18:bc:78:07:2c:05:1f:b6:b8:73:38:c6:2b:ce:
    56:e7:e2:ff:12:bd:06:c4:0a:a6:f4:36:d1:cf:93:
    a6:d5:75:d3:22:b7:3b:3a
    
    
    
prime1: e7


``` 

### Take a look at Bob’s private RSA key. What is the last byte of _q_?

```
prime2 : 27
```


# Task 4 Diffie-Hellman Key Exchange

Alice and Bob can communicate over an insecure channel. By insecure, we mean that there are eavesdroppers who can read the messages exchanged on this channel. How can Alice and Bob agree on a secret key in such a setting? One way would be to use the Diffie-Hellman key exchange.

Diffie-Hellman is an asymmetric encryption algorithm. It allows the exchange of a secret over a public channel. We will skip the modular arithmetic background and provide a simple numeric example. We will need two mathematical operations: power and modulus. _x__p_, i.e., _x_ raised to the power _p_, is _x_ multiplied by itself _p_ times. Furthermore, _x_ mod _m_, i.e., _x_ modulus _m_, is the remainder of the division of _x_ by _m_.

1. Alice and Bob agree on _q_ and _g_. For this to work, _q_ should be a prime number, and _g_ is a number smaller than _q_ that satisfies certain conditions. (In modular arithmetic, _g_ is a generator.) In this example, we take _q_ = 29 and _g_ = 3.
2. Alice chooses a random number _a_ smaller than _q_. She calculates _A_ = (_g__a_) mod _q_. The number _a_ must be kept a secret; however, _A_ is sent to Bob. Let’s say that Alice picks the number _a_ = 13 and calculates _A_ = 313%29 = 19 and sends it to Bob.
3. Bob picks a random number _b_ smaller than _q_. He calculates _B_ = (_g__b_) mod _q_. Bob must keep _b_ a secret; however, he sends _B_ to Alice. Let’s consider the case where Bob chooses the number _b_ = 15 and calculates _B_ = 315%29 = 26. He proceeds to send it to Alice.
4. Alice receives _B_ and calculates _k__e__y_ = _B__a_ mod _q_. Numeric example _k__e__y_ = 2613 mod 29 = 10.
5. Bob receives _A_ and calculates _k__e__y_ = _A__b_ mod _q_. Numeric example _k__e__y_ = 1915 mod 29 = 10.

We can see that Alice and Bob reached the same key.

Although an eavesdropper has learned the values of _q_, _g_, _A_, and _B_, they won’t be able to calculate the secret _k__e__y_ that Alice and Bob have exchanged. The above steps are summarized in the figure below.


Although the numbers we have chosen make it easy to find _a_ and _b_, even without using a computer, real-world examples would select a _q_ of 256 bits in length. In decimal numbers, that’s 115 with 75 zeroes to its right (I don’t know how to read that either, but I was told it is read as 115 quattuorvigintillion). Such a large _q_ will make it infeasible to find _a_ or _b_ despite knowledge of _q_, _g_, _A_, and _B_.

Let’s take a look at actual Diffie-Hellman parameters. We can use `openssl` to generate them; we need to specify the option `dhparam` to indicate that we want to generate Diffie-Hellman parameters along with the specified size in bits, such as `2048` or `4096`.

In the console output below, we can view the prime number `P` and the generator `G` using the command `openssl dhparam -in dhparams.pem -text -noout`. (This is similar to what we did with the RSA private key.)

Diffie-Hellman key exchange algorithm allows two parties to agree on a secret over an insecure channel. However, the discussed key exchange is prone to a Man-in-the-Middle (MitM) attack; an attacker might reply to Alice pretending to be Bob and reply to Bob pretending to be Alice. We discuss a solution to this problem in Task 6.

## Answer the questions below

On the AttackBox, you can find the directory for this task located at `/root/Rooms/cryptographyintro/task04`; alternatively, you can use the task file from Task 2 to work on your own machine.

## A set of Diffie-Hellman parameters can be found in the file `dhparam.pem`. What is the size of the prime number in bits?

```
task04 cat dhparams.pem
-----BEGIN DH PARAMETERS-----
MIICCAKCAgEAwBBlxq3tiASIHudQGzAPBSwt1OpgRJ4q95ACiaR+BZkyONx1UArH
9mv3tJrf78rgzlVdMUg+nDVarQOch9ccSOQuKdyjkIEjf/owXPvYYnuWNe+aD4RJ
xEiXtWM4kQFJ8UIV/dqEppBNLQUQQc8GU1KA6xsRrV1j7f6x96dgHHm4iFSj5GRN
0wSn1XYXANREGdYSqR+qK6xz1lJQkhepzfaw7lVXpNuCbk8AIG9v9bFyl7DFOohH
hsbl3fyRL4IIBQxcwvhikmee8VMkwHbxPQxQMVtWJgo7BaO3vvnupIL4nUarqd25
BCVhWKoqu3wsyOHvrPlQ42QuMJz9SCYlfnXAVlgQjddhtN/3zr2c72+LR4wOzymr
6zNWF5kZ7jBf2Z2AbjyRBebNVcol8uPZyGh0HZ5K51MlHxcnP04pwhmD2k2PtWtc
3mdPARBIhJkywOXgi5/rThj3/8ZHsUe4sn88nL2TwnGztDf8rS7Zry0s+d5/Qos5
IddHjxjE3q1wCxF5xN/vDzqar4VOlQXKNZ5tk5vkZiN4K9n0R+T+KR6qy5VmovIq
w1r6wKB9U710Nx2xx2Znt3tfMrwv+oIKEhUvQRDNEnDM7innHLcH1CgfczwVwKId
K9sHV/cQKMft5DppxNlPD8K0SpcqLLN1d14aIZSMhfsNXpUPyHJZbE8CAQI=
-----END DH PARAMETERS-----
➜  task04 openssl dhparam -in dhparams.pem -text -noout
    DH Parameters: (4096 bit)
    P:
        00:c0:10:65:c6:ad:ed:88:04:88:1e:e7:50:1b:30:
        0f:05:2c:2d:d4:ea:60:44:9e:2a:f7:90:02:89:a4:
        7e:05:99:32:38:dc:75:50:0a:c7:f6:6b:f7:b4:9a:
        df:ef:ca:e0:ce:55:5d:31:48:3e:9c:35:5a:ad:03:
        9c:87:d7:1c:48:e4:2e:29:dc:a3:90:81:23:7f:fa:
        30:5c:fb:d8:62:7b:96:35:ef:9a:0f:84:49:c4:48:
        97:b5:63:38:91:01:49:f1:42:15:fd:da:84:a6:90:
        4d:2d:05:10:41:cf:06:53:52:80:eb:1b:11:ad:5d:
        63:ed:fe:b1:f7:a7:60:1c:79:b8:88:54:a3:e4:64:
        4d:d3:04:a7:d5:76:17:00:d4:44:19:d6:12:a9:1f:
        aa:2b:ac:73:d6:52:50:92:17:a9:cd:f6:b0:ee:55:
        57:a4:db:82:6e:4f:00:20:6f:6f:f5:b1:72:97:b0:
        c5:3a:88:47:86:c6:e5:dd:fc:91:2f:82:08:05:0c:
        5c:c2:f8:62:92:67:9e:f1:53:24:c0:76:f1:3d:0c:
        50:31:5b:56:26:0a:3b:05:a3:b7:be:f9:ee:a4:82:
        f8:9d:46:ab:a9:dd:b9:04:25:61:58:aa:2a:bb:7c:
        2c:c8:e1:ef:ac:f9:50:e3:64:2e:30:9c:fd:48:26:
        25:7e:75:c0:56:58:10:8d:d7:61:b4:df:f7:ce:bd:
        9c:ef:6f:8b:47:8c:0e:cf:29:ab:eb:33:56:17:99:
        19:ee:30:5f:d9:9d:80:6e:3c:91:05:e6:cd:55:ca:
        25:f2:e3:d9:c8:68:74:1d:9e:4a:e7:53:25:1f:17:
        27:3f:4e:29:c2:19:83:da:4d:8f:b5:6b:5c:de:67:
        4f:01:10:48:84:99:32:c0:e5:e0:8b:9f:eb:4e:18:
        f7:ff:c6:47:b1:47:b8:b2:7f:3c:9c:bd:93:c2:71:
        b3:b4:37:fc:ad:2e:d9:af:2d:2c:f9:de:7f:42:8b:
        39:21:d7:47:8f:18:c4:de:ad:70:0b:11:79:c4:df:
        ef:0f:3a:9a:af:85:4e:95:05:ca:35:9e:6d:93:9b:
        e4:66:23:78:2b:d9:f4:47:e4:fe:29:1e:aa:cb:95:
        66:a2:f2:2a:c3:5a:fa:c0:a0:7d:53:bd:74:37:1d:
        b1:c7:66:67:b7:7b:5f:32:bc:2f:fa:82:0a:12:15:
        2f:41:10:cd:12:70:cc:ee:29:e7:1c:b7:07:d4:28:
        1f:73:3c:15:c0:a2:1d:2b:db:07:57:f7:10:28:c7:
        ed:e4:3a:69:c4:d9:4f:0f:c2:b4:4a:97:2a:2c:b3:
        75:77:5e:1a:21:94:8c:85:fb:0d:5e:95:0f:c8:72:
        59:6c:4f
    G:    2 (0x2)
```
4096

### What is the prime number’s last byte (least significant byte)?

4f

# Task 5 Hashing

A cryptographic hash function is an algorithm that takes data of arbitrary size as its input and returns a fixed size value, called _message digest_ or _checksum_, as its output. For example, `sha256sum` calculates the SHA256 (Secure Hash Algorithm 256) message digest. SHA256, as the name indicates, returns a checksum of size 256 bits (32 bytes). This checksum is usually written using hexadecimal digits. Knowing that a hexadecimal digit represents 4 bits, the 256 bits checksum can be represented as 64 hexadecimal digits.

In the terminal output below, we calculate the SHA256 hash values for three files of varying sizes: 4 bytes, 275 MB, and 5.2 GB. Using `sha256sum` to calculate the message digest for each of the three files, we get three completely different values that appear random. It is worth stressing that the length of the resulting message digest or checksum is the same, no matter how small or big the file is. In particular, the four-byte file `abc.txt` and the 5.2 GB file resulted in message digests of equal length independent of the file size.

Terminal

```shell-session
user@TryHackMe$ ls -lh
total 5.5G
-rw-r--r--. 1 strategos strategos    4  7月 21 12:46 abc.txt
-rw-r--r--. 1 strategos strategos 275M  2月 12 19:08 debian-hurd.img.tar.xz
-rw-r--r--. 1 strategos strategos 5.2G  4月 26 16:55 Win11_English_x64v1.iso
$ sha256sum *
c38bb113c89d8fec6475a9936411007c45563ecb7ce8acd5db7fb58c0872bda0  abc.txt
0317ff0150e0d64b70284b28c97bb788310585ea7ac46cc8139d5a3c850dea55  debian-hurd.img.tar.xz
4bc6c7e7c61af4b5d1b086c5d279947357cff45c2f82021bb58628c2503eb64e  Win11_English_x64v1.iso
```

But why would we need such a function? There are many uses, in particular:

- Storing passwords: Instead of storing passwords in plaintext, a hash of the password is stored instead. Consequently, if a data breach occurs, the attacker will get a list of password hashes instead of the original passwords. (In practice, passwords are also “salted”, as discussed in a later task.)
- Detecting modifications: Any minor modification to the original file would lead to a drastic change in hash value, i.e. checksum.

In the following terminal output, we have two files, `text1.txt` and `text2.txt`, which are almost identical except for (literally) one bit being different; the letters `T` and `t` are different in one bit in their ASCII representation. Even though we have flipped only a single bit, it is evident that the SHA256 checksums are entirely different. Consequently, if we use a secure hash function algorithm, we can easily confirm whether any modifications have taken place. This can help protect against both intentional tampering and file transfer errors.

Terminal

```shell-session
user@TryHackMe$ hexdump text1.txt -C
00000000  54 72 79 48 61 63 6b 4d  65 0a                    |TryHackMe.|
0000000a
$ hexdump text2.txt -C
00000000  74 72 79 48 61 63 6b 4d  65 0a                    |tryHackMe.|
0000000a
$ sha256sum text1.txt
f4616fd825a10ded9af58fbaee09f3e31751d15591f9323ea68b03a0e8ac3783  text1.txt
$ sha256sum text2.txt
9ffa3533ee33998aeb1df76026f8031c8af6ccabd8393eca002d5b7471a0b536  text2.txt
```

Some of the hashing algorithms in use and still considered secure are:

- SHA224, SHA256, SHA384, SHA512
- RIPEMD160

Some older hash functions, such as MD5 (Message Digest 5) and SHA-1, are cryptographically broken. By broken, we mean that it is possible to generate a different file with the same checksum as a given file. This means that we can create a hash collision. In other words, an attacker can create a new message with a given checksum, and detecting file or message tampering won’t be possible.

### HMAC

Hash-based message authentication code (HMAC) is a message authentication code (MAC) that uses a cryptographic key in addition to a hash function.

According to [RFC2104](https://www.rfc-editor.org/rfc/rfc2104), HMAC needs:

- secret key
- inner pad (ipad) a constant string. (RFC2104 uses the byte `0x36` repeated B times. The value of B depends on the chosen hash function.)
- outer pad (opad) a constant string. (RFC2104 uses the byte `0x5C` repeated B times.)

Calculating the HMAC follows the following steps as shown in the figure:

1. Append zeroes to the key to make it of length B, i.e., to make its length match that of the ipad.
2. Using bitwise exclusive-OR (XOR), represented by ⊕, calculate _k__e__y_ ⊕ _i__p__a__d_.
3. Append the message to the XOR output from step 2.
4. Apply the hash function to the resulting stream of bytes (in step 3).
5. Using XOR, calculate _k__e__y_ ⊕ _o__p__a__d_.
6. Append the hash function output from step 4 to the XOR output from step 5.
7. Apply the hash function to the resulting stream of bytes (in step 6) to get the HMAC.

The figure above represents the steps expressed in the following formula: _H_(_K_⊕_o__p__a__d_,_H_(_K_⊕_i__p__a__d_,_t__e__x__t_)).

To calculate the HMAC on a Linux system, you can use any of the available tools such as `hmac256` (or `sha224hmac`, `sha256hmac`, `sha384hmac`, and `sha512hmac`, where the secret key is added after the option `--key`). Below we show an example of calculating the HMAC using `hmac256` and `sha256hmac` with two different keys.

Terminal

```shell-session
user@TryHackMe$ hmac256 s!Kr37 message.txt
3ec65b7e80c5bf2e623e52e0528f1c6a74f605b10616621ba1c22a89fb244e65  message.txt

user@TryHackMe$ hmac256 1234 message.txt
4b6a2783631180fca6128592e3d17fb5bff6b0e563ad8f1c6afc1050869e440f  message.txt

user@TryHackMe$ sha256hmac message.txt --key s!Kr37
3ec65b7e80c5bf2e623e52e0528f1c6a74f605b10616621ba1c22a89fb244e65  message.txt

user@TryHackMe$ sha256hmac message.txt --key 1234
4b6a2783631180fca6128592e3d17fb5bff6b0e563ad8f1c6afc1050869e440f  message.txt
```

## Answer the questions below

On the AttackBox, you can find the directory for this task located at `/root/Rooms/cryptographyintro/task05`; alternatively, you can use the task file from Task 2 to work on your own machine.

### What is the SHA256 checksum of the file `order.json`?

```
sha256sum order.json
2c34b68669427d15f76a1c06ab941e3e6038dacdfb9209455c87519a3ef2c660  order.json
```

### Open the file `order.json` and change the amount from `1000` to `9000`. What is the new SHA256 checksum?  

```
sha256sum order1.json
11faeec5edc2a2bad82ab116bbe4df0f4bc6edd96adac7150bb4e6364a238466  order1.json
```

Using SHA256 and the key `3RfDFz82`, what is the HMAC of `order.txt`?

```
openssl dgst -sha256 -hmac "3RfDFz82" order.txt
HMAC-SHA2-256(order.txt)= c7e4de386a09ef970300243a70a444ee2a4ca62413aeaeb7097d43d2c5fac89f
```
# Task 6 PKI and SSL/TLS

Using a key exchange such as the Diffie-Hellman key exchange allows us to agree on a secret key under the eyes and ears of eavesdroppers. This key can be used with a symmetric encryption algorithm to ensure confidential communication. However, the key exchange we described earlier is not immune to Man-in-the-Middle (MITM) attack. The reason is that Alice has no way of ensuring that she is communicating with Bob, and Bob has no way of ensuring that he is communicating with Alice when exchanging the secret key.

Consider the figure below. It is an attack against the key exchange explained in the Diffie-Hellman Key Exchange task. The steps are as follows:

1. Alice and Bob agree on _q_ and _g_. Anyone listening on the communication channel can read these two values, including the attacker, Mallory.
2. As she would normally do, Alice chooses a random variable _a_, calculates _A_ ( _A_ = (_g__a_) mod _q_) and sends _A_ to Bob. Mallory has been waiting for this step, and she has selected a random variable _m_ and calculated the respective _M_. As soon as Mallory receives _A_, she sends _M_ to Bob, pretending she is Alice.
3. Bob receives _M_ thinking that Alice sent it. Bob has already picked a random variable _b_ and calculated the respective _B_; he sends _B_ to Alice. Similarly, Mallory intercepts the message, reads _B_ and sends _M_ to Alice instead.
4. Alice receives _M_ and calculates _k__e__y_ = _M__a_ mod _q_.
5. Bob receives _M_ and calculates _k__e__y_ = _M__b_ mod _q_.

Alice and Bob continue to communicate, thinking that they are communicating directly, unaware that they are communicating with Mallory, who can read and modify the messages before sending them to the intended recipient.


This susceptibility necessitates some mechanism that would allow us to confirm the other party’s identity. This brings us to Public Key Infrastructure (PKI).

Consider the case where you are browsing the website [example.org](https://example.org/) over HTTPS. How can you be confident that you are indeed communicating with the `example.org` server(s)? In other words, how can you be sure that no man-in-the-middle intercepted the packets and altered them before they reached you? The answer lies in the website certificate.

The figure below shows the page we get when browsing example.org. Most browsers represent the encrypted connection with some kind of a lock icon. This lock icon indicates that the connection is secured over HTTPS with a valid certificate.

At the time of writing, example.org uses a certificate signed by DigiCert Inc., as shown in the figure below. In other words, DigiCert confirms that this certificate is valid (till a certain date).


For a certificate to get signed by a certificate authority, we need to:

1. Generate Certificate Signing Request (CSR): You create a certificate and send your public key to be signed by a third party.
2. Send your CSR to a Certificate Authority (CA): The purpose is for the CA to sign your certificate. The alternative and usually insecure solution would be to self-sign your certificate.

For this to work, the recipient should recognize and trust the CA that signed the certificate. And as we would expect, our browser trusts DigiCert Inc as a signing authority; otherwise, it would have issued a security warning instead of proceeding to the requested website.

You can use `openssl` to generate a certificate signing request using the command `openssl req -new -nodes -newkey rsa:4096 -keyout key.pem -out cert.csr`. We used the following options:

- `req -new` create a new certificate signing request
- `-nodes` save private key without a passphrase
- `-newkey` generate a new private key
- `rsa:4096` generate an RSA key of size 4096 bits
- `-keyout` specify where to save the key
- `-out` save the certificate signing request

Then you will be asked to answer a series of questions, as shown in the console output below.

Once the CSR file is ready, you can send it to a CA of your choice to get it signed and ready to use on your server.

Once the client, i.e., the browser, receives a signed certificate it trusts, the SSL/TLS handshake takes place. The purpose would be to agree on the ciphers and the secret key.

We have just described how PKI applies to the web and SSL/TLS certificates. A trusted third party is necessary for the system to be scalable.

For testing purposes, we have created a self-signed certificate. For example, the following command will generate a self-signed certificate.

`openssl req -x509 -newkey -nodes rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 365`

The `-x509` indicates that we want to generate a self-signed certificate instead of a certificate request. The `-sha256` specifies the use of the SHA-256 digest. It will be valid for one year as we added `-days 365`.

To answer the questions below, you need to inspect the certificate file `cert.pem` in the `task06` directory. You can use the following command to view your certificate:

`openssl x509 -in cert.pem -text`

## Answer the questions below

On the AttackBox, you can find the directory for this task located at `/root/Rooms/cryptographyintro/task06`; alternatively, you can use the task file from Task 2 to work on your own machine.

## What is the size of the public key in bits?

```
openssl x509 -in cert.pem -text


Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            2b:29:0c:2f:b0:52:3a:79:89:1f:82:11:07:bd:9d:84:2a:23:d5:1c
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = UK, ST = London, L = London, O = Default Company Ltd
        Validity
            Not Before: Aug 11 11:34:19 2022 GMT
            Not After : Feb 25 11:34:19 2039 GMT
        Subject: C = UK, ST = London, L = London, O = Default Company Ltd
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (4096 bit)
                Modulus:
                    00:b2:92:13:57:5a:6f:34:e2:e1:f2:08:55:ae:a9:
                    cd:da:c8:e9:6b:bf:fd:5c:36:6d:d3:de:81:53:60:
                    e9:8a:ec:f6:84:1a:73:31:1a:73:cf:47:62:4a:61:
                    4e:9b:63:0d:ce:7c:74:3b:9e:d1:dc:ef:90:1e:de:
                    1b:fb:89:5c:03:f2:57:58:4a:d6:d1:d0:a5:eb:4d:
                    1f:c8:d7:c7:11:e0:38:c3:c3:20:5c:ef:23:09:71:
                    f7:54:68:78:d7:35:80:07:18:83:4a:ce:c6:82:5d:
                    1c:96:f6:ab:11:67:86:5e:8c:1f:dc:5e:68:65:24:
                    42:6a:51:21:69:87:b2:63:d8:dc:5d:c5:df:bf:cf:
                    b3:59:7b:88:c5:4e:b2:a5:2c:8d:f6:a7:45:3f:b4:
                    d2:5f:b7:15:72:e0:d1:c1:b4:4f:68:23:08:48:a5:
                    13:e9:d5:7f:21:59:c3:50:a9:09:ea:44:c2:a3:91:
                    3f:78:89:05:b0:35:5b:ee:d0:42:6e:a3:43:d9:39:
                    72:0f:a8:de:e4:83:31:73:37:d7:17:af:0c:ca:49:
                    cc:3f:2d:66:28:66:22:4a:b1:e3:20:b4:fc:67:d9:
                    b1:bb:d2:f5:66:cb:d2:55:df:4e:4b:63:ed:6b:9c:
                    db:ac:82:18:d7:76:f0:8f:20:05:79:2e:01:4c:01:
                    c0:23:54:af:e3:ee:31:ef:d1:a3:fc:69:a2:f2:5c:
                    3d:d9:58:3e:e2:27:93:34:68:04:8b:07:3c:9a:bb:
                    16:3c:26:ff:8a:61:1c:7b:b6:1e:e6:43:f7:3b:bd:
                    f5:e0:ce:c1:32:8d:f5:08:58:37:57:10:b4:d4:01:
                    ed:f7:c4:ef:f1:08:6d:d7:f3:9a:62:37:6a:e8:24:
                    60:e3:20:37:34:4c:04:24:d3:46:a2:2b:10:ea:8b:
                    9f:be:8f:e5:34:b7:ec:36:68:64:ca:92:f3:c5:15:
                    2a:f0:72:fa:23:85:65:7c:61:95:89:f0:07:a2:09:
                    4b:a9:a6:b6:04:bb:f9:1e:79:b2:ef:8c:65:47:cc:
                    bf:09:86:5a:64:64:f9:33:86:24:a3:da:39:7a:b6:
                    db:e6:13:ae:c3:c2:04:d9:02:ea:56:0b:52:02:3f:
                    25:f0:7f:d2:0b:31:1e:63:e5:eb:9a:cf:ac:97:ae:
                    8e:7a:10:e5:42:c8:c1:9b:0c:6e:34:ab:54:54:b6:
                    8e:f8:03:ed:95:bf:c0:3d:c2:ce:99:4f:96:43:d6:
                    48:71:25:bd:b9:47:d1:af:5d:c9:74:f8:b6:25:16:
                    c0:dd:91:86:20:5c:75:81:7e:df:31:e9:86:2a:f1:
                    96:10:37:88:d7:12:9f:ca:a4:f1:81:af:64:9a:c2:
                    a9:9c:9f
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Subject Key Identifier:
                C8:1F:D9:46:B3:B2:25:9C:BE:38:3C:B9:94:B4:31:86:AE:40:2A:35
            X509v3 Authority Key Identifier:
                C8:1F:D9:46:B3:B2:25:9C:BE:38:3C:B9:94:B4:31:86:AE:40:2A:35
            X509v3 Basic Constraints: critical
                CA:TRUE
    Signature Algorithm: sha256WithRSAEncryption
    Signature Value:
        04:ec:02:e4:c7:d2:31:49:5b:9c:c7:38:e2:2a:e7:d4:29:95:
        b9:73:55:ae:f4:f0:cd:91:a4:5c:6d:51:e7:8c:b0:7d:5f:d0:
        f3:11:aa:17:b7:7d:dc:13:ca:a7:50:c6:a9:29:e9:40:df:f5:
        65:c0:da:cb:9a:1e:88:43:61:ba:0a:ca:38:cb:70:e8:5a:b1:
        c5:2e:f6:96:e6:28:51:bd:21:17:8f:a7:ef:fb:76:9c:50:b7:
        3c:6b:01:71:ee:59:2c:54:af:bc:31:05:81:6a:21:de:33:67:
        49:36:f2:00:11:7f:64:0a:7f:b2:4c:b9:de:2a:f2:31:af:a0:
        64:d2:47:29:1d:39:5c:d9:e1:4f:bb:df:c1:6e:f9:27:10:cb:
        8c:0f:1d:df:4f:78:59:29:1a:86:ad:f1:8d:4e:a3:12:cb:23:
        0c:19:14:ef:32:63:e7:bd:2f:62:50:51:57:9c:9e:29:be:92:
        5a:c2:26:c6:ea:09:67:09:8b:f7:3a:5c:97:5c:27:9c:5d:e8:
        8c:cf:9b:69:68:7c:69:0b:03:72:86:70:9c:21:88:f0:1d:00:
        0a:53:da:ac:71:bc:ee:0d:49:7f:c4:a0:a6:1a:da:2c:f9:d4:
        73:c7:5b:ca:89:b1:09:1f:f5:78:6a:08:a7:4e:52:b9:2e:62:
        06:f1:1b:9f:61:03:b1:dc:f2:4d:5f:f5:9f:34:4e:6a:d0:9a:
        12:85:2e:d3:c3:b7:60:0e:f9:58:6e:5b:92:41:25:4e:fa:60:
        61:ad:84:37:b5:9d:9a:97:bc:9b:2d:c0:2f:ad:53:9d:bc:bd:
        5e:fb:00:b6:bd:e3:d8:a8:e1:6f:6e:ce:c4:a1:35:67:37:96:
        9f:07:e6:3a:7d:65:1c:a2:36:d1:93:4c:4b:d4:f5:53:ae:03:
        87:91:d7:14:e1:33:0b:ca:5a:5c:4b:01:c2:3c:ec:79:d4:43:
        ee:a0:54:dd:9c:28:aa:88:7e:f5:bc:76:b2:eb:73:8f:a5:ea:
        12:00:a6:64:96:b2:37:35:48:a0:ba:25:91:29:f8:4d:f0:3a:
        78:68:ac:19:88:f5:34:d3:08:f5:83:30:98:1b:8d:4a:ef:81:
        38:15:b9:a8:a1:b5:95:cf:fc:2b:70:70:fc:fa:69:f6:e0:d9:
        a3:4c:0a:d0:12:49:04:fa:5b:be:b7:e3:a2:77:a5:de:18:85:
        26:30:99:82:0d:81:2f:3f:53:9e:88:f5:1d:cb:30:14:f3:42:
        86:7b:21:49:cc:0a:2d:a9:9d:bd:6e:fb:d8:36:df:92:7e:27:
        16:72:5f:a1:03:33:a9:11:cd:ee:98:44:e0:fb:b1:ee:1b:80:
        d3:fd:93:b7:23:08:be:07
-----BEGIN CERTIFICATE-----
MIIFezCCA2OgAwIBAgIUKykML7BSOnmJH4IRB72dhCoj1RwwDQYJKoZIhvcNAQEL
BQAwTTELMAkGA1UEBhMCVUsxDzANBgNVBAgMBkxvbmRvbjEPMA0GA1UEBwwGTG9u
ZG9uMRwwGgYDVQQKDBNEZWZhdWx0IENvbXBhbnkgTHRkMB4XDTIyMDgxMTExMzQx
OVoXDTM5MDIyNTExMzQxOVowTTELMAkGA1UEBhMCVUsxDzANBgNVBAgMBkxvbmRv
bjEPMA0GA1UEBwwGTG9uZG9uMRwwGgYDVQQKDBNEZWZhdWx0IENvbXBhbnkgTHRk
MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAspITV1pvNOLh8ghVrqnN
2sjpa7/9XDZt096BU2Dpiuz2hBpzMRpzz0diSmFOm2MNznx0O57R3O+QHt4b+4lc
A/JXWErW0dCl600fyNfHEeA4w8MgXO8jCXH3VGh41zWABxiDSs7Ggl0clvarEWeG
Xowf3F5oZSRCalEhaYeyY9jcXcXfv8+zWXuIxU6ypSyN9qdFP7TSX7cVcuDRwbRP
aCMISKUT6dV/IVnDUKkJ6kTCo5E/eIkFsDVb7tBCbqND2TlyD6je5IMxczfXF68M
yknMPy1mKGYiSrHjILT8Z9mxu9L1ZsvSVd9OS2Pta5zbrIIY13bwjyAFeS4BTAHA
I1Sv4+4x79Gj/Gmi8lw92Vg+4ieTNGgEiwc8mrsWPCb/imEce7Ye5kP3O7314M7B
Mo31CFg3VxC01AHt98Tv8Qht1/OaYjdq6CRg4yA3NEwEJNNGoisQ6oufvo/lNLfs
NmhkypLzxRUq8HL6I4VlfGGVifAHoglLqaa2BLv5Hnmy74xlR8y/CYZaZGT5M4Yk
o9o5erbb5hOuw8IE2QLqVgtSAj8l8H/SCzEeY+Xrms+sl66OehDlQsjBmwxuNKtU
VLaO+APtlb/APcLOmU+WQ9ZIcSW9uUfRr13JdPi2JRbA3ZGGIFx1gX7fMemGKvGW
EDeI1xKfyqTxga9kmsKpnJ8CAwEAAaNTMFEwHQYDVR0OBBYEFMgf2UazsiWcvjg8
uZS0MYauQCo1MB8GA1UdIwQYMBaAFMgf2UazsiWcvjg8uZS0MYauQCo1MA8GA1Ud
EwEB/wQFMAMBAf8wDQYJKoZIhvcNAQELBQADggIBAATsAuTH0jFJW5zHOOIq59Qp
lblzVa708M2RpFxtUeeMsH1f0PMRqhe3fdwTyqdQxqkp6UDf9WXA2suaHohDYboK
yjjLcOhascUu9pbmKFG9IRePp+/7dpxQtzxrAXHuWSxUr7wxBYFqId4zZ0k28gAR
f2QKf7JMud4q8jGvoGTSRykdOVzZ4U+738Fu+ScQy4wPHd9PeFkpGoat8Y1OoxLL
IwwZFO8yY+e9L2JQUVecnim+klrCJsbqCWcJi/c6XJdcJ5xd6IzPm2lofGkLA3KG
cJwhiPAdAApT2qxxvO4NSX/EoKYa2iz51HPHW8qJsQkf9XhqCKdOUrkuYgbxG59h
A7Hc8k1f9Z80TmrQmhKFLtPDt2AO+VhuW5JBJU76YGGthDe1nZqXvJstwC+tU528
vV77ALa949io4W9uzsShNWc3lp8H5jp9ZRyiNtGTTEvU9VOuA4eR1xThMwvKWlxL
AcI87HnUQ+6gVN2cKKqIfvW8drLrc4+l6hIApmSWsjc1SKC6JZEp+E3wOnhorBmI
9TTTCPWDMJgbjUrvgTgVuaihtZXP/CtwcPz6afbg2aNMCtASSQT6W76346J3pd4Y
hSYwmYINgS8/U56I9R3LMBTzQoZ7IUnMCi2pnb1u+9g235J+JxZyX6EDM6kRze6Y
ROD7se4bgNP9k7cjCL4H
-----END CERTIFICATE-----
```

4096

### Till which year is this certificate valid?

2039

# Task 7 Authenticating with Passwords

Let’s see how cryptography can help increase password security. With PKI and SSL/TLS, we can communicate with any server and provide our login credentials while ensuring that no one can read our passwords as they move across the network. This is an example of protecting data in transit. Let’s explore how we can safeguard passwords as they are saved in a database, i.e., data at rest.

The least secure method would be to save the username and the password in a database. This way, any data breach would expose the users’ passwords. No effort is required beyond reading the database containing the passwords.

|Username|password|
|---|---|
|`alice`|`qwerty`|
|`bob`|`dragon`|
|`charlie`|`princess`|

The improved approach would be to save the username and a hashed version of the password in a database. This way, a data breach will expose the hashed versions of the passwords. Since a hash function is irreversible, the attacker needs to keep trying different passwords to find the one that would result in the same hash. The table below shows the MD5 sum of the passwords. (We chose MD5 just to keep the password field small for the example; otherwise, we would have used SHA256 or something more secure.)

|Username|Hash(Password)|
|---|---|
|`alice`|`d8578edf8458ce06fbc5bb76a58c5ca4`|
|`bob`|`8621ffdbc5698829397d97767ac13db3`|
|`charlie`|`8afa847f50a716e64932d995c8e7435a`|

The previous approach looks secure; however, the availability of rainbow tables has made this approach insecure. A **rainbow table** contains a list of passwords along with their hash value. Hence, the attacker only needs to look up the hash to recover the password. For example, it would be easy to look up `d8578edf8458ce06fbc5bb76a58c5ca4` to discover the original password of `alice`. Consequently, we need to find more secure approaches to save passwords securely; we can add salt. A **salt** is a random value we can append to the password before hashing it. An example is shown below.

|Username|Hash(Password + Salt)|Salt|
|---|---|---|
|`alice`|`8a43db01d06107fcad32f0bcfa651f2f`|`12742`|
|`bob`|`aab2b680e6a1cb43c79180b3d1a38beb`|`22861`|
|`charlie`|`3a40d108a068cdc8e7951b82d312129b`|`16056`|

The table above used `hash(password + salt)`; another approach would be to use `hash(hash(password) + salt)`. Note that we used a relatively small salt along with the MD5 hash function. We should switch to a (more) secure hash function and a large salt for better security if this were an actual setup.

Another improvement we can make before saving the password is to use a key derivation function such as PBKDF2 (Password-Based Key Derivation Function 2). PBKDF2 takes the password and the salt and submits it through a certain number of iterations, usually hundreds of thousands.

We recommend you check the [Password Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html) if you like to learn about other techniques related to password storage.

## Answer the questions below

### You were auditing a system when you discovered that the MD5 hash of the admin password is `3fc0a7acf087f549ac2b266baf94b8b1`. What is the original password?


qwerty123

# Task 8 Cryptography and Data - Example

In this task, we would like to explore what happens when we log into a website over HTTPS.

1. Client requests server’s SSL/TLS certificate
2. Server sends SSL/TLS certificate to the client
3. Client confirms that the certificate is valid

Cryptography’s role starts with checking the certificate. For a certificate to be considered valid, it means it is signed. Signing means that a hash of the certificate is encrypted with the private key of a trusted third party; the encrypted hash is appended to the certificate.

If the third party is trusted, the client will use the third party’s public key to decrypt the encrypted hash and compare it with the certificate’s hash. However, if the third party is not recognized, the connection will not proceed automatically.

Once the client confirms that the certificate is valid, an SSL/TLS handshake is started. This handshake allows the client and the server to agree on the secret key and the symmetric encryption algorithm, among other things. From this point onward, all the related session communication will be encrypted using symmetric encryption.

The final step would be to provide login credentials. The client uses the encrypted SSL/TLS session to send them to the server. The server receives the username and password and needs to confirm that they match.

Following security guidelines, we expect the server to save a hashed version of the password after appending a random salt to it. This way, if the database were breached, the passwords would be challenging to recover.

# Answer the questions below

Make sure you read and understand the above scenario. The purpose is to see how symmetric and asymmetric encryption are used along with hashing in many secure communications.

# Task 9Conclusion

Cryptography is a vast topic. In this room, we tried to focus on the core concepts that would help you understand the commonly used terms in cryptography. This knowledge is vital to understanding the configuration options of systems that use encryption and hashing.

# Answer the questions below

Make sure you have taken notes of all the concepts and commands covered in this room.