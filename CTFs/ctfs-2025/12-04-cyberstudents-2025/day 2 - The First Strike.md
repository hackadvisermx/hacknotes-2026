
# The First Strike

## Description

A series of repeated authentication failures was detected against the **FTP** service. The traffic pattern matched known Krampus Syndicate infrastructure, indicating the beginning of their intrusion attempts. After a sustained burst of password guessing, one request finally succeeded.

Your task is to examine the logs or packet capture, identify which account was **compromised**, and determine the password used during the successful login.

Submit your answer as: `csd{username_password}`

## Solve

- Abrir el .pcab y buscar : User logged in o successful

```
220 Microsoft FTP Service

USER Elf67

331 Password required

PASS snowball

230 User logged in.

OPTS utf8 on

200 OPTS UTF8 command successful - UTF8 encoding now ON.

PWD

257 "/" is current directory.

TYPE I

200 Type set to I.

PASV

227 Entering Passive Mode (192,168,253,245,192,211).

NLST

125 Data connection already open; Transfer starting.
226 Transfer complete.

QUIT

221 Goodbye.

```

csd{Elf67_snowball}