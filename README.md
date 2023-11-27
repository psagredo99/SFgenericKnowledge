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

# API 302


-When we get 302 on an api integration it means we are being redirected.

```bash
HttpRequest request = new HttpRequest();
HttpResponse response = new HttpResponse();

// Assume that you have already made a request and obtained a response

// Get all header keys
List<String> headerKeys = response.getHeaderKeys();

// Iterate through header keys and print key-value pairs
for (String key : headerKeys) {
    String value = response.getHeader(key);
    System.debug(key + ': ' + value);
}
```

-Usually the correct api endpoint is located on header 'location' or 'Location' Its case sensistive
-So we need to resend request changing endpoint:

```bash
HttpResponse res = new Http().send(req);
while (res.getStatusCode() == 302) {
    req.setEndpoint(res.getHeader('Location'));
    res = new Http().send(req);
}
```
