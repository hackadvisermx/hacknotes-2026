# Syndicate Infrastructure

Category: Miscellaneous

## Description

⚠️ Bruteforcing subdomains is not required and will result in disqualification. Follow the records.

Our monitoring systems have flagged suspicious DNS activity originating from a domain registered by the **KRAMPUS SYNDICATE**. Initial analysis suggests they're using it to coordinate operations against crucial North Pole systems.

The domain in question: `krampus.csd.lol`

We need you to perform a full DNS reconnaissance sweep. The Syndicate thinks they're clever, hiding their infrastructure in plain sight but they're wrong.

Map their infrastructure. Find what they're hiding. Report back before they realize we're onto them.

_- NPLD Threat Intelligence Division_

---

Note: All the information you need is in the DNS records. Dig deep.

## Solve

### 1
```
# Basic DNS queries to try:
# 1. Standard record types
dig krampus.csd.lol ANY
dig krampus.csd.lol A
dig krampus.csd.lol AAAA
dig krampus.csd.lol TXT
dig krampus.csd.lol MX
dig krampus.csd.lol NS
dig krampus.csd.lol CNAME

# 2. Zone transfer attempt
dig axfr @ns1.csd.lol krampus.csd.lol
dig axfr @ns2.csd.lol krampus.csd.lol

# 3. Reverse DNS lookups if we find IPs

; <<>> DiG 9.10.6 <<>> krampus.csd.lol ANY
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 33592
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;krampus.csd.lol.		IN	ANY

;; Query time: 48 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:26:24 CST 2025
;; MSG SIZE  rcvd: 44


; <<>> DiG 9.10.6 <<>> krampus.csd.lol A
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 24677
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;krampus.csd.lol.		IN	A

;; Query time: 14 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:26:24 CST 2025
;; MSG SIZE  rcvd: 44


; <<>> DiG 9.10.6 <<>> krampus.csd.lol AAAA
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 63601
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;krampus.csd.lol.		IN	AAAA

;; Query time: 14 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:26:24 CST 2025
;; MSG SIZE  rcvd: 44


; <<>> DiG 9.10.6 <<>> krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 638
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;krampus.csd.lol.		IN	TXT

;; ANSWER SECTION:
krampus.csd.lol.	264	IN	TXT	"v=spf1 include:_spf.krampus.csd.lol -all"

;; Query time: 44 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:26:24 CST 2025
;; MSG SIZE  rcvd: 97


; <<>> DiG 9.10.6 <<>> krampus.csd.lol MX
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 49129
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;krampus.csd.lol.		IN	MX

;; ANSWER SECTION:
krampus.csd.lol.	284	IN	MX	10 mail.krampus.csd.lol.

;; Query time: 44 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:26:24 CST 2025
;; MSG SIZE  rcvd: 65


; <<>> DiG 9.10.6 <<>> krampus.csd.lol NS
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 17542
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;krampus.csd.lol.		IN	NS

;; AUTHORITY SECTION:
csd.lol.		1784	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 47 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:26:24 CST 2025
;; MSG SIZE  rcvd: 109


; <<>> DiG 9.10.6 <<>> krampus.csd.lol CNAME
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16648
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;krampus.csd.lol.		IN	CNAME

;; AUTHORITY SECTION:
csd.lol.		1784	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 44 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:26:24 CST 2025
;; MSG SIZE  rcvd: 109

dig: couldn't get address for 'ns1.csd.lol': not found
dig: couldn't get address for 'ns2.csd.lol': not found
```

