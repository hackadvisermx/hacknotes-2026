# Cookie

SIV Pipeline Web Group 1

[https://xwiogivp.web.ctf.uscybergames.com](https://xwiogivp.web.ctf.uscybergames.com/)

## Solucion
- Inspeccionamos la cookie

```
QWZ0ZXIgaW5zcGVjdGluZyB0aGUgY29udGVudHMsIGhlJ2xsIGhvcCBvbiB0aGUgUk9CT1QgdmFjY3V1bSBwaWNraW5nIHVwIHRoZSBjcnVtYnMgaGUgbWFkZS4KQ3J1bWIgMTogZFY5Q1FHc3paRjloVA==


After inspecting the contents, he'll hop on the ROBOT vaccuum picking up the crumbs he made.
Crumb 1: dV9CQGszZF9hT


```

- Revisamos robots.txt
```
User-agent: *
Disallow: /admin

# The robot vaccuum arrives at a locked door, which naturally he'll want to get inside
# Crumb 2: jB0SDNSX2MwMG

```

- acceder a /admin
```
   <script>
        const ADMIN_USER = 'admin';
        const CRUMB_3 = 'sxM19mT3JfZEF';
        function login() {
            const user = document.getElementById('username').value;
            const pass = document.getElementById('password').value;
            if (user === ADMIN_USER && pass === CRUMB_3) {
                window.location.href = '/kitchen';
            } else {
                document.getElementById('error').style.display = 'block';
            }
        }

https://xwiogivp.web.ctf.uscybergames.com/kitchen/README.txt

Index of /kitchen/
Name	Last modified	Size
README.txt	2025-05-18 09:56	121
floor/	2025-05-18 10:19	-
pantry/	2025-05-18 10:22	-
refrigerator/	2025-05-18 10:16	-
stove/	2025-05-18 07:37	-

Breaking into the door will make him thirsty, he'll want to find a glass of MILK.

Crumb 3? Try the password on the door.s

```
- refrigerados
```
https://ziscyfvr.web.ctf.uscybergames.com/kitchen/refrigerator

// If he asks for a glass of milk, he's going to want a cookie to go with it.

function pourMilk() {
    console.log("Pouring a fresh glass of milk... 🥛");
}

//TODO: Follow cookie instructions written on NOTE in /kitchen
function bakeCookie() {
    var crumb4 = "fTW9VNWUhISE=";

    return false;
}

pourMilk();
```

 


- Juntamos todo
```
dV9CQGszZF9hTjB0SDNSX2MwMGsxM19mT3JfZEFfTW9VNWUhISE=

dV9CQGszZF9hT jB0SDNSX2MwMG sxM19mT3JfZEF fTW9VNWUhISE=



SVBRG{u_B@k3d_aN0tH3R_c00k13_fOr_dA_MoU5e!!!}
SVBGR{u_B@k3d_aN0tH3R_c00k13_fOr_dA_MoU5e!!!}

SVUSCG{u_B@k3d_aN0tH3R_c00k13_fOr_dA_MoU5e!!!}



```

- Se pone la cookie decodificada en el editor de cookies y se refresca /
```

SVBRG{he_w1ll_g!v3_y0u_A_fL@g_a5_tH4nk5!}

```