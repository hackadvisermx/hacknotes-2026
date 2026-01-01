
Sometimes things are more annoying than they are difficult.

 [DLXENH.zip](https://play.bcactf.com/files/97bf5ef2f616239dad944354696f10d2/DLXENH.zip?token=eyJ1c2VyX2lkIjozMDYsInRlYW1faWQiOjE5NSwiZmlsZV9pZCI6NTF9.aFnkqw.PlaaRx22IeZfYrFtveKYHwWT3TM "DLXENH.zip")

## Solve

- se pude intentar desmpaquetar hasta el cansancio
```python
import zipfile
import os
import glob

def unzip_in_place(start_zip):
    current = start_zip
    i = 0

    while True:
        try:
            with zipfile.ZipFile(current, 'r') as zip_ref:
                zip_ref.extractall()
                print(f"[+] Extracted: {current}")
        except zipfile.BadZipFile:
            print(f"[!] Not a valid zip file: {current}")
            break

        # Delete the zip we just extracted
        os.remove(current)

        # Find the next .zip file (should be only one new zip)
        zips = glob.glob("*.zip")
        if not zips:
            print("[*] No more .zip files found.")
            break

        current = zips[0]
        i += 1

# 🔧 Usage
unzip_in_place("DLXENH.zip")

```

- o solo darle in strings

```
strings DLXENH.zip | grep bca
bcactf{w3ll_th4t_w4s_4nn0y1ng_fca743ef043c1d8}
```
