---
title: "TOOLS"
lastmod: "2022-12-10 11:53:31"
categories: ["Shell"]
draft: false
toc: true
---

## VMwareTools {#vmwaretools}

```sh
#install vmwaretools  need linux-image headers

Vm->install vmware-tools

apt-get install gcc
or install gcc make
apt-get update
apt-get install build-essential

#!!!!重要 install kernel-header (主要是为了解决 What is the location of the directory of C header files that match your running kernel?问题)
apt-cache search linux-headers-$(uname -r)
apt-get install linux-headers-$(uname -r)

./vmware-install.pl
```


## VMwareUdisk {#vmwareudisk}

```sh
add send disk(sata) as boot disk，change bios queen；
del Udisk for error "\\.\PhysicalDrive1"

VMwareClearDisk
~/.cache/vmware/drag_and_drop$ du -d 1 -h
```