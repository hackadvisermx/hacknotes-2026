

# Tarred and Feathered

i recently exfiltrated this archive from a suspect's computer. they illegally stole all of our flags.

however, not everything is as it seems. the flag is in the archive, but where? i couldn't find it, can you?


## Solve

- directo
```
strings challenge.tar| grep bca
bcactf{you_tarred_me_apart_1bf1fb1}
```

- listamos archivos
```
tar -tf challenge.tar | nl

     1	note.txt
     2	../.cache/.hidden_logs/.�\200\213flag.txt

FILENAME=$(tar -xOf challenge.tar | sed -n '2p')
tar -xOf challenge.tar "$FILENAME"
tar: bcactf{you_tarred_me_apart_1bf1fb1}: Not found in archive
tar: Error exit delayed from previous errors.
```


```
ver caracteres invisivles



tar -tf challenge.tar | od -c

0000000    n   o   t   e   .   t   x   t  \n   .   .   /   .   c   a   c
0000020    h   e   /   .   h   i   d   d   e   n   _   l   o   g   s   /
0000040    . 342   \   2   0   0   \   2   1   3   f   l   a   g   .   t
0000060    x   t  \n
0000063


```



```
bcactf{you_tarred_me_apart_1bf1fb1}

```