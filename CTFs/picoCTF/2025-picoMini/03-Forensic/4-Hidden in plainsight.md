You’re given a seemingly ordinary JPG image. Something is tucked away out of sight inside the file. Your task is to discover the hidden payload and extract the flag.Download the jpg image [here](https://challenge-files.picoctf.net/c_saffron_estate/5037bce9fb8a1d1975211489cedcdcd2e374d9e1837d7ce76dc3355ba5d71952/img.jpg).

Hint
- Download the jpg image and read its metadata


## Solucion

- Vemos metadatos
```
exiftool img.jpg
ExifTool Version Number         : 12.57
File Name                       : img.jpg
Directory                       : .
File Size                       : 73 kB
File Modification Date/Time     : 2025:10:03 22:43:25+00:00
File Access Date/Time           : 2025:10:03 22:43:40+00:00
File Inode Change Date/Time     : 2025:10:03 22:43:39+00:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Comment                         : c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9
Image Width                     : 640
Image Height                    : 640
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 640x640
Megapixels                      : 0.410
```

- Decodificamos Comment de base64 y decodificamos de nuevo
```
steghide:

cEF6endvcmQ=
pAzzword
```

- Sacamos los datos con stehide y el password encontrado
```
➜  hiddenplain steghide --extract -sf img.jpg -p pAzzword
wrote extracted data to "flag.txt".
➜  hiddenplain cat flag.txt
picoCTF{h1dd3n_1n_1m4g3_656e4d79}
➜  hiddenplain
```