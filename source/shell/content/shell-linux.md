---
title: "LINUX"
lastmod: "2022-12-10 12:04:58"
categories: ["Shell"]
draft: false
toc: true
---

## GNU/Linux {#gnu-linux}

“GNU”这个名字是“GNU's Not Unix”的递归首字母缩写词。

GNU 是一个类 Unix 操作系统。它是由多个应用程序、系统库、开发工具乃至游戏构成的程序集合。称为 GNU 工程。

类 Unix 操作系统中用于资源分配和硬件管理的程序称为“内核”。GNU 所用的典型内核是 Linux。该组合叫做 GNU/Linux 操作系统。

GNU 自己的内核，The Hurd，开始于 1990 年（早于 Linux）。


## TTY {#tty}

控制台、终端、虚拟终端是一类输入输出设备的总称，拥有将用户指令输入给操作系统和将操作系统返回结果输出给用户的基本功能;

-   电传打字机（teletypewriter，缩写为 tty）是该类设备的具体实例。
-   终端模拟器（Terminal Emulator）是一类应用程序，用来模拟终端设备的功能.
-   伪终端（pseudo tty，缩写为 pty）是 UNIX/Linux 内核中驱动程序模块，是一个软件中间层，用于克服真实终端设备在现代应用场景中的不足。

串行端口（Serial Port）,串口的最大用途就是连接终端，计算机就把连接到串口的外设看作字符设备，外设称为“串口终端（Serial Port Terminal）”

-   在 Linux 系统中对应着设备/dev/ttyS1、/dev/ttyS2......等，Windows 下 COM1、COM2 概念相对应.

一台 PC 通常只有一套键盘和显示器，也就是只有一套物理终端设备.

-   Linux 内核将这一套键盘和显示器映射为 6 个字符终端设备文件，即/dev/tty1~tty6，称为“虚拟终端（Virtual Terminal）”，可通过 Ctrl-Alt-F1~F6 切换.
-   /dev/tty0 则指向用户当前正在使用的虚拟终端，如用户切换到/dev/tty4，那么/dev/tty0 就指向/dev/tty4。

终端模拟器（Terminal Emulator）是基于系统中已有的键盘、显示驱动而构建的图形界面程序，其根本用途只有一个——模拟电子视频终端的功能.

-   xterm 是 X11 图形窗口系统（被很多 Linux、UNIX 发行版采用）下的标配终端模拟器。

终端、虚拟终端、串口终端是有真实物理设备相对应的，一方面数量有限制，另一方面在远程执行主机上的应用程序（比如 sh、vi 等）时，

-   终端虽然通过基于 TCP/IP 协议的 socket 接口与主机连接了，但远程主机上的程序的标准输入、标准输出、标准错误无法关联到 socket 上，
-   同时主机上的程序只有对终端设备操作才能正常运行，socket 无法提供和终端设备兼容的 IO 模式、

伪终端（pseudo tty，缩写为 pty）就是这样一个中间层，是 UNIX/Linux 内核中一对双向互联的设备，分为主设备（pty master）和从设备（pty slave），也称作“伪终端对（pty pair）”

-   pty 从设备表现与真实终端设备完全一致，.
-   在实际应用场景中，“代理程序”可能是 ssh/telnet server，目标程序可能是 shell，本地用户就通过本地主机 ssh/telnet 客户端程序远程登录到主机 shell。


## arp-scan {#arp-scan}

```sh

arp_scan (){
git clone https://github.com/royhills/arp-scan.git

cd arp-scan
autoreconf –install
./configure
make
make check
make install
}
```


## auto-login {#auto-login}

```sh

# 1
/etc/init/tty.conf
exec /sbin/mingetty --autologin root $TTY
# 2)
/etc/gdm/custom.conf
[daemon]
AutomaticLoginEnable=true
AutomaticLogin=root
TimedLoginEnable=true
[security]
AllowRoot=true
```


## bit {#bit}

```sh
getconf LONG_BIT
file /sbin/init
uname -a  # x86_64 :64bit
```


## crontab {#crontab}

