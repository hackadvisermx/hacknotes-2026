Never forget to remove RIFA caps from vintage computer power supplies when restoring a system. I love vintage computing, its the very core of where and when it all began. Sometimes it is the people no one can imagine anything of who do the things no one can imagine. - Alan Turing. You never forget your first 8-bit system.

This FAT12 floppy disk image must have been under an arcade machine here in the Retro Store.

When I was a kid we shared warez by hiding things as deleted files.

I remember writing programs in BASIC. So much fun! My favorite was Star Trek.

The beauty of file systems is that 'deleted' doesn't always mean gone forever.

Ready to dive into some digital archaeology and see what secrets this old disk is hiding?

Download the floppy disk image, and see what you can find!

Hint> I know there are still tools available that can help you find deleted files. Maybe that might help. Ya know, one of my favorite games was a Quick Basic game called Star Trek.
Hint> Wow! A disk from the 1980s! I remember delivering those computer disks to the good boys and girls. Games were their favorite, but they weren't like they are now.

## Retro Recovery

_Difficulty:_ * *
Join Mark in the retro shop. Analyze his disk image for a blast from the retro past and recover some classic treasures.


- Intento 1
```
fls floppy.img -r
r/r * 6:	all_i-want_for_christmas.bas
d/d 8:	qb45
+ r/r 1189:	BC.EXE
+ r/r 1190:	BRUN45.EXE
+ r/r 1191:	LIB.EXE
+ r/r 1192:	LINK.EXE
+ r/r 1193:	MOUSE.COM
+ r/r 1196:	PACKING.LST.txt
+ r/r 1197:	QB.EXE
+ r/r 1198:	QB.INI
r/r * 10:	.all_i-want_f
v/v 45779:	$MBR
v/v 45780:	$FAT1
v/v 45781:	$FAT2
V/V 45782:	$OrphanFiles

```

- Intento 2
```
strings floppy.img | less
echo "bWVycnkgY2hyaXN0bWFzIHRvIGFsbCBhbmQgdG8gYWxsIGEgZ29vZCBuaWdodAo=" | base64 -d
merry christmas to all and to all a good night
```