### 2
```
 # Follow the SPF record
dig _spf.krampus.csd.lol TXT
dig _spf.krampus.csd.lol ANY

# Check the mail subdomain
dig mail.krampus.csd.lol A
dig mail.krampus.csd.lol TXT
dig mail.krampus.csd.lol ANY

# Also try common DNS record types on the subdomains
dig _spf.krampus.csd.lol A
dig _spf.krampus.csd.lol CNAME

# Try other common subdomains that might be in DNS
dig _dmarc.krampus.csd.lol TXT
dig _domainkey.krampus.csd.lol TXT

# Try zone transfer with Cloudflare nameservers
dig axfr krampus.csd.lol @harmony.ns.cloudflare.com
dig axfr krampus.csd.lol @dns.cloudflare.com

# Check for other DNS security records
dig krampus.csd.lol CAA
dig krampus.csd.lol DNSKEY
dig krampus.csd.lol DS

; <<>> DiG 9.10.6 <<>> _spf.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 41650
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;_spf.krampus.csd.lol.		IN	TXT

;; ANSWER SECTION:
_spf.krampus.csd.lol.	300	IN	TXT	"v=spf1 ip4:203.0.113.0/24 ~all"

;; Query time: 69 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:29:45 CST 2025
;; MSG SIZE  rcvd: 92


; <<>> DiG 9.10.6 <<>> _spf.krampus.csd.lol ANY
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 24964
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;_spf.krampus.csd.lol.		IN	ANY

;; Query time: 48 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:29:45 CST 2025
;; MSG SIZE  rcvd: 49


; <<>> DiG 9.10.6 <<>> mail.krampus.csd.lol A
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 49773
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;mail.krampus.csd.lol.		IN	A

;; ANSWER SECTION:
mail.krampus.csd.lol.	300	IN	A	127.0.0.1

;; Query time: 73 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:29:45 CST 2025
;; MSG SIZE  rcvd: 65


; <<>> DiG 9.10.6 <<>> mail.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 49530
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;mail.krampus.csd.lol.		IN	TXT

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 64 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:29:45 CST 2025
;; MSG SIZE  rcvd: 114


; <<>> DiG 9.10.6 <<>> mail.krampus.csd.lol ANY
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 37917
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;mail.krampus.csd.lol.		IN	ANY

;; Query time: 47 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:29:45 CST 2025
;; MSG SIZE  rcvd: 49


; <<>> DiG 9.10.6 <<>> _spf.krampus.csd.lol A
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 50898
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;_spf.krampus.csd.lol.		IN	A

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 67 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:29:45 CST 2025
;; MSG SIZE  rcvd: 114


; <<>> DiG 9.10.6 <<>> _spf.krampus.csd.lol CNAME
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 38265
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;_spf.krampus.csd.lol.		IN	CNAME

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 65 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:29:45 CST 2025
;; MSG SIZE  rcvd: 114


; <<>> DiG 9.10.6 <<>> _dmarc.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 53590
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;_dmarc.krampus.csd.lol.		IN	TXT

;; ANSWER SECTION:
_dmarc.krampus.csd.lol.	300	IN	TXT	"v=DMARC1; p=reject; rua=mailto:dmarc@krampus.csd.lol; ruf=mailto:forensics@ops.krampus.csd.lol; fo=1; adkim=s; aspf=s"

;; Query time: 66 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:29:45 CST 2025
;; MSG SIZE  rcvd: 181


; <<>> DiG 9.10.6 <<>> _domainkey.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 150
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;_domainkey.krampus.csd.lol.	IN	TXT

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 67 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:29:45 CST 2025
;; MSG SIZE  rcvd: 120


; <<>> DiG 9.10.6 <<>> axfr krampus.csd.lol @harmony.ns.cloudflare.com
;; global options: +cmd
; Transfer failed.
;; Connection to 172.64.41.8#53(172.64.41.8) for krampus.csd.lol failed: timed out.
;; Connection to 172.64.41.8#53(172.64.41.8) for krampus.csd.lol failed: timed out.

; <<>> DiG 9.10.6 <<>> axfr krampus.csd.lol @dns.cloudflare.com
;; global options: +cmd
;; connection timed out; no servers could be reached
;; Connection to 172.64.41.8#53(172.64.41.8) for krampus.csd.lol failed: timed out.

; <<>> DiG 9.10.6 <<>> krampus.csd.lol CAA
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 50678
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;krampus.csd.lol.		IN	CAA

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 78 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:30:24 CST 2025
;; MSG SIZE  rcvd: 109


; <<>> DiG 9.10.6 <<>> krampus.csd.lol DNSKEY
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 23357
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;krampus.csd.lol.		IN	DNSKEY

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 77 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:30:25 CST 2025
;; MSG SIZE  rcvd: 109


; <<>> DiG 9.10.6 <<>> krampus.csd.lol DS
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 46052
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;krampus.csd.lol.		IN	DS

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 81 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:30:25 CST 2025
;; MSG SIZE  rcvd: 109
```

