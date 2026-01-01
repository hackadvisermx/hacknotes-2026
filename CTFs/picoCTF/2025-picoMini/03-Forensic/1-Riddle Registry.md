Hi, intrepid investigator! 📄🔍 You've stumbled upon a peculiar PDF filled with what seems like nothing more than garbled nonsense. But beware! Not everything is as it appears. Amidst the chaos lies a hidden treasure—an elusive flag waiting to be uncovered.Find the PDF file here [Hidden Confidential Document](https://challenge-files.picoctf.net/c_saffron_estate/8fc7f4db4cd616afa42099769749bbf3620925ed4ee7d2037ffdbd525aa14dc6/confidential.pdf) and uncover the flag within the metadata.

Hints:
- Don't be fooled by the visible text; it’s just a decoy!
- Look beyond the surface for hidden clues

## Solucion

```

apt update && apt install poppler-utils
pdftotext confidential.pdf h.txt

cat h.txt

Title: The Ultimate Guide to Flag Hunting
Welcome to the challenge!
Don’t worry, this might look like gibberish, but maybe there’s something hidden somewhere? I
spent so much time creating this PDF with care... or maybe not!

Here’s a Quick Story:
Once upon a time, in a land far, far away, there was a secret... But where could it be? Hidden
deep within the document? Maybe the text holds clues?
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante venenatis
dapibus posuere velit aliquet. Aenean lacinia bibendum nulla sed consectetur. Fusce dapibus,
tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet
risus. Curabitur blandit tempus porttitor. Lorem ipsum dolor sit amet, consectetur adipiscing elit.
You thought this was important? Nah, it’s just random text. Keep looking. Or maybe, just
maybe, you’re in the wrong place?

Special Hidden Section:
The author have done a great and good job
Don’t bother trying to reveal the hidden text, it’s just nonsense anyway. Even if you somehow
manage to do it, all you’ll get is:
No flag here. Nice try though!

If you're still reading this, I’ll tell you a secret: the answer might not be here after all...

Good luck! You’ll need it!
```

- metadatos
```
exiftool confidential.pdf
ExifTool Version Number         : 12.57
File Name                       : confidential.pdf
Directory                       : .
File Size                       : 183 kB
File Modification Date/Time     : 2025:10:03 21:15:11+00:00
File Access Date/Time           : 2025:10:03 21:16:15+00:00
File Inode Change Date/Time     : 2025:10:03 21:16:14+00:00
File Permissions                : -rw-r--r--
File Type                       : PDF
File Type Extension             : pdf
MIME Type                       : application/pdf
PDF Version                     : 1.7
Linearized                      : No
Page Count                      : 1
Producer                        : PyPDF2
Author                          : cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOGY5MWQ2OH0=
```

- decodificar
```
echo cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOGY5MWQ2OH0= | base64 -d
picoCTF{puzzl3d_m3tadata_f0und!_c8f91d68}
```