---
layout: post
title:  "SSL Certificates"
date:   2022-08-01 18:00:00 +0900
categories: update
---

# Self Signed Certificates
Certificates not issued by known CA but rather by the server hosting the certificate are called self-signed. These are often used in internal development environments that are not customer facing. The root certificates for these will be absent in the browser’s certificate store.

# Java Truststore & KeyStore
In this section, we’ll discuss where certificates live on a system where the JDK/JRE is installed.

## Truststore
The truststore is a file that contains the root certificates for Certificate Authorities (CA) that issue certificates such as GoDaddy, Verisign, Network Solutions, and others. The truststore comes bundled with the JDK/JRE and is located in `$JAVA_HOME/lib/security/cacerts`. The truststore is used whenever our Java code establishes a connection over SSL.

## Keystore
The keystore is a file used by an application server to store its private key and site certificate.

So if we were running a web application over SSL at tomcat.codebyamir.com, the keystore file named keystore.jks would contain two entries — one for the private key and one for the certificate.

The keystore is used by Java application servers such as Tomcat to serve the certificates.


