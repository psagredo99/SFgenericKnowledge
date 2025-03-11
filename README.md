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


# Send public images in email

-We can add public and working images from email using ContentVersion and ContentDistribution

```bash
ContentVersion contentVersionRec = new ContentVersion();
contentVersionRec.Title = fileName;
contentVersionRec.PathOnClient = '/' + fileName;
contentVersionRec.FirstPublishLocationId = contactRec.Id;
contentVersionRec.VersionData = EncodingUtil.base64Decode(base64File);
contentVersionRec.IsMajorVersion = true;
Insert contentVersionRec;
//update public link on Task
ContentDistribution cdl = new ContentDistribution();
cdl.ContentVersionId = contentVersionRec.Id;
cdl.Name = fileName;
cdl.PreferencesAllowViewInBrowser= true;

insert cdl;
  
ContentDistribution cd = [SELECT DistributionPublicUrl 
                           FROM ContentDistribution 
                           WHERE Id =: cdl.Id 
                           LIMIT 1];
```

# Test a SOAP API - aka sf webservice

We need 2 wsdl files:
-Generic wsdl class to populate login where we need username, password+token (we must append token to end of password).
-Specific class to be test 

Import both files to SOAP UI, first we need to generate auth token based on login.After we select the ws to be tested and select correct method (GET,POST etc) And send the xml file body and remove the headers as they are not needed.

![image](https://github.com/psagredo99/SFgenericKnowledge/assets/72439144/cebec758-5578-46fa-8a07-3b4bd9f6b65b)


# Missing a license from Prod env

In case we miss a license which is currently avalaible on prod env we just need to refresh licenses from Prod enviroment:
![image](https://github.com/user-attachments/assets/6ed1ccfe-8a54-42c4-b5a1-7d27354f961d)

# Matching files to storage usage

Check where Storage/File usage is being filled 

Queries needed:
https://trailhead.salesforce.com/es/trailblazer-community/feed/0D54S00000A7x1MSAR

Create a report:
https://www.simplysfdc.com/2018/05/salesforce-files-sharing-query.html#google_vignette

Create and assign new permission set:
https://help.salesforce.com/s/articleView?id=000381258&type=1
