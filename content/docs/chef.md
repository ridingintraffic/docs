---
layout: single
title: chef 
description: chef notes
---

# chef 

```
$ kitchen list
$ kitchen converge ;# creates the vagrant box from the kitchen.yml
$ kitchen exec -c whoami ;#fire a command from insid ethe vagrant box

$ kitchen verify ;# runs the tests that are configured
$ kitchen login ; # logs into the box directly gives a shell
```