### 3

```
 # Check the ops subdomain
dig ops.krampus.csd.lol A
dig ops.krampus.csd.lol TXT
dig ops.krampus.csd.lol ANY
dig ops.krampus.csd.lol MX
dig ops.krampus.csd.lol NS

# Check the forensics subdomain under ops
dig forensics.ops.krampus.csd.lol A
dig forensics.ops.krampus.csd.lol TXT
dig forensics.ops.krampus.csd.lol ANY

# Also check if there are more subdomains referenced
dig dmarc.krampus.csd.lol A
dig dmarc.krampus.csd.lol TXT

# Try some other common operational subdomains
dig api.krampus.csd.lol TXT
dig admin.krampus.csd.lol TXT
dig portal.krampus.csd.lol TXT

# Check for SRV records (service records)
dig _http._tcp.krampus.csd.lol SRV
dig _https._tcp.krampus.csd.lol SRV

; <<>> DiG 9.10.6 <<>> ops.krampus.csd.lol A
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 5454
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;ops.krampus.csd.lol.		IN	A

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 76 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:56 CST 2025
;; MSG SIZE  rcvd: 113


; <<>> DiG 9.10.6 <<>> ops.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 43054
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;ops.krampus.csd.lol.		IN	TXT

;; ANSWER SECTION:
ops.krampus.csd.lol.	300	IN	TXT	"internal-services: _ldap._tcp.krampus.csd.lol _kerberos._tcp.krampus.csd.lol _metrics._tcp.krampus.csd.lol"

;; Query time: 71 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:57 CST 2025
;; MSG SIZE  rcvd: 167


; <<>> DiG 9.10.6 <<>> ops.krampus.csd.lol ANY
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 23818
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;ops.krampus.csd.lol.		IN	ANY

;; Query time: 50 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:57 CST 2025
;; MSG SIZE  rcvd: 48


; <<>> DiG 9.10.6 <<>> ops.krampus.csd.lol MX
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 39561
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;ops.krampus.csd.lol.		IN	MX

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 71 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:57 CST 2025
;; MSG SIZE  rcvd: 113


; <<>> DiG 9.10.6 <<>> ops.krampus.csd.lol NS
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 7179
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;ops.krampus.csd.lol.		IN	NS

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 72 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:57 CST 2025
;; MSG SIZE  rcvd: 113


; <<>> DiG 9.10.6 <<>> forensics.ops.krampus.csd.lol A
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 13624
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;forensics.ops.krampus.csd.lol.	IN	A

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 80 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:57 CST 2025
;; MSG SIZE  rcvd: 123


; <<>> DiG 9.10.6 <<>> forensics.ops.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 6041
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;forensics.ops.krampus.csd.lol.	IN	TXT

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 47 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:57 CST 2025
;; MSG SIZE  rcvd: 123


; <<>> DiG 9.10.6 <<>> forensics.ops.krampus.csd.lol ANY
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 43499
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;forensics.ops.krampus.csd.lol.	IN	ANY

;; Query time: 49 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:57 CST 2025
;; MSG SIZE  rcvd: 58


; <<>> DiG 9.10.6 <<>> dmarc.krampus.csd.lol A
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 34335
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;dmarc.krampus.csd.lol.		IN	A

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 79 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:57 CST 2025
;; MSG SIZE  rcvd: 115


; <<>> DiG 9.10.6 <<>> dmarc.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 91
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;dmarc.krampus.csd.lol.		IN	TXT

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 48 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:57 CST 2025
;; MSG SIZE  rcvd: 115


; <<>> DiG 9.10.6 <<>> api.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 8653
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;api.krampus.csd.lol.		IN	TXT

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 76 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:57 CST 2025
;; MSG SIZE  rcvd: 113


; <<>> DiG 9.10.6 <<>> admin.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 50951
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;admin.krampus.csd.lol.		IN	TXT

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 66 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:57 CST 2025
;; MSG SIZE  rcvd: 115


; <<>> DiG 9.10.6 <<>> portal.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 60050
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;portal.krampus.csd.lol.		IN	TXT

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 77 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:57 CST 2025
;; MSG SIZE  rcvd: 116


; <<>> DiG 9.10.6 <<>> _http._tcp.krampus.csd.lol SRV
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 40669
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;_http._tcp.krampus.csd.lol.	IN	SRV

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 81 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:57 CST 2025
;; MSG SIZE  rcvd: 120


; <<>> DiG 9.10.6 <<>> _https._tcp.krampus.csd.lol SRV
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 42054
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;_https._tcp.krampus.csd.lol.	IN	SRV

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 80 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:32:58 CST 2025
;; MSG SIZE  rcvd: 121
```

