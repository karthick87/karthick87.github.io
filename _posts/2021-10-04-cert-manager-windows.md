---
layout: post
title:  "Certificate Manager in Windows 10"
date:   2021-10-04 15:00:00 +0900
categories: update
---

- Generate a Key-Pair
- Extract Public Key
- Generate CSR File
- Generate Self-Signed Certificate

```
$ openssl version -a
OpenSSL 1.1.1k  25 Mar 2021
built on: Thu Mar 25 15:15:09 2021 UTC
platform: mingw64
options:  bn(64,64) rc4(16x,int) des(long) idea(int) blowfish(ptr)
compiler: gcc -m64 -Wall -O3 -DL_ENDIAN -DOPENSSL_PIC -DOPENSSL_CPUID_OBJ -DOPENSSL_IA32_SSE2 -DOPENSSL_BN_ASM_MONT -DOPENSSL_BN_ASM_MONT5 -DOPENSSL_BN_ASM_GF2m -DSHA1_ASM -DSHA256_ASM -DSHA512_ASM -DKECCAK1600_ASM -DRC4_ASM -DMD5_ASM -DAESNI_ASM -DVPAES_ASM -DGHASH_ASM -DECP_NISTZ256_ASM -DX25519_ASM -DPOLY1305_ASM -DUNICODE -D_UNICODE -DWIN32_LEAN_AND_MEAN -D_MT -DZLIB -DZLIB_SHARED -DNDEBUG -D__MINGW_USE_VC2005_COMPAT -DOPENSSLBIN="\"/mingw64/bin\""
OPENSSLDIR: "/mingw64/ssl"
ENGINESDIR: "/mingw64/lib/engines-1_1"
Seeding source: os-specific
```

# Generating a Key Pair 

It contains both public and private key

```
$ openssl genrsa -out demo.key 2048
Generating RSA private key, 2048 bit long modulus (2 primes)
..........................................+++++
...................................................+++++
e is 65537 (0x010001)
```

# Extracting the Public Key from the Key Pair

```
$ openssl rsa -in demo.key -pubout -out demo_public.key
writing RSA key
```

# Creating a CSR

```
$ openssl req -new -key demo.key -out demo.csr
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:IN
State or Province Name (full name) [Some-State]:TN
Locality Name (eg, city) []:Chennai
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Demo
Organizational Unit Name (eg, section) []:Demo
Common Name (e.g. server FQDN or YOUR name) []:*.demo.com
Email Address []:abc@examp.com

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
```

# Verifying CSR 

- Before Passing the CSR to the Certificate Authority, verify the CSR using the below command.

```
$ openssl req -text -in demo.csr -noout -verify
Certificate Request:
    Data:
        Version: 1 (0x0)
        Subject: C = IN, ST = TN, L = Chennai, O = Demo, OU = Demo, CN = *.demo.com, emailAddress = abc@examp.com
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                RSA Public-Key: (2048 bit)
                Modulus:
                    00:d0:f0:03:50:28:e3:5d:0a:9c:98:57:80:13:8a:
                    8e:8d:9c:c5:89:a3:3c:dc:5d:c1:7f:d3:f3:a7:4f:
                    8b:1c:9e:69:86:70:88:14:c0:44:aa:6e:ca:de:c1:
                    81:58:1e:57:a4:ca:c6:1b:49:6a:9f:85:c8:03:c2:
                    ee:de:6b:6a:b5:8d:ee:9e:b0:bf:74:b5:1e:e3:74:
                    4e:47:41:53:80:02:a5:3a:6e:08:ae:6f:59:18:8c:
                    7a:d4:23:28:a1:09:86:a2:b6:38:d6:25:df:13:f1:
                    92:50:47:11:5a:18:c8:f8:03:ea:92:bc:5c:74:71:
                    36:5a:bf:74:93:29:64:c2:0d:0e:b2:69:0b:ca:30:
                    73:fa:17:14:29:42:24:49:7f:a6:05:57:c9:d4:ac:
                    b3:99:62:8c:85:d8:76:e0:9d:e7:c6:43:62:70:c0:
                    68:86:fd:2e:51:0d:c5:8a:87:c6:5c:ce:e8:82:d0:
                    b3:35:ca:82:e1:ed:51:a1:cd:98:71:49:da:87:37:
                    c1:63:bd:8e:92:05:30:e7:20:ed:6f:70:36:f9:13:
                    fa:46:ca:85:72:e2:93:b0:73:56:a5:5c:08:50:0f:
                    42:3e:bb:04:dd:d7:d0:4a:36:b7:e8:fa:35:5c:84:
                    27:3b:52:67:4d:9d:6f:03:b8:71:ef:4c:60:0e:48:
                    b2:65
                Exponent: 65537 (0x10001)
        Attributes:
            a0:00
    Signature Algorithm: sha256WithRSAEncryption
         b2:4d:a4:4d:1f:fe:c4:ff:bb:c0:28:39:0f:bd:a5:07:19:7a:
         e7:83:f9:8f:b8:67:53:30:d1:2e:72:23:3c:6c:24:d6:62:37:
         0a:bf:a3:33:6e:16:78:ac:71:8c:be:e1:a9:d2:c1:ba:35:ee:
         8c:f6:ab:8b:d0:a6:4e:46:65:73:8a:19:9a:0c:d4:63:4b:30:
         42:43:c8:65:ce:f0:c3:4d:e9:2c:b4:32:2d:2d:c2:4d:f1:78:
         27:4e:44:45:94:ed:ea:c3:9b:46:ea:7b:7c:54:f2:bd:3f:5e:
         42:a2:27:93:24:f9:79:e3:12:d9:6f:72:e0:d7:47:db:a3:1d:
         4e:08:25:0c:72:9e:81:a4:71:e9:f9:ee:0d:e7:08:05:58:eb:
         4a:84:de:1e:ff:ba:35:3f:f8:9f:8c:95:ca:bf:c7:0a:b5:c9:
         c7:96:36:df:2f:23:13:e8:91:98:79:ae:2e:c8:c1:8f:04:6e:
         6b:d0:73:10:2d:96:78:54:18:4f:04:c3:57:73:d3:a6:3c:e9:
         c6:02:11:27:32:79:b3:0c:e9:8c:24:b4:2d:4c:0e:3a:e8:70:
         36:0f:71:2e:3f:2b:f6:4a:eb:d8:f0:80:28:62:97:bf:cc:28:
         1b:f5:c2:57:f2:bb:a6:af:be:45:05:5f:fb:f1:9d:98:2b:90:
         ae:14:e4:93
verify OK
```

# Signing Certificate (Making Self Signed Certificate)

```
$ openssl x509 -in demo.csr -out demo.csr -req -signkey demo.key -days 365
Signature ok
subject=C = IN, ST = TN, L = Chennai, O = Demo, OU = Demo, CN = *.demo.com, emailAddress = abc@examp.com
Getting Private key
```

Access Certificate Manager in Windows 10 using the below command in Run Terminal

certmgr.msc

![image](https://user-images.githubusercontent.com/12709834/135869386-b23f7f3f-1ade-4733-8848-7020aef293bc.png)
