
## ver que ha detrras de cloudfare o al menos intentarlo

### 0) Ver qué dice DNS hoy

`dig +short is.inscripciones-uaie.mx A`

- **Si NO sale `148.217.50.23`**, entonces esa IP no es la que usa el dominio en producción.

### 1) Petición normal (DNS real) + encabezados

`curl -kIsS https://is.inscripciones-uaie.mx/ -D -`

Mira el `HTTP/… <código>`, `Server:`, `Location:`, `Content-Type:`.

### 2) Forzar esa IP con SNI correcto (lo que ya hiciste, pero con más datos)

`curl -ksS https://is.inscripciones-uaie.mx/ \   --resolve is.inscripciones-uaie.mx:443:148.217.50.23 \   -o /dev/null -D - \   -w 'code=%{http_code} ip=%{remote_ip} tls=%{ssl_version} alpn=%{proto}\n'`

- Si aquí ves **“It works!!!”** (o `200` con `Server` genérico), el _virtual host_ de ese servidor probablemente **no** está configurado para `is.inscripciones-uaie.mx`.
    
### 3) Probar la IP directa (SNI = IP)

`curl -kIsS https://148.217.50.23/ -D -`

- Si esto **igual** devuelve la página genérica, refuerza que la IP sirve un “default site”.

### 4) Comparar **SNI correcto vs SNI incorrecto**

> (SNI = nombre que se manda en TLS; puede cambiar la respuesta aunque el Host HTTP sea el mismo)
- **SNI correcto** (se toma del host de la URL y lo fija `--resolve`):
`curl -vk https://is.inscripciones-uaie.mx/ \   --resolve is.inscripciones-uaie.mx:443:148.217.50.23 \   -o /dev/null`

- **SNI incorrecto** (SNI será la IP):
`curl -vk https://148.217.50.23/ \   -H 'Host: is.inscripciones-uaie.mx' \   -o /dev/null`

Compara las líneas de `* TLSv1.3 ...` y `* ALPN, server accepted ...` y si cambia el certificado presentado.

### 5) Ver el certificado que presenta esa IP para ese host (openssl)

`openssl s_client -connect 148.217.50.23:443 -servername is.inscripciones-uaie.mx < /dev/null 2>/dev/null \ | openssl x509 -noout -subject -issuer -dates -ext subjectAltName`

- Revisa que en `subjectAltName` aparezca `DNS:is.inscripciones-uaie.mx`.
- Si no aparece, el cert **no** corresponde a ese FQDN.

### 6) One-liner para “radiografía” completa

`host=is.inscripciones-uaie.mx; ip=148.217.50.23 echo "DNS actual:"; dig +short $host A echo -e "\nNormal (DNS):"; curl -kIsS https://$host/ -D - echo -e "\nForzado a $ip (SNI correcto):" curl -ksS https://$host/ --resolve $host:443:$ip -o /dev/null -D - \   -w 'code=%{http_code} ip=%{remote_ip} tls=%{ssl_version} alpn=%{proto}\n' echo -e "\nIP directa (SNI=IP):"; curl -kIsS https://$ip/ -D - echo -e "\nCertificado que presenta $ip para $host:"; \ openssl s_client -connect $ip:443 -servername $host < /dev/null 2>/dev/null \ | openssl x509 -noout -subject -issuer -dates -ext subjectAltName`

## ¿Cómo interpretar rápidamente?

- **DNS ≠ 148.217.50.23:** Estás apuntando a otra máquina distinta a producción.
- **Forzado (2) muestra “It works!!!” o 200 con server genérico:** En `148.217.50.23` no está mapeado el vhost `is.inscripciones-uaie.mx` (o la app no está desplegada ahí).
- **IP directa (3) = misma página genérica:** El “default site” es lo único activo en esa IP.
- **Certificado (5) sin SAN para el FQDN:** El TLS no está preparado para ese dominio en esa IP (mala config de SNI/cert).

## Algo aplicado

```
dig +short is.inscripciones-uaie.mx A

104.21.2.152
172.67.129.86

```