```sh

contab(){
#!/bin/sh
 kill -9 $(lsof | grep deleted | awk '{print $2}')
}
```


## grub2 {#grub2}

```sh
grub --version
grub-install -v
update-grub

ub-install  --root-directory=/ /dev/sda  #--no-floppy
grub-mkconfig -o /boot/grub/grub.cfg


# 处理能引导 windos 但无法引导 linux
wajig update grub
wajig install os-prober
#aptitude 是文本界面的最好工具功能强大完全能够替代 apt-get、dselect。
#synaptic 则是图形方式下一款强大的包管理工具他是 apt-get 的 GTK 前端。
#wajig （Gnome GUI）比较新，有待发展。
```


## iptables {#iptables}

```sh
iptables -A INTPUT/OUTPUT -p tcp --dport 端口号-j DROP

#debian
iptables-save > aaa
iptables-restore < aaa

#redaht/Centos
/etc/sysconfig/iptables 
etc/sysconfig/iptables-config # 将里面的 IPTABLES_SAVE_ON_STOP="no", 这一句的 "no" 改为 "yes" .
# 这样每次服务在停止之前会自动将现有的规则保存在 /etc/sysconfig/iptables 
```


## LVM {#lvm}

逻辑卷管理。使用 LVM 的机制是这样的：
  首先把硬盘分区或者整块硬盘标记为一个物理卷（PV），然后再创建一个卷组（VG），
    \\\\把一个或多个物理卷加入卷组，最后对卷组进行分区，每一个分区称为一个逻辑卷（LV）。
  LVM 的优点就是可以随时向卷组中添加物理卷扩展卷组的大小，以可以动态调整逻辑卷的大小。
  LVM 既可以搭配 MBR 使用，也可以搭配 GPT 使用。


## lost_power_fsck {#lost-power-fsck}

```sh
cat > /etc/sysconfig/autofsck <<'EOF'
AUTOFSCK_DEF_CHECK=yes
PROMPT=yes
EOF

# /etc/fstab 文件的根目录最后改成 1
```


## MBR&lt;=&gt;GPT {#mbr-gpt}


### gdisk {#gdisk}

```sh
# mbr 分区格式最大只支持 2TB 容量的硬盘，并且由于整个 mbr 分区只有 512KB 大小，最多只能支持 4 个主分区的局限性。

# 备份 mbr 分区
# 磁盘的结构:前 512K 的内容是 MBR+分区表。
sudo dd if=/dev/sda of=/root/mbr.grub bs=512 count=1

# 分区格式转换
gdisk /dev/sda

# 用 mbr 和第一个分区之间的空间分配一个 bios boot 分区
n 新建一个分区
选择一个未使用的分区 ID
分区范围选择 34-2047 扇区
设置分区类型为 ef02
最后按 w 保存分区并转换

# 重新安装 grub 的 bootloader
# 原来的 bootloader 在 mbr 内，转换之后，bootloader 删除了，需要重新将 bootloader 安装到新建的 bios boot 分区
grub-install /dev/sda
# NOTE
# 为了避免与其他系统的差异性，安装好 bootloader 后将 bios boot 分区删除。
```


### parted {#parted}

直接使用 parted 命令即可

```sh
$ parted /dev/sdb
(parted) mklabel
New disk label type? gpt # msdos
```


## pam.d {#pam-dot-d}

```sh
/etc/pam.d/common-password
first line:enforce_for_root ---  root cannot change user password

/lib/i386-linux-gnu/security	#lib location
```


## partition {#partition}


### grub {#grub}

grub 是要在 mbr 里写东西的，但 446 字节的机器码也干不了太多东西，只是负责把后续的内容加载到内存在执行而已。这个写到 mbr 的是 stage1，它加载的是写在 mbr 之后 62 个扇区中的 stage1.5
（因为过去磁盘是按磁道还划分分区的，一个磁道 63 个扇区，因为 mbr 占据了第一个磁道的第一个扇区，所以第一个分区只能从第二个磁道开始，
  \\\\在 mbr 和第一个分区之间就留下了 62 个扇区的空间，62\*512byte＝31KB）。

