---
layout: post
title: Python Code to get public ip on the host system.
---

Code will identify the IP which can be used to communicate to the external network

```
from netifaces import interfaces, ifaddresses, AF_INET
from ipaddress import ip_address
for net in interfaces():
    try:
            for link in ifaddresses(net)[netifaces.AF_INET]:
                     print("%s is private : %s" % (link['addr'], ip_address(link['addr']).is_private))
    except KeyError as e:
             pass

```
