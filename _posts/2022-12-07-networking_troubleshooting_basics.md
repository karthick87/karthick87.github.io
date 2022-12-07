---
layout: post
title:  "Networking Troubleshooting Basics"
date:   2022-12-07 10:00:00 +0900
categories: update
---

# Networking Basics
```
[5.59 sec] > Test-NetConnection google.com


ComputerName           : google.com
RemoteAddress          : 142.250.74.142
InterfaceAlias         : Ethernet 4
SourceAddress          : 10.83.247.45
PingSucceeded          : True
PingReplyDetails (RTT) : 433 ms

[7.05 sec] > Test-NetConnection google.com -Port 443


ComputerName     : google.com
RemoteAddress    : 142.250.74.142
RemotePort       : 443
InterfaceAlias   : Ethernet 4
SourceAddress    : 10.83.247.45
TcpTestSucceeded : True
```
