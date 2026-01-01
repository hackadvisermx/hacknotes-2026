
# Task 6 Osint  OSINT 2


## Intento real

- se cargaba un java scritp en : https://stage0.virelia-water.it.com/
- marcaba error al cargar el sitio , no cargaba el .js
- pero nos daba un nom,bre de dominio uplink que no resuelve pero si TXT

```
https://raw.githubusercontent.com/SanTzu/uplink-config/refs/heads/main/init.js

var beacon = {
  session_id: "O-TX-11-403",
  fallback_dns: "uplink-fallback.virelia-water.it.com",
  token: "JBSWY3DPEBLW64TMMQQQ=="
};

```

```
dig TXT uplink-fallback.virelia-water.it.com


; <<>> DiG 9.20.9-1-Debian <<>> TXT uplink-fallback.virelia-water.it.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 57284
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;uplink-fallback.virelia-water.it.com. IN TXT

;; ANSWER SECTION:
uplink-fallback.virelia-water.it.com. 1799 IN TXT "eyJzZXNzaW9uIjoiVC1DTjEtMTcyIiwiZmxhZyI6IlRITXt1cGxpbmtfY2hhbm5lbF9jb25maXJtZWR9In0="

;; Query time: 47 msec
;; SERVER: 192.168.100.1#53(192.168.100.1) (UDP)
;; WHEN: Fri Jun 27 21:36:32 CDT 2025
;; MSG SIZE  rcvd: 162



{"session":"T-CN1-172","flag":"THM{uplink_channel_confirmed}"}

```




## Estos intentos no me dieron la solución, aunque si algo de info

- examinando el dominio: stage0.virelia-water.it.com
- hacemos una busqueda en github

```
https://github.com/virelia-water/compliance

https://github.com/virelia-water/compliance/commit/bf80b28d73cdbbccaa37c34633de98cd00e7b236

-----BEGIN PGP SIGNATURE----- 
iQFQBAEBCgA6FiEEiN7ee3MFE71e3W2fpPD+sISjEeUFAmhZTEQcHGFsZXJ0c0B2
aXJlbGlhLXdhdGVyLml0LmNvbQAKCRCk8P6whKMR5ZIUCADM7F0WpKWWyj4WUdoL
6yrJfJfmUKgJD+8K1neFosG7yaz+MspYxIlbKUek/VFhHZnaG2NRjn6BpfPSxfEk
uvWNIP8rMVEv32vpqhCJ26pwrkAaUHlcPWqM4KYoAn4eEOeHCvxHNJBFnmWI5PBF
pXbj7s6DhyZEHUmTo4JK2OZmiISP3OsHW8O8iz5JLUrA/qw9LCjY8PK79UoceRwW
tJj9pVsE+TKPcFb/EDzqGmBH8GB1ki532/1/GDU+iivYSiRjxWks/ZYPu/bhktTo
NNcOzgEfuSekkQAz+CiclXwEcLQb219TqcS3plnaO672kCV4t5MUCLvkXL5/kHms
Sh5H
=jdL7
-----END PGP SIGNATURE-----

alerts@virelia-water.it.com


```

```

git log --all --graph -p


-<!DOCTYPE html>
-<html lang="en">
-<head>
-  <meta charset="UTF-8">
-  <meta name="robots" content="index,follow">
-  <title>OT Alerts Exceptions – June 2025</title>
-  <link rel="stylesheet" href="/styles.css">
-</head>
-<body>
-  <header><h1>OT Alerts Exception Report – June 2025</h1></header>
-  <nav>
-    <a href="/">Home</a>
-    <a href="/mail-archives/">Archives Home</a>
-    <a href="/policies/">Compliance Policies</a>
-  </nav>
-  <main>
-    <p>This page lists <em>exceptional</em> OT-Alert messages for June 2025 only. Routine alerts have been redacted.</p>
-    <div class="message">
-      <div class="hdr">
-        From: DarkPulse &lt;alerts@virelia-water.it.com&gt;<br>
-        Date: Mon, 15 Jun 2025 02:15:00 +0000<br>
-        Subject: Scheduled OT Calibration
-      </div>
-      <pre>
------BEGIN PGP SIGNED MESSAGE-----
-Hash: SHA512
 
-Please confirm system integrity at 03:00 UTC.
------BEGIN PGP SIGNATURE-----
-
-iQFQBAEBCgA6FiEEiN7ee3MFE71e3W2fpPD+sISjEeUFAmhZTEQcHGFsZXJ0c0B2
-aXJlbGlhLXdhdGVyLml0LmNvbQAKCRCk8P6whKMR5ZIUCADM7F0WpKWWyj4WUdoL
-6yrJfJfmUKgJD+8K1neFosG7yaz+MspYxIlbKUek/VFhHZnaG2NRjn6BpfPSxfEk
-uvWNIP8rMVEv32vpqhCJ26pwrkAaUHlcPWqM4KYoAn4eEOeHCvxHNJBFnmWI5PBF
-pXbj7s6DhyZEHUmTo4JK2OZmiISP3OsHW8O8iz5JLUrA/qw9LCjY8PK79UoceRwW
-tJj9pVsE+TKPcFb/EDzqGmBH8GB1ki532/1/GDU+iivYSiRjxWks/ZYPu/bhktTo
-NNcOzgEfuSekkQAz+CiclXwEcLQb219TqcS3plnaO672kCV4t5MUCLvkXL5/kHms
-Sh5H
-=jdL7
------END PGP SIGNATURE-----
-      </pre>
-    </div>
-  </main>
-  <footer>&copy; 2025 Virelia Water Control Facility</footer>
-</body>
-</html>

```


```
git log -p -S thm
```


```


https://raw.githubusercontent.com/SpeedieTest/uplink-config/refs/heads/main/init.js
https://raw.githubusercontent.com/SpeedieTest/uplink-config/refs/heads/main/init.js
```


- otros dominios en git

```

https://github.com/search?q=virelia-water&type=code



https://github.com/solstice-tech1/staging-panel/blob/main/index.html
https://github.com/FamilyBoggart/Ciber-CTFS

```