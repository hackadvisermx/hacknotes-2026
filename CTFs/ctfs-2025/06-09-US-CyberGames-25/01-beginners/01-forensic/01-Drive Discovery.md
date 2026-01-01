
# Drive Discovery

SIV Pipeline Forensics Group 1

 [drivediscovery.zip](https://ctf.uscybergames.com/files/3fcada93af9e766aacd1c200a62c3819/drivediscovery.zip?token=eyJ1c2VyX2lkIjoyMjEsInRlYW1faWQiOm51bGwsImZpbGVfaWQiOjZ9.aEeTBg.ulPU6PbpVQ0q2K-EBIoWvpC803c "drivediscovery.zip")
## Solucion



```
┌──(root㉿kali)-[/home/kali/tmp/uscyber]
└─# mmls nothinginterestinghere.001             
GUID Partition Table (EFI)
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Safety Table
001:  -------   0000000000   0000000127   0000000128   Unallocated
002:  Meta      0000000001   0000000001   0000000001   GPT Header
003:  Meta      0000000002   0000000033   0000000032   Partition Table
004:  000       0000000128   0000016511   0000016384   Basic data partition
005:  -------   0000016512   0000020479   0000003968   Unallocated
                                                                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/tmp/uscyber]
└─# fls -o 128 nothinginterestinghere.001
r/r 4-128-1:    $AttrDef
r/r 8-128-2:    $BadClus
r/r 8-128-1:    $BadClus:$Bad
r/r 6-128-4:    $Bitmap
r/r 7-128-1:    $Boot
d/d 11-144-4:   $Extend
r/r 2-128-1:    $LogFile
r/r 0-128-6:    $MFT
r/r 1-128-1:    $MFTMirr
d/d 36-144-1:   $RECYCLE.BIN
r/r 9-128-8:    $Secure:$SDS
r/r 9-144-11:   $Secure:$SDH
r/r 9-144-14:   $Secure:$SII
r/r 10-128-1:   $UpCase
r/r 10-128-4:   $UpCase:$Info
r/r 3-128-3:    $Volume
d/d 39-144-1:   Pictures
d/d 35-144-1:   Recipes
d/d 40-144-1:   Secrets
d/d 41-144-1:   System Volume Information
-/d * 51-144-1: MSI82360.tmp
V/V 256:        $OrphanFiles
                                                                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/tmp/uscyber]
└─# fls -o 128 nothinginterestinghere.001 40-144-1
r/r 49-128-1:   note to self.txt
-/r * 50-128-1: flag.txt
                                                                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/tmp/uscyber]
└─# icat -o 128 nothinginterestinghere.001 50-128-1
U1ZCUkd7ZDNsMzczZF9uMDdfZjByNjA3NzNuXzI4MzAyOTM4Mn0=                                                                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/tmp/uscyber]
└─# icat -o 128 nothinginterestinghere.001 50-128-1 | base64 -d
SVBRG{d3l373d_n07_f0r60773n_283029382}                                                                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/tmp/uscyber]

```
