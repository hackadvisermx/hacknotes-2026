



```
file stick.img    
stick.img: DOS/MBR boot sector, code offset 0x58+2, OEM-ID "mkfs.fat", sectors 49152 (volumes <=32 MB), Media descriptor 0xf8, sectors/track 32, heads 4, FAT (32 bit), sectors/FAT 378, serial number 0x8caae860, unlabeled


```


```
hexdump -C stick.img | head -n 10

00000000  eb 58 90 6d 6b 66 73 2e  66 61 74 00 02 01 20 00  |.X.mkfs.fat... .|
00000010  02 00 00 00 c0 f8 00 00  20 00 04 00 00 00 00 00  |........ .......|
00000020  00 00 00 00 7a 01 00 00  00 00 00 00 02 00 00 00  |....z...........|
00000030  01 00 06 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
00000040  80 00 29 60 e8 aa 8c 4e  4f 20 4e 41 4d 45 20 20  |..)`...NO NAME  |
00000050  20 20 46 41 54 33 32 20  20 20 0e 1f be 77 7c ac  |  FAT32   ...w|.|
00000060  22 c0 74 0b 56 b4 0e bb  07 00 cd 10 5e eb f0 32  |".t.V.......^..2|
00000070  e4 cd 16 cd 19 eb fe 54  68 69 73 20 69 73 20 6e  |.......This is n|
00000080  6f 74 20 61 20 62 6f 6f  74 61 62 6c 65 20 64 69  |ot a bootable di|
00000090  73 6b 2e 20 20 50 6c 65  61 73 65 20 69 6e 73 65  |sk.  Please inse|

```


```
┌──(kali㉿kali)-[~/tmp/scriptctf/forensic/disk]
└─$ mkdir /tmp/stick
                                                                                                                                                                                                                 
┌──(kali㉿kali)-[~/tmp/scriptctf/forensic/disk]
└─$ sudo mount -t vfat -o loop,ro stick.img /tmp/stick

[sudo] password for kali: 
                                                                                                                                                                                                                 
┌──(kali㉿kali)-[~/tmp/scriptctf/forensic/disk]
└─$ ls /tmp/stick 
notes.txt  random_thoughts.txt
                                                                                                                                                                                                                 
┌──(kali㉿kali)-[~/tmp/scriptctf/forensic/disk]
└─$ 

```

