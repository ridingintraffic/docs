---
layout: single
title:  ssh 
description: ssh notes
---

# ssh 
SSH Proxy
```
ssh -o ProxyCommand='ssh -W %h:%p user@bastion' user@target
```

~/.ssh/config 
```
Host bastion
  Hostname my-bastion-host.example.com

Host my_server
  Hostname 10.0.1.18
  ProxyCommand ssh bastion -W %h:%p
```
 then you can use:
` $ ssh my_server`

