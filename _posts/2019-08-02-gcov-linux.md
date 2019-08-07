---
layout: post
title: Enable Code Coverage for Linux Kernel
---
The idea is to document the steps to enable the test coverage of Linux Kernel 
using gcov/lcov/

The following steps will explain how to instrument the linux kernel. 

Enable the following in kernel config file 

``` 
CONFIG_GCOV_KERNEL=y
CONFIG_ARCH_HAS_GCOV_PROFILE_ALL=y
CONFIG_GCOV_PROFILE_ALL=y
CONFIG_GCOV_FORMAT_4_7=y
```

Bydefault debugfs will be enabled on Linux, if not please enable the same

``` 
CONFIG_DEBUG_FS=y
```

Compile the kernel and boot the system with latest compiled kernel.

``` 
make -j <no of thread>
make modules_install
make install
reboot
```
Once the system booted with gcov enable we have the following files listed in debugfs.

```
/sys/kernel/debug/gcov
```
under gcov we will have the kernel source files with extention .gcda and .gcno. 

Install lcov, gcov is part of gcc.
``` 
yum install lcov
```

To reset the counters
```
lcov --zerocounters
```

Run all your test to check the coverage, corresponding files in debugs/gcov will be update with the coverage. 

Generate coverage info and generate webpage
```
lcov -c -o /tmp/kern.info
genhtml -o /var/www/html /tmp/kern.info 
```

To view data on browser, start the httpd server
```
systemctl start httpd
```

