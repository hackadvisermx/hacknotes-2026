## Free Ski

_Difficulty:_ 

HONK! Well hello there! Fancy meeting you here in the Dosis Neighborhood. You know, it's the strangest thing... I used to just waddle around the Geese Islands going 'BONK' all day long. Random noises, no thoughts, just vibes. But then something changed, and now here I am—speaking, thinking, wondering how I even got here!

This game looks simple enough, doesn't it? Almost too simple. But between you and me... it seems nearly impossible to win fair and square.

My advice? If you ain't cheatin', you ain't tryin'. _wink_

Now get out there and show that mountain who's boss!

## Hints

### 1
 Extraction
From: Santa
Objective: Free Ski
Have you ever used PyInstaller Extractor?



# Solve

# d1
```
sudo apt install pyinstxtractor

┌──(root㉿kali)-[/home/kali/tmp/sans-hd-2025/freeski]
└─#  pyinstxtractor FreeSki.exe 
[+] Processing FreeSki.exe
[+] Pyinstaller version: 2.1+
[+] Python version: 3.13
[+] Length of package: 16806404 bytes
[+] Found 98 files in CArchive
[+] Beginning extraction...please standby
[+] Possible entry point: pyiboot01_bootstrap.pyc
[+] Possible entry point: pyi_rth_inspect.pyc
[+] Possible entry point: pyi_rth_pkgres.pyc
[+] Possible entry point: pyi_rth_setuptools.pyc
[+] Possible entry point: pyi_rth_multiprocessing.pyc
[+] Possible entry point: pyi_rth_pkgutil.pyc
[+] Possible entry point: FreeSki.pyc
[+] Found 471 files in PYZ archive
[!] Error: Failed to decompress PYZ.pyz_extracted/jaraco.pyc, probably encrypted. Extracting as is.
[!] Error: Failed to decompress PYZ.pyz_extracted/setuptools/_distutils/compilers.pyc, probably encrypted. Extracting as is.
[!] Error: Failed to decompress PYZ.pyz_extracted/setuptools/_distutils/compilers/C.pyc, probably encrypted. Extracting as is.
[!] Error: Failed to decompress PYZ.pyz_extracted/setuptools/_vendor.pyc, probably encrypted. Extracting as is.
[!] Error: Failed to decompress PYZ.pyz_extracted/setuptools/_vendor/jaraco.pyc, probably encrypted. Extracting as is.
[+] Successfully extracted pyinstaller archive: FreeSki.exe

You can now use a python decompiler on the pyc files within the extracted directory

```

## d2
```
pipx install uncompyle6
  installed package uncompyle6 3.9.3, installed using Python 3.13.9
  These apps are now globally available
    - uncompyle6
    - uncompyle6-tokenize
⚠️  Note: '/root/.local/bin' is not on your PATH environment variable. These apps will not be globally accessible until your PATH is updated. Run `pipx ensurepath` to
    automatically add it, or manually modify your PATH in your shell's config file (e.g. ~/.bashrc).
done! ✨ 🌟 ✨

──(root㉿kali)-[/home/…/tmp/sans-hd-2025/freeski/FreeSki.exe_extracted]
└─# uncompyle6 FreeSki.pyc > FreeSki.py

# Unsupported bytecode in file FreeSki.pyc
# Unsupported Python version, 3.13.0, for decompilation

# Unsupported Python version, 3.13.0, for decompilation
# Can't uncompile FreeSki.pyc

```

## d3
```
cd /tmp  # Move to a temporary directory
git clone https://github.com/zrax/pycdc.git
cd pycdc
cmake .
make
```

