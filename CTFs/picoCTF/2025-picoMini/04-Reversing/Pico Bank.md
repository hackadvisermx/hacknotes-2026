In a bustling city where innovation meets finance, Pico Bank has emerged as a beacon of cutting-edge security. Promising state-of-the-art protection for your assets, the bank claims its mobile application is impervious to all forms of cyber threats. Pico Bank’s tagline, "Security Beyond the Limits," echoes through its high-tech marketing campaigns, assuring users of their utmost safety.As a cybersecurity enthusiast, your mission is to test these bold claims. You’ve been hired by a secretive organization to put Pico Bank’s mobile app through a rigorous security assessment. The flag might be in one or more locations, and additional information reveals that a Pico Bank user’s credentials were leaked in an unusual way. Your task is to crack the username and password based on the following profile information: His name is Alex Johnson with the email johnson@picobank.com, Date of Birth: March 14, 1990, Last Transaction Amount: $345.67, Pet name: tricky, and Favorite Color: Blue.To perform this challenge, you can use any Android emulator. Some examples include [Genymotion Android Emulator](https://www.genymotion.com/product-desktop/download/) or [Android Studio](https://developer.android.com/studio).

Additional details will be available after launching your challenge instance.

Hints
- Use tools like JadxGUI or apktool to inspect the APK.
- Look at the app's network requests, especially for login and OTP.
- The flag has two parts.
- Check the server’s response after entering the correct OTP.
- Investigate the transaction history for unusual data.

## Solucion

- Instalar jadx en kali
```
sudo apt install jadx 
```

- Examinamos con jadx-gui
```
jadx-gui picobank.apk
```
- vamos a Source Code - example.picobank - Login, y sacamos el user y pass
``` 
 if ("johnson".equals(username) && "tricky1990".equals(password))
 
johnson
tricky1990

9673

```



- Obtener mi IP en mac
```
ifconfig | grep "inet "

	inet 127.0.0.1 netmask 0xff000000
	inet 127.94.0.1 netmask 0xff000000
	inet 192.168.100.11 netmask 0xffffff00 broadcast 192.168.100.255
```


- Instalar Android tools en mac
```
brew install --cask android-platform-tools

```

- Instalar android tools en Kali
```
sudo apt install android-tools-adb 
```
## Crear dispositivo nuevo emulado en Androido Sutdio
- Solo tener en cuenta API Google, no Play Store (Los XL me funcionaron)

## Agregar el certificado de Burp al dispositivo
### Preparar el certificado para copia en el dispositivo emulado
- Exportar certificado de burp
- Convertirlo al formato pem
```
openssl x509 -inform DER -in cacert.der -out cacert.pem
```
- obtener el hash
```
openssl x509 -inform PEM -subject_hash_old -in cacert.pem | head -1
```
- renombar el archivo con el nombre del hash
```
mv cacert.pem 9a5ba578.0
```
- subirlo al dispositivo
```
adb push 9a5ba575.0 /sdcard/
```
### Copiar certificado al dispositivo emulado 
- Iniciar en modo root y remontar el sistema (talvez requeira reiniciar)
```
adb devices
adb root
adb remount
adb reboot
```
- Copiar el certificado de /sdcard al /systema
```
mount -o rw,remount /system
mv /sdcard/9a5ba578.0 /system/etc/security/cacerts/
chmod 644 /system/etc/security/cacerts/9aef356c.0

```



## En mac con Android Studio

### Listar dispositivos
```
~/Library/Android/sdk/emulator/emulator -list-avds

Medium_Phone_API_36.1
Pixel_2_XL
```
### Iniciarlo con sistemas escribible
```
~/Library/Android/sdk/emulator/emulator -adv Pixel_2_XL -writable-system
```
### Parar un dispositivo
```
adb devices

List of devices attached
emulator-5554	device

adb -s emulator-5554 emu kill

OK: killing emulator, bye bye
OK

```
### Reiniciar
```
adb reboot
```
### Root y remount para poder escribir
```
❯ adb devices
List of devices attached
emulator-5554	device

 
❯ adb root
restarting adbd as root
 
❯ adb remount
Successfully disabled verity
```

## Makig para roterar Android emulads

```


```


## Instalar modulo para certificados

```
https://github.com/NVISOsecurity/AlwaysTrustUserCerts/releases


```

## Frida

```
adb push frida-server /data/local/tmp/
adb shell "chmod 755 /data/local/tmp/frida-server"
adb shell "su -c /data/local/tmp/frida-server &" 


source ~/venv/bin/activate
pip install frida-tools
frida-ps -Uia



```


## Remove disable proxy
```
adb shell settings delete global http_proxy
adb shell settings delete global global_http_proxy_host
adb shell settings delete global global_http_proxy_port
```

## logcat
- listar paquetes
```
pm list packages | grep pico
package:com.example.picobank
```
- sacar el PID
```
pidof com.example.picobank
6640
```
- ver los logs solo de mi app
```
logcat --pid=6640
```

## Referencias
https://www.youtube.com/watch?v=R3ptGaFW1AU
https://www.youtube.com/watch?v=QzsNn3GhYYk
https://www.youtube.com/watch?v=pcwRWBHFAlg

https://github.com/NVISOsecurity/AlwaysTrustUserCerts/releases
https://gitlab.com/newbit/rootAVD

https://github.com/frida/frida



en jadx

- buscamos opt_value
```
    <string name="otp_value">9673</string>
```

```

        this.transactionList.add(new Transaction("Grocery Shopping", "2023-07-21", "$ 1110000", false));
        this.transactionList.add(new Transaction("Electricity Bill", "2023-07-20", "$ 1101001", false));
        this.transactionList.add(new Transaction("Salary", "2023-07-18", "$ 1100011", true));
        this.transactionList.add(new Transaction("Internet Bill", "2023-07-17", "$ 1101111", false));
        this.transactionList.add(new Transaction("Freelance Payment", "2023-07-16", "$ 1000011", true));
        this.transactionList.add(new Transaction("Dining Out", "2023-07-15", "$ 1010100", false));
        this.transactionList.add(new Transaction("Gym Membership", "2023-07-14", "$ 1000110", false));
        this.transactionList.add(new Transaction("Stocks Dividend", "2023-07-13", "$ 1111011", true));
        this.transactionList.add(new Transaction("Car Maintenance", "2023-07-12", "$ 110001", false));
        this.transactionList.add(new Transaction("Gift Received", "2023-07-11", "$ 1011111", true));
        this.transactionList.add(new Transaction("Rent", "2023-07-10", "$ 1101100", false));
        this.transactionList.add(new Transaction("Water Bill", "2023-07-09", "$ 110001", false));
        this.transactionList.add(new Transaction("Interest Earned", "2023-07-08", "$ 110011", true));
        this.transactionList.add(new Transaction("Medical Expenses", "2023-07-07", "$ 1100100", false));
        this.transactionList.add(new Transaction("Transport", "2023-07-06", "$ 1011111", false));
        this.transactionList.add(new Transaction("Bonus", "2023-07-05", "$ 110100", true));
        this.transactionList.add(new Transaction("Subscription Service", "2023-07-04", "$ 1100010", false));
        this.transactionList.add(new Transaction("Freelance Payment", "2023-07-03", "$ 110000", true));
        this.transactionList.add(new Transaction("Entertainment", "2023-07-02", "$ 1110101", false));
        this.transactionList.add(new Transaction("Groceries", "2023-07-01", "$ 1110100", false));
        this.transactionList.add(new Transaction("Insurance Premium", "2023-06-28", "$ 1011111", false));
        this.transactionList.add(new Transaction("Charity Donation", "2023-06-26", "$ 1100010", true));
        this.transactionList.add(new Transaction("Vacation Expense", "2023-06-26", "$ 110011", false));
        this.transactionList.add(new Transaction("Home Repairs", "2023-06-24", "$ 110001", false));
        this.transactionList.add(new Transaction("Pet Care", "2023-06-22", "$ 1101110", false));
        this.transactionList.add(new Transaction("Personal Loan", "2023-06-18", "$ 1100111", true));
        this.transactionList.add(new Transaction("Childcare", "2023-06-15", "$ 1011111", false));
```

```
1110000
1101001
1100011
1101111
1000011
1010100
1000110
1111011
110001
1011111
1101100
110001
110011
1100100
1011111
110100
1100010
110000
1110101
1110100
1011111
1100010
110011
110001
1101110
1100111
1011111
```


```
picoCTF{1_l13d_4b0ut_b31ng_s3cur3d_m0b1l3_l0g1n_56fd4e6b}}

picoCTF{1_l13d_4b0ut_b31ng_1337}

picoCTF{1_l13d_4b0ut_b31ng_s4f3}
picoCTF{1_l13d_4b0ut_b31ng_s3cur3}
picoCTF{1_l13d_4b0ut_b31ng_9673}
picoCTF{1_l13d_4b0ut_b31ng_flag}
```

## Al final

```
curl -X POST http://saffron-estate.picoctf.net:50504/verify-otp -H "Content-Type: application/json" -d '{"otp":"9673"}' {"success":true,"message":"OTP verified successfully","flag":"s3cur3d_m0b1l3_l0g1n_56fd4e6b}","hint":"The other part of the flag is hidden in the app"}
```
## Referencias
- Binarios de andriod arm64 > https://github.com/bnsmb/binaries-for-Android/tree/main/binaries
