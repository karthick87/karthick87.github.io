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