```
curl -kIsS https://is.inscripciones-uaie.mx/ -D -

HTTP/2 403 
HTTP/2 403 
date: Wed, 13 Aug 2025 23:27:34 GMT
date: Wed, 13 Aug 2025 23:27:34 GMT
content-type: text/html; charset=UTF-8
content-type: text/html; charset=UTF-8
accept-ch: Sec-CH-UA-Bitness, Sec-CH-UA-Arch, Sec-CH-UA-Full-Version, Sec-CH-UA-Mobile, Sec-CH-UA-Model, Sec-CH-UA-Platform-Version, Sec-CH-UA-Full-Version-List, Sec-CH-UA-Platform, Sec-CH-UA, UA-Bitness, UA-Arch, UA-Full-Version, UA-Mobile, UA-Model, UA-Platform-Version, UA-Platform, UA
accept-ch: Sec-CH-UA-Bitness, Sec-CH-UA-Arch, Sec-CH-UA-Full-Version, Sec-CH-UA-Mobile, Sec-CH-UA-Model, Sec-CH-UA-Platform-Version, Sec-CH-UA-Full-Version-List, Sec-CH-UA-Platform, Sec-CH-UA, UA-Bitness, UA-Arch, UA-Full-Version, UA-Mobile, UA-Model, UA-Platform-Version, UA-Platform, UA
cf-mitigated: challenge
cf-mitigated: challenge
critical-ch: Sec-CH-UA-Bitness, Sec-CH-UA-Arch, Sec-CH-UA-Full-Version, Sec-CH-UA-Mobile, Sec-CH-UA-Model, Sec-CH-UA-Platform-Version, Sec-CH-UA-Full-Version-List, Sec-CH-UA-Platform, Sec-CH-UA, UA-Bitness, UA-Arch, UA-Full-Version, UA-Mobile, UA-Model, UA-Platform-Version, UA-Platform, UA
critical-ch: Sec-CH-UA-Bitness, Sec-CH-UA-Arch, Sec-CH-UA-Full-Version, Sec-CH-UA-Mobile, Sec-CH-UA-Model, Sec-CH-UA-Platform-Version, Sec-CH-UA-Full-Version-List, Sec-CH-UA-Platform, Sec-CH-UA, UA-Bitness, UA-Arch, UA-Full-Version, UA-Mobile, UA-Model, UA-Platform-Version, UA-Platform, UA
cross-origin-embedder-policy: require-corp
cross-origin-embedder-policy: require-corp
cross-origin-opener-policy: same-origin
cross-origin-opener-policy: same-origin
cross-origin-resource-policy: same-origin
cross-origin-resource-policy: same-origin
origin-agent-cluster: ?1
origin-agent-cluster: ?1
permissions-policy: accelerometer=(),autoplay=(),browsing-topics=(),camera=(),clipboard-read=(),clipboard-write=(),geolocation=(),gyroscope=(),hid=(),interest-cohort=(),magnetometer=(),microphone=(),payment=(),publickey-credentials-get=(),screen-wake-lock=(),serial=(),sync-xhr=(),usb=()
permissions-policy: accelerometer=(),autoplay=(),browsing-topics=(),camera=(),clipboard-read=(),clipboard-write=(),geolocation=(),gyroscope=(),hid=(),interest-cohort=(),magnetometer=(),microphone=(),payment=(),publickey-credentials-get=(),screen-wake-lock=(),serial=(),sync-xhr=(),usb=()
referrer-policy: same-origin
referrer-policy: same-origin
server-timing: chlray;desc="96ebfbe119a57694"
server-timing: chlray;desc="96ebfbe119a57694"
x-content-type-options: nosniff
x-content-type-options: nosniff
x-frame-options: SAMEORIGIN
x-frame-options: SAMEORIGIN
x-frame-options: SAMEORIGIN
x-frame-options: SAMEORIGIN
cache-control: private, max-age=0, no-store, no-cache, must-revalidate, post-check=0, pre-check=0
cache-control: private, max-age=0, no-store, no-cache, must-revalidate, post-check=0, pre-check=0
expires: Thu, 01 Jan 1970 00:00:01 GMT
expires: Thu, 01 Jan 1970 00:00:01 GMT
report-to: {"group":"cf-nel","max_age":604800,"endpoints":[{"url":"https://a.nel.cloudflare.com/report/v4?s=xrwNAIWgNwOFluyNklszcnKXc48AGXRvhctoDJzZpHE1u38nh%2Be56tsIb8nKMY9X0LmLfekqHCpz9BLN1Uz4WNg6y36mTYiYuG5LOCcaZ%2FV4HeQTwFA9Qw%3D%3D"}]}
report-to: {"group":"cf-nel","max_age":604800,"endpoints":[{"url":"https://a.nel.cloudflare.com/report/v4?s=xrwNAIWgNwOFluyNklszcnKXc48AGXRvhctoDJzZpHE1u38nh%2Be56tsIb8nKMY9X0LmLfekqHCpz9BLN1Uz4WNg6y36mTYiYuG5LOCcaZ%2FV4HeQTwFA9Qw%3D%3D"}]}
nel: {"report_to":"cf-nel","success_fraction":0.0,"max_age":604800}
nel: {"report_to":"cf-nel","success_fraction":0.0,"max_age":604800}
server: cloudflare
server: cloudflare
cf-ray: 96ebfbe119a57694-SEA
cf-ray: 96ebfbe119a57694-SEA
alt-svc: h3=":443"; ma=86400
alt-svc: h3=":443"; ma=86400

```

```
curl -ksS https://is.inscripciones-uaie.mx/ \
  --resolve is.inscripciones-uaie.mx:443:148.217.50.23 \
  -o /dev/null -D - \
  -w 'code=%{http_code} ip=%{remote_ip} tls=%{ssl_version} alpn=%{proto}\n'

HTTP/1.1 200 OK
Date: Wed, 13 Aug 2025 20:43:23 GMT
Server: Apache/2.4.10 (Debian)
Content-Length: 21
Content-Type: text/html; charset=UTF-8

curl: unknown --write-out variable: 'ssl_version'
curl: unknown --write-out variable: 'proto'
code=200 ip=148.217.50.23 tls= alpn=

```





## Todo
```
host=is.inscripciones-uaie.mx; ip=148.217.50.23
echo "DNS actual:"; dig +short $host A
echo -e "\nNormal (DNS):"; curl -kIsS https://$host/ -D -
echo -e "\nForzado a $ip (SNI correcto):"
curl -ksS https://$host/ --resolve $host:443:$ip -o /dev/null -D - \
  -w 'code=%{http_code} ip=%{remote_ip} tls=%{ssl_version} alpn=%{proto}\n'
echo -e "\nIP directa (SNI=IP):"; curl -kIsS https://$ip/ -D -
echo -e "\nCertificado que presenta $ip para $host:"; \
openssl s_client -connect $ip:443 -servername $host < /dev/null 2>/dev/null \
| openssl x509 -noout -subject -issuer -dates -ext subjectAltName


```