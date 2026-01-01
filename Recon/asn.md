

## Charla Jasson Jadix / Cyber Rush week

https://www.youtube.com/watch?v=SVfFpVig-nw&list=PLYyiZV6qZAcRNj6vwXIDzk7sXbKEr_36Y&index=1


### ASN numbers

- https://bgp.he.net/

### Dns Check

- https://dnschecker.org/all-dns-records-of-domain.php

### Revisar adqusisions


- https://asrank.caida.org/

### Autodisover Interrogator
https://github.com/expl0itabl3/check_mdi

```
──(root㉿kali)-[/opt]
└─# python3 check_mdi.py -d tesla.com 

[+] Domains found:
service.tesla.com
teslaalerts.com
c.tesla.com
ext.tesla.com
teslagrohmannautomation.de
solarcity.com
t.tesla.com
m.tesla.com
tesla.com
siilion.com
mta.tesla.com
TeslaMotorsInc.mail.onmicrosoft.com
tesla.services
teslamotors.com
perbix.com
TeslaMotorsInc.onmicrosoft.com

[+] Tenant found: 
TeslaMotorsInc

[+] An MDI instance was found for TeslaMotorsIncsensorapi.atp.azure.com!

```

### ASN Port Scan

- Para usar asnmap, me registre aqui para la api
https://cloud.projectdiscovery.io/


```
echo AS8151 | asnmap -silent | naabu -silent -nmap-cli 'nmap -sV'
```

### Pasive Port Scan

https://github.com/s0md3v/Smap


### Search for certs

https://github.com/g0ldencybersec/Caduceus

```shell
go install github.com/g0ldencybersec/Caduceus/cmd/caduceus@latest
```


```
┌──(kali㉿kali)-[~]
└─$ caduceus -i 189.195.30.67/24
msc.zacatecas.tecnm.mx
msc.zacatecas.tecnm.mx
utzac.edu.mx
utzac.edu.mx
pagos.zacatecas.tecnm.mx
pagos.zacatecas.tecnm.mx
clouditz.itz.edu.mx
clouditz.itz.edu.mx
tecnm.mx
syscom.zacatecas.tecnm.mx
syscom.zacatecas.tecnm.mx
enlinea.zacatecas.tecnm.mx
enlinea.zacatecas.tecnm.mx
lakeland-ind.com

```

#### de rebote
pagos.zacatecas.tecnm.mx


## Efficient Bug Bounty Automation Techniques, Gunnar Andrews | Bug Bounty Village, DEF CON 32
https://www.youtube.com/watch?v=yQQ92XAWfGY





