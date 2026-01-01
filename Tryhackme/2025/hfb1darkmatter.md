
# hfb1darkmatter

The Hackfinitiy high school has been hit by DarkInjector's ransomware, and some of its critical files have been encrypted. We need you and Void to use your crypto skills to find the RSA private key and restore the files. After some research and reverse engineering, you discover they have forgotten to remove some debugging from their code. The ransomware saves this data to the tmp directory.

Click the start machine button below, the VM will open in your browser:

Can you find the RSA private key?  
  
Note:  
**  
You can close the window prompting for a password after the VM has booted; this will not affect the challenge.  
If you close the ransomware note before solving the challenge, you might need to reboot the VM.**  
  

## Solve

```
buntu@tryhackme:/tmp$ ls
dock-replace.log
encrypted_aes_key.bin
public_key.txt
snap-private-tmp
systemd-private-682971858fa846099f1d47c59048dd98-ModemManager.service-bZZgEd
systemd-private-682971858fa846099f1d47c59048dd98-colord.service-LkogaV
systemd-private-682971858fa846099f1d47c59048dd98-polkit.service-GR9E7D
systemd-private-682971858fa846099f1d47c59048dd98-power-profiles-daemon.service-p3nz4l
systemd-private-682971858fa846099f1d47c59048dd98-switcheroo-control.service-ums1WY
systemd-private-682971858fa846099f1d47c59048dd98-systemd-logind.service-flmTbk
systemd-private-682971858fa846099f1d47c59048dd98-systemd-resolved.service-bLnPwU
systemd-private-682971858fa846099f1d47c59048dd98-systemd-timedated.service-mJ2Jh3
systemd-private-682971858fa846099f1d47c59048dd98-systemd-timesyncd.service-ziXweb
systemd-private-682971858fa846099f1d47c59048dd98-upower.service-iKdwM2
tigervnc.TRqLaJ
ubuntu@tryhackme:/tmp$ cat public_key.txt 
n=340282366920938460843936948965011886881
e=65537
ubuntu@tryhackme:/tmp$ 

```

- Abrimos el archivo encriptado: student_grades.docx
```
THM{d0nt_l34k_y0ur_w34k_m0dulu5}
```