mbr 之前说了容量太小没法放下识别文件系统的代码，只能以计算扇区绝对偏移的方法加载 stage1.5，但 31KB 的 stage1.5 就足够了
（但基本也只够一种类型的文件系统，所以 stage1.5 是有好几个，分别对应 ext4，xfs 等等，在 grub 安装时根据需要写入.
  \\\\随便一提，正是因为 GPT 分区表占用了后 62 个扇区的相当一部分位置，导致空间不够写下 stage1.5，所以需要额外分出一个非常小的分区来存放）。

stage1.5 可以识别文件系统，然后根据安装时硬写到里面的系统路径（hexdump 可以看到）找到 stage2，
  \\\\然后这个 stage2 才是真正负责干活的，它会读取 grub.cfg 并生成启动菜单，然后根据你的选择加载内核并把执行权限转过去，完成启动。


### MBR {#mbr}

全新硬盘（未初始化）装系统之前，必须对齐进行分区，硬盘分区初始化的格式包括 MBR 和 GPT 两种。当然对于基于 PowerPC 的 Mac 电脑还有专门的 Apple 分区图.

MBR 的全称是 Master Boot Record（主引导记录）,主引导扇区是硬盘的第一扇区。
它由三个部分组成，主引导记录 MBR、硬盘分区表 DPT 和硬盘有效标志。

-   第一部分是 MBR，在总共 512 字节的主引导扇区里 MBR 占 446 个字节，偏移地址 0000H--0088H），它负责从活动分区中装载，并运行系统引导程序；
-   第二部分是 Partition table 区（DPT 分区表），占 64 个字节；分区表偏移地址为 01BEH--01FDH，每个分区表项长 16 个字节，分别对应 MBR 的四个主分区。
-   第三部分是 Magic number，占 2 个字节。Magic number 也就是结束标志字，偏移地址 01FE--01FF 的 2 个字节，\*\*固定为 55AA\*\*，如果该标志错误系统就不能启动。

MBR 最大支持 2.2TB 磁盘，它无法处理大于 2.2TB 容量的磁盘。

引导代码占 MBR 分区的前 440 字节,440~445 字节，是磁盘签名，可以写 0（windows 下用，linux 下不用）


### MBR 签名 {#mbr-签名}

可以理解为主引导扇区的磁盘签名。在系统在初始化硬盘时随机生成的一个必要的标签。
Note：一块硬盘如果不是系统引导盘，MBR 扇区中可以没有引导程序，但是绝对不能没有磁盘签名。


### GPT {#gpt}

GPT 的全称是 Globally Unique Identifier Partition Table，意即 GUID 分区表;

它的推出是和 UEFI BIOS 相辅相成的;鉴于 MBR 的磁盘容量和分区数量已经不能满足硬件发展的需求，GPT 首要的任务就是突破了 2.2T 分区的限制，最大支持 18EB 的分区。

而在分区数量上，GPT 会为每一个分区分配一个全局唯一的标识符，理论上 GPT 支持无限个磁盘分区，不过在 Windows 系统上由于系统的限制，最多只能支持 128 个磁盘分区，基本可以满足所有用户的存储需求。
  \\\\在每一个分区上，这个标识符是一个随机生成的字符串，可以保证为地球上的每一个 GPT 分区都分配完全唯一的标识符。

而在安全性方面，GPT 分区表也进行了全方位改进。在早期的 MBR 磁盘上，分区和启动信息是保存在一起的。如果这部分数据被覆盖或破坏，事情就麻烦了。
  \\\\相对的，GPT 在整个磁盘上保存多个这部分信息的副本，因此它更为健壮，并可以恢复被破坏的这部分信息。GPT 还为这些信息保存了循环冗余校验码（CRC）以保证其完整和正确——如果数据被破坏，GPT 会发觉这些破坏，并从磁盘上的其他地方进行恢复。