### 4

```
# Query the internal services mentioned
dig _ldap._tcp.krampus.csd.lol SRV
dig _ldap._tcp.krampus.csd.lol TXT
dig _ldap._tcp.krampus.csd.lol ANY

dig _kerberos._tcp.krampus.csd.lol SRV
dig _kerberos._tcp.krampus.csd.lol TXT
dig _kerberos._tcp.krampus.csd.lol ANY

dig _metrics._tcp.krampus.csd.lol SRV
dig _metrics._tcp.krampus.csd.lol TXT
dig _metrics._tcp.krampus.csd.lol ANY

; <<>> DiG 9.10.6 <<>> _ldap._tcp.krampus.csd.lol SRV
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 4478
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;_ldap._tcp.krampus.csd.lol.	IN	SRV

;; ANSWER SECTION:
_ldap._tcp.krampus.csd.lol. 300	IN	SRV	0 0 389 dc01.krampus.csd.lol.

;; Query time: 79 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:33:44 CST 2025
;; MSG SIZE  rcvd: 95


; <<>> DiG 9.10.6 <<>> _ldap._tcp.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 56459
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;_ldap._tcp.krampus.csd.lol.	IN	TXT

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 76 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:33:44 CST 2025
;; MSG SIZE  rcvd: 120


; <<>> DiG 9.10.6 <<>> _ldap._tcp.krampus.csd.lol ANY
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 12906
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;_ldap._tcp.krampus.csd.lol.	IN	ANY

;; ANSWER SECTION:
_ldap._tcp.krampus.csd.lol. 300	IN	SRV	0 0 389 dc01.krampus.csd.lol.

;; Query time: 24 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:33:44 CST 2025
;; MSG SIZE  rcvd: 95


; <<>> DiG 9.10.6 <<>> _kerberos._tcp.krampus.csd.lol SRV
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 14816
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;_kerberos._tcp.krampus.csd.lol.	IN	SRV

;; ANSWER SECTION:
_kerberos._tcp.krampus.csd.lol.	300 IN	SRV	0 0 88 dc01.krampus.csd.lol.

;; Query time: 76 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:33:45 CST 2025
;; MSG SIZE  rcvd: 99


; <<>> DiG 9.10.6 <<>> _kerberos._tcp.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 54693
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;_kerberos._tcp.krampus.csd.lol.	IN	TXT

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 75 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:33:45 CST 2025
;; MSG SIZE  rcvd: 124


; <<>> DiG 9.10.6 <<>> _kerberos._tcp.krampus.csd.lol ANY
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 63609
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;_kerberos._tcp.krampus.csd.lol.	IN	ANY

;; ANSWER SECTION:
_kerberos._tcp.krampus.csd.lol.	300 IN	SRV	0 0 88 dc01.krampus.csd.lol.

;; Query time: 21 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:33:45 CST 2025
;; MSG SIZE  rcvd: 99


; <<>> DiG 9.10.6 <<>> _metrics._tcp.krampus.csd.lol SRV
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 27545
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;_metrics._tcp.krampus.csd.lol.	IN	SRV

;; ANSWER SECTION:
_metrics._tcp.krampus.csd.lol. 300 IN	SRV	0 0 443 beacon.krampus.csd.lol.

;; Query time: 79 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:33:45 CST 2025
;; MSG SIZE  rcvd: 100


; <<>> DiG 9.10.6 <<>> _metrics._tcp.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 45298
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;_metrics._tcp.krampus.csd.lol.	IN	TXT

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 75 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:33:45 CST 2025
;; MSG SIZE  rcvd: 123


; <<>> DiG 9.10.6 <<>> _metrics._tcp.krampus.csd.lol ANY
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 8961
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;_metrics._tcp.krampus.csd.lol.	IN	ANY

;; ANSWER SECTION:
_metrics._tcp.krampus.csd.lol. 299 IN	SRV	0 0 443 beacon.krampus.csd.lol.

;; Query time: 22 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:33:45 CST 2025
;; MSG SIZE  rcvd: 100

```

