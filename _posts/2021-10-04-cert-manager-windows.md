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

Generating a Key Pair 

It contains both public and private key

```
$ openssl genrsa -out demo.key 2048
Generating RSA private key, 2048 bit long modulus (2 primes)
..........................................+++++
...................................................+++++
e is 65537 (0x010001)
```

Extracting the Public Key

```
$ openssl rsa -in demo.key -pubout -out demo_public.key
writing RSA key
```

Creating a CSR

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

Access Certificate Manager in Windows 10 using the below command in Run Terminal

certmgr.msc

![image](https://user-images.githubusercontent.com/12709834/135869386-b23f7f3f-1ade-4733-8848-7020aef293bc.png)
