---
layout: post
title: Enable Code Coverage for Linux Kernel
---
The idea is to document the steps to enable the test coverage of Linux Kernel 
using gcov/lcov/

The following steps will explain how to instrument the linux kernel. 

Enable the following in kernel config file 

```Kernel_Config
CONFIG_GCOV_KERNEL=y
CONFIG_ARCH_HAS_GCOV_PROFILE_ALL=y
CONFIG_GCOV_PROFILE_ALL=y
CONFIG_GCOV_FORMAT_4_7=y
```