### 5
```
# Check dc01 subdomain
dig dc01.krampus.csd.lol A
dig dc01.krampus.csd.lol TXT
dig dc01.krampus.csd.lol ANY
dig dc01.krampus.csd.lol AAAA

# Check beacon subdomain
dig beacon.krampus.csd.lol A
dig beacon.krampus.csd.lol TXT
dig beacon.krampus.csd.lol ANY
dig beacon.krampus.csd.lol AAAA
dig beacon.krampus.csd.lol CNAME

; <<>> DiG 9.10.6 <<>> dc01.krampus.csd.lol A
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 13135
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;dc01.krampus.csd.lol.		IN	A

;; ANSWER SECTION:
dc01.krampus.csd.lol.	300	IN	A	203.0.113.1

;; Query time: 71 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:34:25 CST 2025
;; MSG SIZE  rcvd: 65


; <<>> DiG 9.10.6 <<>> dc01.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 51883
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;dc01.krampus.csd.lol.		IN	TXT

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 71 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:34:26 CST 2025
;; MSG SIZE  rcvd: 114


; <<>> DiG 9.10.6 <<>> dc01.krampus.csd.lol ANY
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 19595
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;dc01.krampus.csd.lol.		IN	ANY

;; Query time: 44 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:34:26 CST 2025
;; MSG SIZE  rcvd: 49


; <<>> DiG 9.10.6 <<>> dc01.krampus.csd.lol AAAA
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 41019
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;dc01.krampus.csd.lol.		IN	AAAA

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 72 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:34:26 CST 2025
;; MSG SIZE  rcvd: 114


; <<>> DiG 9.10.6 <<>> beacon.krampus.csd.lol A
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 27080
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;beacon.krampus.csd.lol.		IN	A

;; ANSWER SECTION:
beacon.krampus.csd.lol.	300	IN	A	203.0.113.2

;; Query time: 72 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:34:26 CST 2025
;; MSG SIZE  rcvd: 67


; <<>> DiG 9.10.6 <<>> beacon.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 55470
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;beacon.krampus.csd.lol.		IN	TXT

;; ANSWER SECTION:
beacon.krampus.csd.lol.	300	IN	TXT	"config=ZXhmaWwua3JhbXB1cy5jc2QubG9s=="

;; Query time: 69 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:34:26 CST 2025
;; MSG SIZE  rcvd: 101


; <<>> DiG 9.10.6 <<>> beacon.krampus.csd.lol ANY
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 30517
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;beacon.krampus.csd.lol.		IN	ANY

;; Query time: 44 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:34:26 CST 2025
;; MSG SIZE  rcvd: 51


; <<>> DiG 9.10.6 <<>> beacon.krampus.csd.lol AAAA
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 54170
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;beacon.krampus.csd.lol.		IN	AAAA

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 72 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:34:26 CST 2025
;; MSG SIZE  rcvd: 116


; <<>> DiG 9.10.6 <<>> beacon.krampus.csd.lol CNAME
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 17687
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;beacon.krampus.csd.lol.		IN	CNAME

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 72 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:34:26 CST 2025
;; MSG SIZE  rcvd: 116
```