1、保留 MBR，GPT 的分区方案，硬盘的第一个物理扇区，仍然是一个前面讲过的 MBR，这个 MBR 主要是出于软件兼容性的考虑，对 GPT 分区方案本身来讲，其实没有啥意义。
2、GPT 分区表头，这个在保留 MBR 之后，也就是占用第二个物理扇区，GPT 分区表头中，定义了分区的数量，基本上，你可以认为 GPT 分区的数量是没有限制的；
3、GPT 分区表，从第三个扇区开始，是实际的分区表。请注意：每个扇区可以保存 4 个分区信息，说明每个分区的分区信息占用的空间是 128 个字节。
4、从 3 中，我们知道每个分区的信息占用了四分之一个扇区，也就是 128 字节的空间，对比一下 MBR 分区方案中，每个分区的信息只有 16 个字节，
  \\\\所以 GPT 分区方案，有充足的空间去存储分区的开始位置及总的容量等，基本上，不用考虑对分区容量的限制。
5、从 3 中，我们知道，GPT 分区方案，分了多少个区，就在分区表中有多少个分区信息。然而实际情形并不是这样，
  \\\\事实上，如图中所示：如果你使用 windows 操作系统，通常 GPT 分区表占用 32 个扇区的空间，可以保存 128 个分区信息，用不到的空间会被保留，实际使用了多少分区信息与保留了多少分区信息，
  \\\\在 2 中的 GPT 分区表头中设置。我们的电脑，通常不会有超过 10 个的分区，所以 GPT 分区表中的空间，90%以上都是保留空间，其实就是被浪费了。


### UEFI BIOS {#uefi-bios}

UEFI 的全称是 Unified Extensible Firmware Interface，意即统一可扩展固件接口

UEFI 和 GPT 是相辅相成的，二者缺一不可，要想使用 GPT 分区表则必须是 UEFI BIOS 环境。

-   UEFI 于用户而言最典型的特征就是使用了图形化界面,可以很好的查看和设置 BIOS 的相关选项和功能。
-   UEFI 相比传统 BIOS，还提供了文件系统的支持，它能够直接读取 FAT、FAT32 分区中的文件，新的 UEFI 主板基本都提供了截屏功能，这些截屏图片都可以存储在 U 盘当中。
-   在 UEFI 下运行应用程序，这类程序文件通常以 efi 结尾。利用 UEFI 可以直接识别 FAT 分区中的文件，又有可直接在其中运行应用程序。
    -   \\\\我们就可以将 Windows 安装程序做成 efi 类型应用程序，然后把它放到任意 FATA 分区中直接运行即可。

备注\*NOTE\*：
    \\\\主板为了兼容 MBR 分区表，一般会提供 Legacy BIOS 和 UEFI BIOS 启动模式选项，如果要使用 UEFI 模式安装 Windows，就必须开启 UEFI 启动模式。
    \\\\一个计算机是使用 BIOS 还是使用 UEFI，是由这台计算机的主板决定的
    \\\\格式化，就是指的在硬盘分区上创建文件系统的过程。
    \\\\什么是文件系统呢？简单说，就是数据（具体说，就是文件和目录结构）如何在分区的空间上保存的规范。
    \\\\格式化后的分区，虽然在电脑中已经看不到了，但其原来的数据 99%以上并没有被真正删除，使用数据恢复软件，能够被轻易的找回。


### DiskGenius {#diskgenius}

MBR 分区与 GPT 分区的相互转换
  \\\\点击“硬盘”菜单并选择“转换分区表类型为 GUID 格式”。

从分区中恢复文件
  \\\\“恢复文件”
  \\\\“完整恢复”


## pam.d - faillock {#pam-dot-d-faillock}

