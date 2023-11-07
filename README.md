# SFgenericKnowledge

# Transform .pfx certs to .jks 

keytool -importkeystore -srckeystore archivo.pfx -srcstoretype pkcs12 -destkeystore salida.jks -deststoretype JKS
 
keytool -changealias -alias 1 -destalias nuevoAlias -keystore salida.jks
