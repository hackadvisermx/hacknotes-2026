
# Como saber la IP real detras de Cloudfare

Para encontrar la IP real detrás de un sitio protegido por Cloudflare, normalmente necesitas combinar varias técnicas OSINT y de análisis de infraestructura, ya que Cloudflare actúa como un proxy inverso ocultando la IP del servidor origen. Aquí tienes un enfoque detallado, solo para fines legales, auditorías o pentesting autorizado:

---

## 1. **Comprobar historial de DNS**

- Usa servicios como:
    - SecurityTrails
    - ViewDNS
    - DNSDumpster
- Busca **registros históricos A** o **subdominios** que apunten directamente a una IP antes de que se configurara Cloudflare.
    

---

## 2. **Revisar subdominios sin Cloudflare**

- A veces solo el dominio principal pasa por Cloudflare y los subdominios (por ejemplo, `mail.dominio.com` o `direct.dominio.com`) resuelven directamente a la IP real.
- Herramientas útiles:
    - `subfinder`, `amass`, `assetfinder` (reconnaissance)
    - Ejemplo:
        `subfinder -d dominio.com | httpx -ip`

## 3. **Buscar filtraciones en cabeceras y servicios**

- Escanea la IP para encontrar servicios que respondan con el mismo **banner del servidor**.
- Compara cabeceras HTTP (`Server`, `X-Powered-By`) entre Cloudflare y candidatos.
- Ejemplo:
    `curl -I http://posible-ip`
    

## 4. **Historial WHOIS y registros inversos**

- Con WHOIS y búsquedas inversas de IP (`reverse IP lookup`) puedes encontrar otros dominios hospedados en la misma IP.
- Herramientas:
    - Shodan
    - Censys
        

## 5. **Comprobar registros SPF, DKIM, MX**

- Muchos administradores olvidan que los **registros MX** (correo) no pasan por Cloudflare y pueden apuntar a la misma máquina.
    
- Ejemplo:
    `dig MX dominio.com dig A mail.dominio.com`
    

## 6. **Filtraciones en contenido web o APIs**

- Busca rutas como `/robots.txt`, `/sitemap.xml`, o configuraciones JS que revelen subdominios internos.
- Analiza archivos antiguos en Wayback Machine para ver si aparece la IP.
    

## 7. **Errores de configuración**

- A veces el servidor responde por HTTP sin Cloudflare si accedes directamente por IP.
- Si encuentras una IP candidata:
    `curl -H "Host: dominio.com" http://IP_candidata`
    
    Si devuelve el mismo contenido que el dominio en Cloudflare, probablemente sea la IP real.
    

---

⚠ **Advertencia Legal:**  
Estas técnicas deben usarse únicamente en contextos **autorizados** (pentesting contratado, auditoría de tu propio dominio o CTF). En muchos países, el acceso o escaneo no autorizado a sistemas de terceros es ilegal.