```cfg
auth     requisite     pam_faillock.so preauth audit deny=3 even_deny_root unlock_time=60
auth     [default=die] pam_faillock.so authfail audit deny=3 even_deny_root unlock_time=60
account  required      pam_faillock.so
---

auth     required       pam_securetty.so
auth     required       pam_env.so
auth     required       pam_nologin.so
# optionally call: auth requisite pam_faillock.so preauth deny=4 even_deny_root unlock_time=1200
# to display the message about account being locked
auth     [success=1 default=bad] pam_unix.so
auth     [default=die]  pam_faillock.so authfail deny=4 even_deny_root unlock_time=1200
auth     sufficient     pam_faillock.so authsucc deny=4 even_deny_root unlock_time=1200
auth     required       pam_deny.so
account  required       pam_unix.so
auth     required       pam_nologin.so
auth     required       pam_faillock.so preauth silent deny=4 even_deny_root unlock_time=1200
# optionally use requisite above if you do not want to prompt for the password
# on locked accounts, possibly with removing the silent option as well
auth     sufficient     pam_unix.so
auth     [default=die]  pam_faillock.so authfail deny=4 even_deny_root unlock_time=1200
auth     required       pam_deny.so
account  required       pam_faillock.so
# if you drop the above call to pam_faillock.so the lock will be done also
# on non-consecutive authentication failures
account  required       pam_unix.so
password required       pam_unix.so shadow
session  required       pam_selinux.so close
session  required       pam_loginuid.so
session  required       pam_unix.so
session  required       pam_selinux.so openh
```


## rsync {#rsync}

```sh

-z 传输前进行压缩
-v 显示命令执行详细信息
-r 递归拷贝目录
-a 选项亦包含递归的作用，因而可以替代-r 选项。

_rsync  (){
rsync [OPTION]... SRC DEST
rsync [OPTION]... SRC [USER@]host:DEST
rsync [OPTION]... [USER@]HOST:SRC DEST

rsync -a /data  /backup
rsync -avz test.a  foo:src
rsync -avz foo:src/bar  /data
rsync -av root@192.168.78.192:www /databack

# use ssh tunnel
rsync -avz -e ssh /root/temp/ lx@192.168.1.103:/home/lx/tmp/

# --progress 选项可以显示同步的进度，包括文件传输完成进度、传输速率信息：
rsync -avz --progress /var/opt/lx/ /root/temp/

# 默认情况下 rsync 采用增量拷贝，这样能节省带宽，在所同步文件不大的情况下，我们可以通过 -W 选项实现全拷贝：e
rsync -avzW /var/opt/lx/ /root/temp/

# --include 和 --exclude 选项，可以帮助我们完成只同步特定文件的目的，例如以下只同步以 'a' 开头的文件：a
rsync -avz --include 'a*' --exclude '*' /var/opt/lx/ /root/temp/
}
```


## route {#route}

```sh

_route(){
route add -net 192.168.0.0 netmask 255.255.255.0 dev eth0
route del -net 192.168.0.0 netmask 255.255.255.0 dev eth0
  route add default gw 192.168.1.2

  dns /etc/resolve.conf
}
```


## service {#service}

```sh
## 查看
service --status-all
chkconfig --list

ps -aux ｜ grep xxx
service vsftpd status
chkconfig vsftpd status

##启动
# setup 启动配置
chkconfig –level 345 vsftpd off/on  (#保证机器重启后 vsftpd 服务还在
service httpd start

netstat -ntlp	看下对应端口有没有启动

chkconfig –add xxx ( 注意：服务脚本必须存放在 /etc/init.d/目录下)
chkconfig –del XXX
```


## syslinux {#syslinux}