### 6
```
# Check the exfil subdomain
dig exfil.krampus.csd.lol A
dig exfil.krampus.csd.lol TXT
dig exfil.krampus.csd.lol ANY
dig exfil.krampus.csd.lol AAAA
dig exfil.krampus.csd.lol CNAME
dig exfil.krampus.csd.lol MX

; <<>> DiG 9.10.6 <<>> exfil.krampus.csd.lol A
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 55634
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;exfil.krampus.csd.lol.		IN	A

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 77 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:35:52 CST 2025
;; MSG SIZE  rcvd: 115


; <<>> DiG 9.10.6 <<>> exfil.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 43987
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;exfil.krampus.csd.lol.		IN	TXT

;; ANSWER SECTION:
exfil.krampus.csd.lol.	300	IN	TXT	"status=active; auth=dkim; selector=syndicate"

;; Query time: 71 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:35:52 CST 2025
;; MSG SIZE  rcvd: 107


; <<>> DiG 9.10.6 <<>> exfil.krampus.csd.lol ANY
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 18432
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;exfil.krampus.csd.lol.		IN	ANY

;; Query time: 52 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:35:52 CST 2025
;; MSG SIZE  rcvd: 50


; <<>> DiG 9.10.6 <<>> exfil.krampus.csd.lol AAAA
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 36349
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;exfil.krampus.csd.lol.		IN	AAAA

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 70 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:35:53 CST 2025
;; MSG SIZE  rcvd: 115


; <<>> DiG 9.10.6 <<>> exfil.krampus.csd.lol CNAME
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 2722
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;exfil.krampus.csd.lol.		IN	CNAME

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 67 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:35:53 CST 2025
;; MSG SIZE  rcvd: 115


; <<>> DiG 9.10.6 <<>> exfil.krampus.csd.lol MX
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 24659
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;exfil.krampus.csd.lol.		IN	MX

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 72 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:35:53 CST 2025
;; MSG SIZE  rcvd: 115
```

### 7

```
# Query the DKIM record with the syndicate selector
dig syndicate._domainkey.krampus.csd.lol TXT
dig syndicate._domainkey.krampus.csd.lol ANY

# Also try it under exfil subdomain
dig syndicate._domainkey.exfil.krampus.csd.lol TXT

; <<>> DiG 9.10.6 <<>> syndicate._domainkey.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 8548
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;syndicate._domainkey.krampus.csd.lol. IN TXT

;; ANSWER SECTION:
syndicate._domainkey.krampus.csd.lol. 300 IN TXT "v=DKIM1; k=rsa; p=Y3Nke2RuNV9tMTlIVF9CM19LMU5ENF9XME5LeX0="

;; Query time: 76 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:36:51 CST 2025
;; MSG SIZE  rcvd: 136


; <<>> DiG 9.10.6 <<>> syndicate._domainkey.krampus.csd.lol ANY
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 40697
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;syndicate._domainkey.krampus.csd.lol. IN ANY

;; Query time: 51 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:36:51 CST 2025
;; MSG SIZE  rcvd: 65


; <<>> DiG 9.10.6 <<>> syndicate._domainkey.exfil.krampus.csd.lol TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 20289
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;syndicate._domainkey.exfil.krampus.csd.lol. IN TXT

;; AUTHORITY SECTION:
csd.lol.		1800	IN	SOA	harmony.ns.cloudflare.com. dns.cloudflare.com. 2390291443 10000 2400 604800 1800

;; Query time: 74 msec
;; SERVER: fe80::1%14#53(fe80::1%14)
;; WHEN: Wed Dec 03 20:36:51 CST 2025
;; MSG SIZE  rcvd: 136
```
### Sumary
**The flag is: `csd{dn5_m19HT_B3_K1ND4_W0NKy}`**

## Summary of the DNS Trail:

1. **krampus.csd.lol** → TXT record pointed to `_spf.krampus.csd.lol`
2. **krampus.csd.lol** → MX record pointed to `mail.krampus.csd.lol`
3. **_dmarc.krampus.csd.lol** → Revealed `ops.krampus.csd.lol`
4. **ops.krampus.csd.lol** → TXT revealed SRV records for internal services
5. **_metrics._tcp.krampus.csd.lol** → SRV pointed to `beacon.krampus.csd.lol`
6. **beacon.krampus.csd.lol** → TXT had Base64 that decoded to `exfil.krampus.csd.lol`
7. **exfil.krampus.csd.lol** → TXT revealed DKIM selector "syndicate"
8. **syndicate._domainkey.krampus.csd.lol** → TXT contained the Base64-encoded flag!

The flag format suggests: "DNS might be kinda wonky" 😄

**Flag: `csd{dn5_m19HT_B3_K1ND4_W0NKy}`**

