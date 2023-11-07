# SFgenericKnowledge

# Transform .pfx certs to .jks 


-Basic cert transformation
```bash
keytool -importkeystore -srckeystore archivo.pfx -srcstoretype pkcs12 -destkeystore salida.jks -deststoretype JKS

```

-Change alias of keys in case of alias error

```bash
keytool -changealias -alias 1 -destalias nuevoAlias -keystore salida.jks
```