```cfg

1：37：40 分别为 1 粗细 37 宽 40 高
#ffffffff #00000000 none 前景色和背景色 none 关闭 all 显示菜单框 std 字体阴影，#00000000 背景色透明必须#+8 位，前景色可以为#+6 位
menu color screen 37;40    #ffffffff #00000000 none 显示出左边框和上边框
menu color border 30;44    #00000000 #00000000 none 定义边框颜色
menu color title 1;36;44   #f01291a9 #00000000 none 定义 MENU TITLE 颜色
menu color unsel 37;44     #e01291a9 #00000000 none 定义菜单字体背景色
menu color hotkey 1;37;44  #e060CA00 #00000000 none 未选中热键的显示颜色
menu color hotsel 37;40    #9060CA00 #00000000 std 选中菜单当前热键的背景显示颜色
menu color sel 7;37;40     #e0712704 #20ff8000 all 选中菜单当前的背景颜色
menu color hotsel 1;7;37;40 #e0400000 #20ff8000 all 选中菜单当前热键颜色
menu color disabled 1;30;44 #60cccccc #00000000 none 未知
menu color scrollbar 30;44 #40000000 #00000000 std 滚动条

menu color tabmsg 31;40    #9060CA00 #00000000 none 标签
menu color cmdmark 1;36;40 #c000ffff #00000000 std
menu color cmdline 37;40   #c0ffffff #00000000 none tab 菜单编辑模式字体颜色
menu color pwdborder 30;47 #80ffffff #20ffffff std
menu color pwdheader 31;47 #80ff8080 #20ffffff std
menu color pwdentry 30;47  #80ffffff #20ffffff std
menu color timeout_msg 37;40 #e060CA00 #00000000 none 进入界面倒计时提示文字颜色
menu color timeout 1;37;40 #f060CA00 #00000000 none 进入界面倒计时秒数颜色
menu color help 37;40      #c0ffffff #00000000 none 菜单提示字体颜色
menu color msg07 37;40     #90ffffff #00000000 none

# 设置显示的背景和前景色。
0 = black 		8 = dark grey
1 = dark blue 	9 = bright blue
2 = dark green 	a = bright green
3 = dark cyan 	b = bright cyan
4 = dark red 	c = bright red
5 = dark purple d = bright purple
6 = brown 		e = yellow
7 = light grey 	f = white

# 选择亮色 (8-f) 为背景色，导致前景中相应的暗色 (0-7) 闪烁。
#  在串行控制台颜色不可见。
```


## update.rc.d {#update-dot-rc-dot-d}

```sh
# 进入/etc/init.d 目录，用 update-rc.d 命令将连接文件 startBlog 添加到启动脚本中去。/init.d/下要有 startBlog
update-rc.d startBlog defaults 99  #取值范围是 0-99。序号越大的越晚执行
update-rc.d -f startBlog remove  	#-f 选项表示强制执行
update-rc.d -f ＜basename＞ remove	# 删除所有级别中的开机自启动
update-rc.d [-n] name default [NN | SS KK]  #NN 表示执行序号（0-99），SS 表示启动时的执行序号，KK 表示关机时的执行序号

# 如果执行脚本 B 需要先执行脚本 A，如下设置（A的启动顺序比 B 的小，结束顺序比 B 的大）：
update-rc.d script_for_A defaults 80 20
update-rc.d script_for_B defaults 90 10

# E.G.
root@debian10:/etc/init.d# ln -s /etc/init.d/startvnc.sh /etc/rc5.d/S99startvnc //在图形化界面 init 5 处设置脚本链接。
root@debian10:/etc/init.d# update-rc.d startvnc.sh start 99 5  //图形化界面（init 5）才能 vnc 。
root@debian10:/etc/init.d# update-rc.d startvnc.sh defaults 99
```


## vga {#vga}

```sh

vga ()  {
 Color            640x480     800x600      1024x768     1280x1024
   256    8 bit     769         771           773          775
 32000   15 bit     784         787           790          793
 65000   16 bit     785         788           791          794
 16.7M   24 bit     786         789           792          795
}
```


## qume {#qume}

```sh
qemu-system-x86_64 -kernel vmlinuz -initrd new.cpio
qemu-system-x86_64 -kernel kernel/vmlinuz -initrd initrd/rootfs.cpio.xz -enable-kvm -append 'loglevel=3 text superuser showapps noutc noswap lst=onboot.lst mydata=mydata vga=0x317 waitusb=5:UUID="B4FE-5315" tce=UUID="B4FE-5315"'  $@
qemu-system-x86_64 -kernel kernel/vmlinuz -initrd initrd/initrd.gz -enable-kvm -m 1024 \
                   -append 'loglevel=3 text superuser showapps noutc noswap lst=onboot.lst mydata=mydata vga=0x317 waitusb=5:UUID="B4FE-5315" tce=UUID="B4FE-5315" console=tty0'  $@
```