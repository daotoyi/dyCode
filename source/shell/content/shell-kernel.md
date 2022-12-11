---
title: "KERNEL"
lastmod: "2022-12-10 12:16:57"
categories: ["Shell"]
draft: false
toc: true
---

## compile {#compile}

```bash
make mrproper	#清除环境
make menuconfig
make dep

make -j4	#编译内核和模块
make modules_install	#安装模块
make install	#安装内核

CONCURRENCY_LEVEL=`getconf _NPROCESSORS_ONLN` INSTALL_MOD_STRIP=1 make-kpkg \
--append-to-version $VER \
  #也是一种版本信息，它不仅出现在 deb 安装包的文件名里，也会影响到 kernel 的名称。
--revision $REV \
  #会给生成的 deb 文件加上一个版本信息。这个参数只是影响到文件名，如果不指定，默认会是“10.00.Custom”
--initrd \
  #会让 make-kpkg 自动帮我们生成 initramfs
--rootcmd fakeroot \
  #用普通用户来执行 make-kpkg，需要加上 fakeroot 运行
kernel_image \
  #表示生成内核和默认模块的安装包
modules_image \
kernel_headers
  #make-kpkg 会生成一个内核头文件的安装包。


# 1)Ubuntu16.06/Debkian
sudo apt-get install ncurses-dev
sudo apt-get install libelf-dev	#apt-get=apt
sudo apt-get libssl-dev #openssh


# EG)：====================
sudo apt-get install libncurses5-dev binutils-dev linux-source
sudo apt-get install fakeroot build-essential crash kernel-wedge kernel-package

apt-get source linux-image-$(uname -r)

make menuconfig	#cp /boot/config-`uname –r`.config
#make-kpkg clean 清理源代码树
#make-kpkg	清洁
export CONCURRENCY_LEVEL=3
fakeroot make-kpkg --append-to-version "-Daoyikernel" --revision "1" --initrd kernel_image kernel_headers
  sudo CONCURRENCY_LEVEL=4 make-kpkg --initrd kernel-image kernel_headers
  #4相当于多线程，make -j4

### ---------

Q:fakeroot: nested operation not yet supported
A:define in *.bb,directly make-kpkg
```


## makefile {#makefile}

```bash
###shell 文件内调用makefile
#!/bin/bash
cd ctemplate-2.1
./configure
sudo make -f install
cd ../
cd TemplateProcesser
make

###makefile文件内调用shell脚本文件
SHELL := /bin/bash
test:
@pwd
cd ./TemplateProcesser && pwd
sh ./build.sh
@pwd

###build.sh为shell脚本文件。
/usr/bin/perl *.pl	#调用perl文件
/usr/bin/env *.py	#调用python文件
```