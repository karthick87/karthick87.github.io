---
layout: post
title:  "Installing Java in Windows 10"
date:   2022-08-01 10:00:00 +0900
categories: update
---

# Installing Java in Windows 10

# Setting Environment Variables

```shell
C:\Windows\system32>setx JAVA_HOME "C:\Program Files\Java\jdk1.8.0_152"
SUCCESS: Specified value was saved.

C:\Windows\system32>setx CLASSPATH "C:\Program Files\Java\jdk1.8.0_152\lib"
SUCCESS: Specified value was saved.

C:\Windows\system32>setx MAVEN_HOME "C:\opt\apache-maven-3.8.6"
SUCCESS: Specified value was saved.
```

**Note:** Adding **/M** `setx /M JAVA_HOME "C:\Program Files\Java\jdk1.8.0_152"` is considered as System Variable. Therefore if you wanted to set it as User Variable then remove **/M** and execute the command.

# Checking JAVA & MAVEN Home Path
```shell
C:\Users\murugkar>echo %JAVA_HOME%
C:\Program Files\Java\jdk1.8.0_152

C:\Users\murugkar>echo %MAVEN_HOME%
C:\opt\apache-maven-3.8.6

C:\Users\murugkar>echo %CLASSPATH%
C:\Program Files\Java\jdk1.8.0_152\lib
```

# Checking Java Version and Maven Version
Note: The below output indicates that we are using Oracle Java. Oracle during the last few years restricted the free use of their Java. 

```shell
C:\Users\murugkar>mvn -version
Apache Maven 3.8.6 (84538c9988a25aec085021c365c560670ad80f63)
Maven home: C:\opt\apache-maven-3.8.6
Java version: 1.8.0_152, vendor: Oracle Corporation, runtime: C:\Program Files\Java\jdk1.8.0_152\jre
Default locale: en_US, platform encoding: Cp1252
OS name: "windows 10", version: "10.0", arch: "amd64", family: "windows"

C:\Users\murugkar>java -version
java version "1.8.0_333"
Java(TM) SE Runtime Environment (build 1.8.0_333-b02)
Java HotSpot(TM) 64-Bit Server VM (build 25.333-b02, mixed mode)
```
# Java version: 1.8.0_152
`cacerts` is where Java stores Public certificates of root CA's. Java uses cacerts to authenticate to the servers. Keystore is where Java stores the Private keys of the clients so that it can share it to the server when the server requests client authentication.

**Note:** The initial password of the cacerts keystore file is changeit.

# To List All Certificates from Java Keystore
```cmd
keytool -list -v -keystore "%JAVA_HOME%\jre\lib\security\cacerts" -storepass changeit
```
---
# To Export Certificate from Java Keystore
```cmd
keytool -export -alias "digicertassuredidg3 [jdk]" -keystore "C:\Program Files\Java\jdk1.8.0_333\jre\lib\security\cacerts" -rfc -file C:\Users\murugkar\digi_cert -storepass changeit
```
---
# To Import Certificate into Java Keystore
```cmd
keytool -importcert -alias "digicertassuredidg3 [jdk]" -file C:\Users\murugkar\digi_cert -keystore "C:\Program Files\Java\jdk1.8.0_152\jre\lib\security\cacerts" -storepass changeit
```
---
# To Delete Certificate from Java Keystore
```cmd
keytool -delete -alias "digicertassuredidg3 [jdk]" -keystore "C:\Program Files\Java\jdk1.8.0_152\jre\lib\security\cacerts" -storepass changeit
```
Note: To import or to delete certificate from the keystore, we need to execute the command from Elevated Prompt.

---
