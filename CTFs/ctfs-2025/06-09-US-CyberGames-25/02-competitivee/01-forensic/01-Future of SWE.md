
# Future of SWE

Competitive

Chris Haller

Our founder is convinced that ChatGPT will replace all sofware engineers in the future. Perhaps related, but it appears the ClippyGPT SaaS he's signed up for has deleted his documents. Can you help recover them?

# Solucion

- ver particiones
```
fdisk -l future_of_swe.raw.001
Disk future_of_swe.raw.001: 128 MiB, 134217728 bytes, 262144 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x6f20736b

Device                  Boot      Start        End    Sectors   Size Id Type
future_of_swe.raw.001p1       778135908 1919645538 1141509631 544.3G 72 unknown
future_of_swe.raw.001p2       168689522 2104717761 1936028240 923.2G 65 Novell Netware 386
future_of_swe.raw.001p3      1869881465 3805909656 1936028192 923.2G 79 unknown
future_of_swe.raw.001p4               0 3637226495 3637226496   1.7T  d unknown

Partition table entries are not in disk order.

```

- extraer con binwalk
```
binwalk --dd='.*' future_of_swe.raw.001


Extractor Exception: Binwalk extraction uses many third party utilities, which may not be secure. If you wish to have extraction utilities executed as the current user, use '--run-as=root' (binwalk itself must be run as root).
----------------------------------------------------------------------------------------------------
Traceback (most recent call last):
  File "/usr/lib/python3/dist-packages/binwalk/core/module.py", line 258, in __init__
    self.load()
    ~~~~~~~~~^^
  File "/usr/lib/python3/dist-packages/binwalk/modules/extractor.py", line 153, in load
    raise ModuleException("Binwalk extraction uses many third party utilities, which may not be secure. If you wish to have extraction utilities executed as the current user, use '--run-as=%s' (binwalk itself must be run as root)." % user_info.pw_name)
binwalk.core.exceptions.ModuleException: Binwalk extraction uses many third party utilities, which may not be secure. If you wish to have extraction utilities executed as the current user, use '--run-as=root' (binwalk itself must be run as root).
----------------------------------------------------------------------------------------------------

                                                                                                                                                                                                                                
┌──(root㉿kali)-[/home/…/uscyber/competitive/forensic/futureswe]
└─# binwalk --dd='.*' future_of_swe.raw.001 --run-as=root

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
288768        0x46800         PDF document, version: "1.3"
348160        0x55000         Zip archive data, at least v2.0 to extract, compressed size: 361, uncompressed size: 1440, name: [Content_Types].xml
349090        0x553A2         Zip archive data, at least v2.0 to extract, compressed size: 244, uncompressed size: 588, name: _rels/.rels
349895        0x556C7         Zip archive data, at least v2.0 to extract, compressed size: 677, uncompressed size: 1625, name: xl/workbook.xml
350617        0x55999         Zip archive data, at least v2.0 to extract, compressed size: 258, uncompressed size: 980, name: xl/_rels/workbook.xml.rels
351195        0x55BDB         Zip archive data, at least v2.0 to extract, compressed size: 658, uncompressed size: 1535, name: xl/worksheets/sheet1.xml
351907        0x55EA3         Zip archive data, at least v2.0 to extract, compressed size: 615, uncompressed size: 1377, name: xl/worksheets/sheet2.xml
352576        0x56140         Zip archive data, at least v2.0 to extract, compressed size: 583, uncompressed size: 1247, name: xl/worksheets/sheet3.xml
353213        0x563BD         Zip archive data, at least v2.0 to extract, compressed size: 1638, uncompressed size: 6995, name: xl/theme/theme1.xml
354900        0x56A54         Zip archive data, at least v2.0 to extract, compressed size: 677, uncompressed size: 1618, name: xl/styles.xml
355620        0x56D24         Zip archive data, at least v2.0 to extract, compressed size: 373, uncompressed size: 768, name: xl/sharedStrings.xml
356043        0x56ECB         Zip archive data, at least v2.0 to extract, compressed size: 333, uncompressed size: 613, name: docProps/core.xml
356687        0x5714F         Zip archive data, at least v2.0 to extract, compressed size: 394, uncompressed size: 820, name: docProps/app.xml
358171        0x5771B         End of Zip archive, footer length: 22
362056        0x58648         XML document, version: "1.0"


```

```
ls -la
total 527200
drwxr-xr-x 6 root root          192 Jun 13 00:42 .
drwxr-xr-x 5  501 dialout       160 Jun 13 00:42 ..
-rw-r--r-- 1 root root    133928960 Jun 13 00:42 46800
-rw-r--r-- 1 root root    133869568 Jun 13 00:42 55000
-rw-r--r-- 1 root root    133859557 Jun 13 00:42 5771B
-rw-r--r-- 1 root root    133855672 Jun 13 00:42 58648

file ./*  
./5771B: Zip archive data (empty)
./46800: PDF document, version 1.3, 2 page(s)
./55000: Microsoft Excel 2007+
./58648: data

```

```
fls -r -f fat16 future_of_swe.raw.001

r/r 3:  NEW VOLUME  (Volume Label Entry)
d/d 6:  System Volume Information
+ r/r 519:      WPSettings.dat
+ r/r 522:      IndexerVolumeGuid
r/r 9:  meeting_notes.txt
r/r 12: AI_vs_Humanity.pdf
r/r 15: clippyGPT_log.txt
r/r * 18:       passwords.xlsx
r/r * 21:       ProjectNextBigThing.docx
v/v 4185987:    $MBR
v/v 4185988:    $FAT1
v/v 4185989:    $FAT2
V/V 4185990:    $OrphanFiles

```

```bash
icat -f fat16 future_of_swe.raw.001 9        
=== 18-May-2025 Staff Sync ===
- Agenda: ClippyGPT post-deployment triage
- Action: Investigate why ClippyGPT replaced CEO password with "password123"
- Reminder: ProjectNextBigThing.docx was “encrypted” during cleanup.
  Password stored in passwords.xlsx, Sheet2, row 4.


 (\_/)
 (•‿•)  <-- 'Everything's fine' meme bunny
 /   \


=== 18-May-2025 Ad-hoc ===
- Determine if AI deleting files actually improves productivity...

```

```
icat -f fat16 future_of_swe.raw.001 18 > passwords.xlsx

Website	Username	Password
example.com	alice	h@rdPa$$1!
email.org	bob	P@55w0rd!
supersecure.net	ceo	CorrectHorseBatteryStaple

ClippyGPT Generated Passwords
clippyisawesome
1234
password123
ilovecoffee


```


```
icat -f fat16 future_of_swe.raw.001 21 > ProjectNextBigThing.docx

clippyisawesome

```

```
SVUSCG{th3_futur3_is_look1n_br1ght}
```