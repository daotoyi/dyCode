+++
lastmod = "2022-12-11 10:53:38"
categories = ["Shell"]
draft = false
toc = true
+++

## Linux {#linux}


### GNU/Linux {#gnu-linux}

“GNU”这个名字是“GNU's Not Unix”的递归首字母缩写词。

GNU 是一个类 Unix 操作系统。它是由多个应用程序、系统库、开发工具乃至游戏构成的程序集合。称为 GNU 工程。

类 Unix 操作系统中用于资源分配和硬件管理的程序称为“内核”。GNU 所用的典型内核是 Linux。该组合叫做 GNU/Linux 操作系统。

GNU 自己的内核，The Hurd，开始于 1990 年（早于 Linux）。


### TTY {#tty}

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


### arp-scan {#arp-scan}

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


### auto-login {#auto-login}

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


### bit {#bit}

```sh
getconf LONG_BIT
file /sbin/init
uname -a  # x86_64 :64bit
```


### crontab {#crontab}

```sh

contab(){
#!/bin/sh
 kill -9 $(lsof | grep deleted | awk '{print $2}')
}
```


### grub2 {#grub2}

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


### iptables {#iptables}

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


### LVM {#lvm}

逻辑卷管理。使用 LVM 的机制是这样的：

首先把硬盘分区或者整块硬盘标记为一个物理卷（PV），然后再创建一个卷组（VG），把一个或多个物理卷加入卷组，最后对卷组进行分区，每一个分区称为一个逻辑卷（LV）。

LVM 的优点就是可以随时向卷组中添加物理卷扩展卷组的大小，以可以动态调整逻辑卷的大小。

LVM 既可以搭配 MBR 使用，也可以搭配 GPT 使用。


### lost_power_fsck {#lost-power-fsck}

```sh
cat > /etc/sysconfig/autofsck <<'EOF'
AUTOFSCK_DEF_CHECK=yes
PROMPT=yes
EOF

# /etc/fstab 文件的根目录最后改成 1
```


### MBR&lt;=&gt;GPT {#mbr-gpt}


#### gdisk {#gdisk}

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


#### parted {#parted}

直接使用 parted 命令即可

```sh
$ parted /dev/sdb
(parted) mklabel
New disk label type? gpt # msdos
```


### pam.d {#pam-dot-d}

```sh
/etc/pam.d/common-password
first line:enforce_for_root ---  root cannot change user password

/lib/i386-linux-gnu/security	#lib location
```


### partition {#partition}


#### grub {#grub}

grub 是要在 mbr 里写东西的，但 446 字节的机器码也干不了太多东西，只是负责把后续的内容加载到内存在执行而已。这个写到 mbr 的是 stage1，它加载的是写在 mbr 之后 62 个扇区中的 stage1.5
（因为过去磁盘是按磁道还划分分区的，一个磁道 63 个扇区，因为 mbr 占据了第一个磁道的第一个扇区，所以第一个分区只能从第二个磁道开始， 在 mbr 和第一个分区之间就留下了 62 个扇区的空间，62\*512byte＝31KB）。

mbr 之前说了容量太小没法放下识别文件系统的代码，只能以计算扇区绝对偏移的方法加载 stage1.5，但 31KB 的 stage1.5 就足够了 （但基本也只够一种类型的文件系统，所以 stage1.5 是有好几个，分别对应 ext4，xfs 等等，在 grub 安装时根据需要写入. 随便一提，正是因为 GPT 分区表占用了后 62 个扇区的相当一部分位置，导致空间不够写下 stage1.5，所以需要额外分出一个非常小的分区来存放）。

stage1.5 可以识别文件系统，然后根据安装时硬写到里面的系统路径（hexdump 可以看到）找到 stage2，然后这个 stage2 才是真正负责干活的，它会读取 grub.cfg 并生成启动菜单，然后根据你的选择加载内核并把执行权限转过去，完成启动。


#### MBR {#mbr}

全新硬盘（未初始化）装系统之前，必须对齐进行分区，硬盘分区初始化的格式包括 MBR 和 GPT 两种。当然对于基于 PowerPC 的 Mac 电脑还有专门的 Apple 分区图.

MBR 的全称是 Master Boot Record（主引导记录）,主引导扇区是硬盘的第一扇区。
它由三个部分组成，主引导记录 MBR、硬盘分区表 DPT 和硬盘有效标志。

-   第一部分是 MBR，在总共 512 字节的主引导扇区里 MBR 占 446 个字节，偏移地址 0000H--0088H），它负责从活动分区中装载，并运行系统引导程序；
-   第二部分是 Partition table 区（DPT 分区表），占 64 个字节；分区表偏移地址为 01BEH--01FDH，每个分区表项长 16 个字节，分别对应 MBR 的四个主分区。
-   第三部分是 Magic number，占 2 个字节。Magic number 也就是结束标志字，偏移地址 01FE--01FF 的 2 个字节，\*\*固定为 55AA\*\*，如果该标志错误系统就不能启动。

MBR 最大支持 2.2TB 磁盘，它无法处理大于 2.2TB 容量的磁盘。

引导代码占 MBR 分区的前 440 字节,440~445 字节，是磁盘签名，可以写 0（windows 下用，linux 下不用）


#### MBR 签名 {#mbr-签名}

可以理解为主引导扇区的磁盘签名。在系统在初始化硬盘时随机生成的一个必要的标签。

Note：一块硬盘如果不是系统引导盘，MBR 扇区中可以没有引导程序，但是绝对不能没有磁盘签名。


#### GPT {#gpt}

GPT 的全称是 Globally Unique Identifier Partition Table，意即 GUID 分区表;

它的推出是和 UEFI BIOS 相辅相成的;鉴于 MBR 的磁盘容量和分区数量已经不能满足硬件发展的需求，GPT 首要的任务就是突破了 2.2T 分区的限制，最大支持 18EB 的分区。

而在分区数量上，GPT 会为每一个分区分配一个全局唯一的标识符，理论上 GPT 支持无限个磁盘分区，不过在 Windows 系统上由于系统的限制，最多只能支持 128 个磁盘分区，基本可以满足所有用户的存储需求。 在每一个分区上，这个标识符是一个随机生成的字符串，可以保证为地球上的每一个 GPT 分区都分配完全唯一的标识符。

而在安全性方面，GPT 分区表也进行了全方位改进。在早期的 MBR 磁盘上，分区和启动信息是保存在一起的。如果这部分数据被覆盖或破坏，事情就麻烦了。相对的，GPT 在整个磁盘上保存多个这部分信息的副本，因此它更为健壮，并可以恢复被破坏的这部分信息。GPT 还为这些信息保存了循环冗余校验码（CRC）以保证其完整和正确——如果数据被破坏，GPT 会发觉这些破坏，并从磁盘上的其他地方进行恢复。

1、保留 MBR，GPT 的分区方案，硬盘的第一个物理扇区，仍然是一个前面讲过的 MBR，这个 MBR 主要是出于软件兼容性的考虑，对 GPT 分区方案本身来讲，其实没有啥意义。
2、GPT 分区表头，这个在保留 MBR 之后，也就是占用第二个物理扇区，GPT 分区表头中，定义了分区的数量，基本上，你可以认为 GPT 分区的数量是没有限制的；
3、GPT 分区表，从第三个扇区开始，是实际的分区表。请注意：每个扇区可以保存 4 个分区信息，说明每个分区的分区信息占用的空间是 128 个字节。
4、从 3 中，我们知道每个分区的信息占用了四分之一个扇区，也就是 128 字节的空间，对比一下 MBR 分区方案中，每个分区的信息只有 16 个字节，所以 GPT 分区方案，有充足的空间去存储分区的开始位置及总的容量等，基本上，不用考虑对分区容量的限制。
5、从 3 中，我们知道，GPT 分区方案，分了多少个区，就在分区表中有多少个分区信息。然而实际情形并不是这样，事实上，如图中所示：如果你使用 windows 操作系统，通常 GPT 分区表占用 32 个扇区的空间，可以保存 128 个分区信息，用不到的空间会被保留，实际使用了多少分区信息与保留了多少分区信息，在 2 中的 GPT 分区表头中设置。我们的电脑，通常不会有超过 10 个的分区，所以 GPT 分区表中的空间，90%以上都是保留空间，其实就是被浪费了。


#### UEFI BIOS {#uefi-bios}

UEFI 的全称是 Unified Extensible Firmware Interface，意即统一可扩展固件接口

UEFI 和 GPT 是相辅相成的，二者缺一不可，要想使用 GPT 分区表则必须是 UEFI BIOS 环境。

-   UEFI 于用户而言最典型的特征就是使用了图形化界面,可以很好的查看和设置 BIOS 的相关选项和功能。
-   UEFI 相比传统 BIOS，还提供了文件系统的支持，它能够直接读取 FAT、FAT32 分区中的文件，新的 UEFI 主板基本都提供了截屏功能，这些截屏图片都可以存储在 U 盘当中。
-   在 UEFI 下运行应用程序，这类程序文件通常以 efi 结尾。利用 UEFI 可以直接识别 FAT 分区中的文件，又有可直接在其中运行应用程序。
    -   我们就可以将 Windows 安装程序做成 efi 类型应用程序，然后把它放到任意 FATA 分区中直接运行即可。

备注\*NOTE\*：

-   主板为了兼容 MBR 分区表，一般会提供 Legacy BIOS 和 UEFI BIOS 启动模式选项，如果要使用 UEFI 模式安装 Windows，就必须开启 UEFI 启动模式。
-   一个计算机是使用 BIOS 还是使用 UEFI，是由这台计算机的主板决定的
-   格式化，就是指的在硬盘分区上创建文件系统的过程。
-   什么是文件系统呢？简单说，就是数据（具体说，就是文件和目录结构）如何在分区的空间上保存的规范。
-   格式化后的分区，虽然在电脑中已经看不到了，但其原来的数据 99%以上并没有被真正删除，使用数据恢复软件，能够被轻易的找回。


#### DiskGenius {#diskgenius}

MBR 分区与 GPT 分区的相互转换,

-   点击“硬盘”菜单并选择“转换分区表类型为 GUID 格式”。

从分区中恢复文件

-   “恢复文件”
-   “完整恢复”


### pam.d - faillock {#pam-dot-d-faillock}

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


### rsync {#rsync}

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


### route {#route}

```sh

_route(){
route add -net 192.168.0.0 netmask 255.255.255.0 dev eth0
route del -net 192.168.0.0 netmask 255.255.255.0 dev eth0
  route add default gw 192.168.1.2

  dns /etc/resolve.conf
}
```


### service {#service}

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


### syslinux {#syslinux}

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


### update.rc.d {#update-dot-rc-dot-d}

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


### vga {#vga}

```cfg

vga ()  {
 Color            640x480     800x600      1024x768     1280x1024
   256    8 bit     769         771           773          775
 32000   15 bit     784         787           790          793
 65000   16 bit     785         788           791          794
 16.7M   24 bit     786         789           792          795
}
```


### qume {#qume}

```sh
qemu-system-x86_64 -kernel vmlinuz -initrd new.cpio
qemu-system-x86_64 -kernel kernel/vmlinuz -initrd initrd/rootfs.cpio.xz -enable-kvm -append 'loglevel=3 text superuser showapps noutc noswap lst=onboot.lst mydata=mydata vga=0x317 waitusb=5:UUID="B4FE-5315" tce=UUID="B4FE-5315"'  $@
qemu-system-x86_64 -kernel kernel/vmlinuz -initrd initrd/initrd.gz -enable-kvm -m 1024 \
                   -append 'loglevel=3 text superuser showapps noutc noswap lst=onboot.lst mydata=mydata vga=0x317 waitusb=5:UUID="B4FE-5315" tce=UUID="B4FE-5315" console=tty0'  $@
```


## Command {#command}


### skill {#skill}

```sh
skill_(){
    find -type f -exec grep --color -nH fstab {} \;  ##find fstab in exec file.
    tune2fs -U  #change the uuid

    find / -type f -exec grep -sH 'text-to-find-here' {} \; 2>/dev/null #-s (=no message ,pemission

    # ******* -exec == | xargs

    find . -type f \( -name "*.pas" -o -name "*.dfm" \) -print0 | \
        xargs --null grep --with-filename --line-number --no-messages --color --ignore-case "searchtext"
    #-print0 和--null 在另一侧 （管道）是关键的 \
        #-print0:去掉 换行符 \n
    #--null：保证归档数据的一致性。
    #	将文件名从 find 发送到嵌入在 xargs 的 grep \
        #	允许在文件名中传递带有空格的文件名，允许 grep 将路径和文件名视为一个字符串，而不是破坏它在每个空间。

    ##Big file && Directory
    find . -type f -size +800M  -print0 | xargs -0 du -hm | sort -nr
    du -hm --max-depth=2 | sort -nr | head -12

    find . -type f -perm 750 -maxdepth 1 -exec ldd {} \;| grep not
}
```


### apt {#apt}

```sh

Apt(){
    apt-cache pkgnames					#list pkg
    apt-cache search "web server"		#
    apt-cache show postfix				#basic info
    apt-cache depends postfix			#list depends
    apt-get update						#synchronize pkg index  "/etc/apt/sources.list
    apt-get upgrade						#upgrade all pkg  installed
    sudo apt-get install filezilla --only-upgrade	#upgrade pkg confirm

    apt-get remove skype				#del pkg
    apt-get purge skype					#del config
    apt-get remove --purge skype		#

    apt-get download icinga				#download in current dir
    apt-get clean						#清空 apt-get 所下载的包占用的磁盘空间
    apt-get autoclean					#autoclean 清理不再使用且没用的下载
    apt-get autoremove icinga			删除为了满足依赖而安装且现在没用的包
    apt-get changelog apache2			显示包的更新日志
    apt-get check						显示损坏的依赖关系

}
```


### ag {#ag}

```sh

ag(){

ag 类似 grep 和 find，但是执行效率比后两者高。

ag -g <File Name> 类似于 find . -name <File Name>
ag -i PATTERN： 忽略大小写搜索含 PATTERN 文本
ag -A PATTERN：	搜索含 PATTERN 文本，并显示匹配内容之后的 n 行文本，例如：ag -A 5  abc 会显示搜索到的包含 abc 的行以及它之后 5 行的文本信息。
ag -B PATTERN：	搜索含 PATTERN 文本，并显示匹配内容之前的 n 行文本
ag -C PATTERN：	搜索含 PATTERN 文本，并同时显示匹配内容以及它前后各 n 行文本的内容。
ag -w PATTERN： 全匹配搜索，只搜索与所搜内容完全匹配的文本。
ag --ignore-dir <Dir Name>：忽略某些文件目录进行搜索。
ag --java PATTERN： 		在 java 文件中搜索含 PATTERN 的文本。
ag --xml PATTERN：			在 XML 文件中搜索含 PATTERN 的文本。
}
```


### lsof {#lsof}

```sh

lsof (){
lsof +D /mnt   #find some progress using file in /mnt
lsof -c abc		#find the progress whose name begin with "abc"
lsof abc.txt	#find the progress using the abc.txt file
lsof -p 1234	#find the file used 1234 progress
lsof -u uname	#find the progress owned uanme
}
getopts (){
  while getopts hmfts  opt
  do
    case $opt in
    h)
      show_help
      exit 0
      ;;
    m)
      ubus call system watchdog
      exit 0
      ;;
    f)
      fqy="$2"
      ubus call system watchdog '{ "frequency": '$fqy' }' >/dev/null
      shift
      ;;
    t)
      tout="$2"
      ubus call system watchdog '{ "timeout": '$tout' }' >/dev/null
      shift
      ;;
    s)
      stopwd="true"
      ubus call system watchdog '{ "stop": '$stopwd' }' >/dev/null
      ;;
    esac
    shift
  done
}
```


### crontab {#crontab}

```sh

crontab () {

    ~* *　　*　　*　　*　　command~

    分 　时　 日　 月　 周 　命令
    01   *   *   *   *     root run-parts /etc/cron.hourly
    # 说明:run-parts 这个参数了，如果去掉这个参数的话，后面就可以写要运行的某个脚本名，而不是目录名了

    #a-b 时表示从第 a 分钟到第 b 分钟这段时间内要执行
    #*/n 时表示每 n 分钟个时间间隔执行一次


    # crontab  启动 依赖 crontabs 包和 crond 服务，crond 服务使用的 crontab 定义的命令
    # 因此需要:  service crond start    （有的是 service cron start）
    # 或者       /etc/rc.d/init.d/crond start
    # 加入开机自动启动:chkconfig --level 35 crond on
}
```


### cpio {#cpio}

```sh

encode_cpio (){
find ./etc -print |cpio -ov >etc.cpio
cpio -idv
cpio -tv

find . -name inittab -depth | cpio -ovcB -A -O initrd.cpio
cpio --absolute-filenames -icvu < test.cpio

file initre.img  #查看文件格式
cpio -ivmd < initrd.img
find . | cpio -cv -o > ../initrd.new.img
zcat initrd.img | cpio -id
find . | cpio -o -H newc > ../new.cpio  #-H:指定格式   newc:ramdisk 制作 ramdisk 就用这个格式

##  square
 genext2fs -b 8192 -d /home/ ramdisk
 simg2img <sparse_image_files> <raw_image_file>
 img2simg <raw_image_file> <sparse_image_file> [<block_size>]

##  xz
xz -z filenaem  #compress
tar -Jcf linux-3.12.tar.xz linux-3.12/

xz -d filenaem	-k #-k 保留被压缩的文件
tar -Jxf linux-3.12.tar.xz

##  gzip
gzip –c filename > filename.gz
gunzip –d filename.gz

unzip -n test.zip -d /tmp #	不覆盖原先的文件
unzip -o test.zip -d tmp/ #覆盖原先的文件
unzip -v test.zip		  # 查看不解压
unzip test.zip			  # 解压在当前目录下
}
```


### dpkg-deb {#dpkg-deb}

```sh

_dpkg-deb(){

mkdir extract
mkdir extract/DEBIAN
mkdir build

# 0 解压出包中的文件到 extract 目录下
dpkg -X ../openssh-client_6.1p1_i386.deb extract/
# 1 解压出包的控制信息 extract/DEBIAN/下：
dpkg -e ../openssh-client_6.1p1_i386.deb extract/DEBIAN/
#change code
# 2 修改后的内容重新进行打包生成 deb 包
dpkg-deb -b extract/ build/
}
```


### tar {#tar}

```sh

_tar (){
tar -cvf test.tgz  test/ --exclude  *.jpg
tar -zxvf test.tgz  test/test.txt

zip -r mydata.zip mydata
unzip mydata.zip -d mydatabak

rar a all *.jpg #-> all.rar
unrar e all.rar
}
```


### dd {#dd}

```sh

_dd (){
dd if=diska.img of=boot.img skip=1 seek=1 bs=512 count=2879
dd if=/dev/zero  of=/dev/sda  bs=512 count=1

## skip  if
## seek  of
  skip=xxx 是在备份时对 if 后面的部分也就是原文件跳过多少块再开始读出；
  seek=xxx 是在备份时对 of 后面的部分也就是目标文件跳过多少块再开始写入。

if=输入文件(input file),  如： if=/dev/sda,缺省为标准输入
of=输出文件(output file), 如： of=mbr， 缺省为标准输出
ibs=Bytes,一次读入 Bytes 个字节，即一个块大小为 Bytes 个字节
obs=Bytes, 一次写 Bytes 个字节，即一个块大小为 Bytes 个字节
bs=Bytes ，同时设置读写块的大小为 Bytes 字节，可代替 ibs,obs
cbs=Bytes,一次转换 Bytes 个字节，即转换缓冲区大小
skip=blocks, 从输入文件开头跳过 blocks 个块后再开始复制
seek=blocks,从输出文件开头路过 blocks 个块后再开始复制（通常只有当输出文件是磁盘或磁带时才有效）
count=blocks, 仅复制 blocks 个块，块大小是 ibs 指定的字节数
}

dd if=/dev/hdx of=/dev/hdy        #将本地的/dev/hdx 整盘备份到/dev/hdy
dd if=/dev/hdx of=/path/to/image  #将/dev/hdx 全盘数据备份到指定路径的 image 文件
dd if=/dev/hdx | gzip >/path/to/image.gz  #备份/dev/hdx 全盘数据，并利用 gzip 工具进行压缩，保存到指定路径
gzip -dc /path/to/image.gz | dd of=/dev/hdx #将压缩的备份文件恢复到指定盘

dd if=/dev/mem of=/root/mem.bin bs=1024   #将内存里的数据拷贝到 root 目录下的 mem.bin 文件

dd if=/dev/urandom of=/dev/hda1 销毁磁盘数据

# 通过上两个命令输出的执行时间，可以计算出测试硬盘的读／写速度
dd if=/root/1Gb.file bs=64k | dd of=/dev/null
dd if=/dev/zero of=/root/1Gb.file bs=1024 count=1000000

# 当硬盘较长时间（比如 1，2 年）放置不使用后，磁盘上会产生 magnetic flux point。
# 当磁头读到这些区域时会遇到困难，并可能导致 I/O 错误。当这种情况影响到硬盘的第一个扇区时，可能导致硬盘报废
dd if=/dev/sda of=/dev/sda

```


### dd-Swap {#dd-swap}

```sh

dd if=/dev/zero of=/swapfile bs=1024 count=262144 #创建一个足够大的文件（此处为 256M）
mkswap /swapfile #把这个文件变成 swap 文件
swapon /swapfile #启用这个 swap 文件
/swapfile swap swap defaults 0 0 #在每次开机的时候自动加载 swap 文件, 需要在 /etc/fstab 文件中增加一行
```


### blockdev {#blockdev}

```sh

_blockdev (){
    # ensure that the Data disk is not less than 120 GiB
    if [ `blockdev --getsize64 $BLKDEV_DATA` -lt $((120 << 30)) ]; then
        # never return
        error_abort "Data Disk $BLKDEV_DATA is less than 120 GiB."
    fi

  TMP=`grep "$DSTDISK$" /proc/partitions | awk '{print $3}'`
  DISK_SIZE=`expr $TMP / 1000 \* 1024 / 1000`
}
```


### jobs {#jobs}

```sh

_jobs (){
    $ ./tcpserv01
        ^Z              #pause the process,
        [1]+  Stopped                 ./tcpserv01
    $ bg %1         #keep  it background
        [1]+ ./tcpserv01 &
    $ jobs -l
       [1]+  4524 Running                 ./tcpserv01 &
    $ fg %1            # #keep  it  foreground
        ./tcpserv01
    $ kill %1           #kill it in background
}
```


### nohup {#nohup}

> 使用 &amp; 命令后，作业被提交到后台运行，当前控制台没有被占用，但是一但把当前控制台关掉 (退出帐户时)，作业就会停止运行。
> nohup 命令可以在你退出帐户之后继续运行相应的进程。nohup 就是不挂起的意思 ( no hang up)。该命令的一般形式为：
> nohup command &amp;
> 如果使用 nohup 命令提交作业，那么在缺省情况下该作业的所有输出都被重定向到一个名为 nohup.out 的文件中，除非另外指定了输出文件：
> nohup command &gt; myout.file 2&gt;&amp;1 &amp;


### trap {#trap}

```sh

trap (){
  trap commands signal-list
  trap "ENV=/etc/profile getty  -l /bin/sh -n  115200 console;"  INT QUIT ABRT
  #HUP(1) :挂起
  #INT(2) :Ctrl + c
  #QUIT(3) :Ctrl + /
  #ABRT(6) :中止，因某些严重错误引发
  #ALRM(14) ：告警，处理超时
  #TERM(15) ：终止，关机时发送
  #ILL() : 严重错误
}
```


### bomb {#bomb}

```sh

bomb (){

    bomb | bomb &
}
```


### dos2unix {#dos2unix}

```sh

_dos2unix (){

vim
  :set ff?　查看文件格式
  :%s/^M//g	#注意同时按 Ctrl -v -m 输入 ^M
  :%s//r//g	#
  :set ff=unix

  sed 's/^M//' filename > tmp_filename
  tr -d "\015" dos_file.txt
  cat dos_file.txt | perl -pe '~s/\r//g' > dos_file.txt
}
```


### cp {#cp}

```sh

# - cp
cp /home/usr/dir/{file1,file2,file3,file4} /home/usr/destination/

# - conman pre./
cp /home/usr/dir/file{1..4} ./
```


### mv {#mv}

```sh

移动多个文件

- 参数 t
$ mv a b c -t d
$ mv -t d a b c
```


### rpm {#rpm}

```sh

_rpm(){
rpm -ivh --nodeps --force XXX
}
```


### stty {#stty}

```sh

_stty (){
  stty -F /dev/ttyS5 ispeed 115200 ospeed 115200 raw -echo
  stty -F /dev/ttyS2 peed 115200 parodd
# parodd 奇校验
# parenb 偶校验
# cs8，8 位数据位
# cstopb，2 位停止位
# crtscts，硬件流控
# raw
# 　　RAW 模式简单的来说，是发送端发动的二进制码原封不动的被接收端接收
    # 非 RAW 模式下，系统会对串口收到的数据中某些具有特殊意义的字符或组合进行转义.
    # 在 Linux 下系统的 tty 模式为非 RAW 模式，如果要调试单片机这种嵌入式设备，则需要将串口 设置为 RAW 模式。

stty -F /dev/ttyS0 speed 115200  cs8 -parenb -cstopb
# 15200 波特率 8 数据位 1 停止位 无校验位

# 其中"-"表示未设置状态，因此该串口设备默认的参数是： **9600bps 波特率、8位数据位、无校验、1位停止位、无硬件流控**
  exec > /dev/ttyS5
  exec < /dev/ttyS5

  while true;
  do read line
  done

  stty -F /dev/ttySx  raw -echo
}
```


### case {#case}

```sh

_case (){
case "${UTC}" in
  yes|true|1)
    ;;
  no|false|0)
    ;;
  *)
    ;;
esac

  while true
  do
    read -r -p "***, are you sure? [y/n] " input

    case $input in
      [yY][eE][sS]|[yY])
        ;;
      [nN][oO]|[nN])
        ;;
      *)
        ;;
    esac
}
```


### shift {#shift}

```sh

_shift (){
echo "参数个数为：$#,其中："
for i in $(seq 1 $#)
do
  eval j=\$$i
  echo "第$i 个参数($"$i")：$j"
done

shift 3

echo "执行 shift 3 操作后："
echo "参数个数为：$#,其中："
for i in $(seq 1 $#)
do
  #通过 eval 把 i 变量的值($i)作为变量 j 的名字
  eval j=\$$i
  echo "第$i 个参数($"$i")：$j"
done
}
_eval (){
    if [ -f $config_file ]; then

        # convert to unix new-line style
        cp -v $config_file  /tmp/
        config_file=/tmp/$(basename $config_file)
        dos2unix $config_file

        while read line;
        do
            # ignore the comment line
            echo $line | grep '^ *#' > /dev/null && continue;

            # ignore the empty line
            [ -z $line ] && continue;

            eval "export $line";
        done < $config_file;

        rm $config_file
    fi
}
```


### set {#set}

```sh

_set (){
set -o nounset  # -u
set -o errexit  # -e
}
```


### sed {#sed}

```sh

#+begin_src sh
  _sed (){
      sed '/^$/d' file
      sed -i 's/A/B/g' input
      sed '/^$/d;s/1111/AAA&/;s/1111/&BBB/' input
      #0000AAA1111BBB2222

      sed -i /^[[:space:]]*$/d filename #删除空行
      #因为由于特殊字符的存在，空行并不是真的空行（^$）
      #[[:space:]]表示空格或者 tab 的集合，（以及^M 这个不可见的换行符号）另外，到[[:space:]]后面跟着一个*，表示匹配 0 个或多个。
      #[[:space:]]可以用/s 表示
  }
```


### PS1 {#ps1}

```sh

_PS1 (){

  # \[\e[32;40m\] {\u} \[\e[0m\]
  # \e[32;40m\] {\u} \e[0m\]

  export PS1="\[\e[37;40m\][\[\e[32;40m\]\u\[\e[37;40m\]@\[\e[33;40m\h\e[0m \e[36;40m\]\w\[\e[0m\]]\\$ "
}
```


### mount {#mount}

```sh

_mount (){
mount -t vfat -o iocharset=cp936 /dev/sdd1 /mnt/usb   #若汉字文件名显示为乱码或不显示
  # -o options 主要用来描述设备或档案的挂接方式。常用的参数有：
  # loop：用来把一个文件当成硬盘分区挂接上系统
  # ro：采用只读方式挂接设备
  # rw：采用读写方式挂接设备
  # iocharset：指定访问文件系统所用字符集

mount -o remount,rw /
mount -o remount,rw /dev/sda1
}
```


### top {#top}

```sh
_top(){
sh -c top -b -n 2|grep Cpu |cut -d "," -f 1|cut -d ":" -f 2
}
```


### vim {#vim}

\#+begin_src sh

\_vi_vim(){
yy---复制当前；
p---粘贴当前
dd---删除当前行
nyy---复制多行(比如 3yy，复制 3 行)
ndd---删除多行
np---复制多遍
}


### ethtool {#ethtool}

\#+begin_src sh

\_ethtool(){
ethtool ethX
ethtool –i ethX    //查询 ethX 网口的相关信息
ethtool –s ethX [speed 10|100|1000]\\         //设置网口速率 10/100/1000M
[duplex half|full]\\           //设置网口半/全双工
[autoneg on|off]\\            //设置网口是否自协商
[port tp|aui|bnc|mii]\\         //设置网口类型

EG:ethtool -s ethX autoneg off speed 100 duplex full

1)/etc/rc.local
2)/etc/sysconfig/network-scripts/ifcfg-eth0;add:
	ETHTOOL_OPTS="speed 100 duplex full autoneg off"
}


### tmux {#tmux}

```sh

_tmux(){
Ctrl-B d， detach
Ctrl+b %：划分左右两个窗格。
Ctrl+b '"'：划分上下两个窗格。
Ctrl+b <arrow key>：光标切换到其他窗格。<arrow key>是指向要切换到的窗格的方向键，比如切换到下方窗格，就按方向键↓。
Ctrl+b ;：光标切换到上一个窗格。
Ctrl+b o：光标切换到下一个窗格。
Ctrl+b {：当前窗格左移。
Ctrl+b }：当前窗格右移。
Ctrl+b Ctrl+o：当前窗格上移。
Ctrl+b Alt+o：当前窗格下移。
Ctrl+b x：关闭当前窗格。
Ctrl+b !：将当前窗格拆分为一个独立窗口。
Ctrl+b z：当前窗格全屏显示，再使用一次会变回原来大小。
Ctrl+b Ctrl+<arrow key>：按箭头方向调整窗格大小。
Ctrl+b q：显示窗格编号。
}
```


## Shell {#shell}


### basic {#basic}


#### whiptail {#whiptail}

```sh
local retval=
    eval  "/usr/bin/whiptail --clear --backtitle '  --== ZKTY(TM) System Install (version: `cat /etc/system-version`) ==--' $@"
    retval=$?
    return $retval

## 1 Message Box
  whiptail --title "Test Message Box" --msgbox "Create a message box with whiptail. Choose Ok to continue." 10 60

## 2 Yes / No button
  if (whiptail --title "Test Yes/No Box" --yesno "Choose between Yes and No." 10 60) then
  #if (whiptail --title "xx" --yes-button "xx" --no-button "xx"  --yesno "xx" 10 60) then
    echo "You chose Yes. Exit status was $?."
  else
    echo "You chose No. Exit status was $?."
  fi

## 3 radiolist: only one
    #whiptail --title "<menu title>" --radiolist "<text to show>" <height> <width> <menu height> [ <tag> <item> ] . . .
OPTION=$(whiptail --title "Test Menu Dialog" --radiolist "Choose your option" 15 60 4 \
"1" "Grilled Spicy Sausage" \
"2" "Grilled Halloumi Cheese" \
"3" "Charcoaled Chicken Wings" \
"4" "Fried Aubergine"  3>&1 1>&2 2>&3)#(3>&1 1>&2 2>&3)是为了把选择的内容填进变量OPTION

exitstatus=$?
if [ $exitstatus = 0 ]; then
    echo "Your chosen option:" $OPTION   ##default return "1" "2" ...
else
    echo "You chose Cancel."
fi

## 4 checklist: not only
    #whiptail --title "<menu title>" --checklist "<text to show>" <height> <width> <menu height> [ <tag> <item> ] . . .
DISTROS=$(whiptail --title "Test Checklist Dialog" --checklist \
"Choose preferred Linux distros" 15 60 4 \
"debian" "Venerable Debian" ON \
"ubuntu" "Popular Ubuntu" OFF \
"centos" "Stable CentOS" ON \
"mint" "Rising Star Mint" OFF 3>&1 1>&2 2>&3)

exitstatus=$?
if [ $exitstatus = 0 ]; then
    echo "Your favorite distros are:" $DISTROS   ## defualts return "debian" "centos"
else
    echo "You chose Cancel."
fi

## 4 gauge
  {
    for ((i = 0 ; i <= 100 ; i+=20)); do
        sleep 1
        echo $i
    done
  } | whiptail --gauge "Please wait while installing" 6 60 0
  #	whiptail --gauge "<test to show>" <height> <width> <inital percent>

select_ (){
    clear
    echo -e "\t\tmain Menu\n"

    PS3='Please enter your choice[1-4]: '
    options=("Backup System" "One Key Restore" "Command" "Reboot")
    select opt in "${options[@]}"
    do
    case $opt in
      "Backup System")
      ##
      ;;
      "One Key Restore")
      ##
      ;;
      "Command")
      exit
      ;;
      "Reboot")
      reboot
      ;;
      *)
      echo Please enter your choice in [1-4]
      ;;
    esac
    done
}

```


#### get-path {#get-path}

```sh
DIR_PWD=$(dirname $(readlink -f "$0"))
DIR_PWD=$(cd `dirname $0` && pwd)
DIR_PWD=$(cd `dirname $0` ; pwd)
```


#### note/comment {#note-comment}

```sh
: << !
!

: << 'COMMENT'

COMMENT

: '

'
```


#### linux-version {#linux-version}

```sh
lsb_release -a
cat /etc/issue

cat /etc/redhat-release
cat /etc/debian_version

cat /proc/version
```


#### delay-loop {#delay-loop}

```sh
# eg.:20 200000 "waiting "
  local loop=$1
  local interval=$2 # in usec
  local info=$3

  local i=

  echo -n $info

  i=0
  while [ $i -lt $loop ];
  do
      usleep $interval;
      i=$(( $i + 1 ));
      echo -n "."
  #echo -ne "\r                               \r" # Clear this line.
  done
  echo
```


#### check-machine {#check-machine}

```shell
local cpu_type=

cpu_type=$(cat /proc/cpuinfo | grep '^model name' | head -1 )
cpu_type=$(echo $cpu_type | sed -r 's/^model name[ \t]*:[ \t]*//g')
cpu_type=$(echo $cpu_type | sed -r 's/[ \t]*@.*$//g')

echo -e $"\t======================================================"
echo -e $"\t\t\033[32m    CPU type: $cpu_type	\033[0m";d
echo -e $"\t======================================================"

if [ "$cpu_type" != "Intel(R) Celeron(R) 2980U" ]; then
    return 1;
fi

# OK, machine type is TPE4000, continue to install the OS
return 0;
```


#### source.lst {#source-dot-lst}

```sh

lsb_release -a		#查看版本
Distributor ID: Debian
Description:    Debian GNU/Linux 8.1 (jessie)
Release:        8.1
Codename:       jessie


#iso 镜像 source.list
deb file:///mnt/cdrom lucid main
deb file://   #debian系列ISO源的固定格式
lucid             #发行版代号或昵称

此外，源来源有5个，分别是:
main               #Canonical支持的开源软件
universe         #社区维护的开源软件
restricted       #设备的专有驱动
multiverse     #有版权与合法性问题限制的软件
source            #源代码
```


### sys-install {#sys-install}

```shell
sys_install (){
  local DISK=$1
  local NAME=/mnt/xj_intall/$2

  UNIT=`fdisk -l 2> /dev/null | grep "Disk /dev/${DISK}" | cut -f 4 -d " " | cut -f 1 -d ','`
  CAPACITY=`fdisk -l 2> /dev/null | grep "Disk /dev/${DISK}" | cut -f 3 -d " "`
  if [ "`echo ${CAPACITY} | grep "\."`" != "" ]; then
    CAPACITY=`echo ${CAPACITY} | cut -f 1 -d .`
  fi
  echo -e "\n\t>>>>>################### DISK information ###########################"
  echo -e "\tDISK /dev/${DISK}: ${CAPACITY}${UNIT}"

  echo -e "\n\t>>>>>################### Create Partition talbe #####################"
  parted -s /dev/${DISK} mktable msdos
  parted -s /dev/${DISK} print | grep "Partition Table"

  echo -e "\n\t>>>>>############### Create Partitions /dev/${DISK}##################"
  #parted -s /dev/${DISK} mkpart primary ext3 0% 20G
  #parted -s /dev/${DISK} mkpart primary ext3 20G 100%
    ###64G:20G + else
  echo -ne "n\np\n1\n\n+20G\nn\ne\n4\n\n\nn\nl\n\n\nw\n" | fdisk /dev/$DISK  1> /dev/null
    ### >= 120G:20G + 60G + else
  #echo -ne "n\np\n1\n\n+20G\nn\ne\n4\n\n\nn\nl\n\n+60G\nn\nl\n\n\nw\n" | fdisk /dev/$DISK  1> /dev/null

  echo -e "\n\t>>>>>################## Set /dev/${DISK}1 boot on ###################"
  parted -s /dev/${DISK}  set 1 boot on
  sync

  echo -e "\n\t>>>>>################## Format Partitions ###########################"
  mkfs.ext3 /dev/${DISK}1  &> /dev/null
  echo -e "\tFormat /dev/${DISK}1 /dev/${DISK}5 to ext3"
  sleep 1
  sync
  mkfs.ext3 /dev/${DISK}5  &> /dev/null
  sync

  echo -e "\n\t>>>>>#################### Partition information #####################"
  parted -s /dev/${DISK} print

  echo -e $"\n\033[31m############## Repartition /dev/${DISK} finished! #############\033[0m"

  ### mount /dev/${DISK}
  mkdir -p /${DISK}1
  sync
  mount /dev/${DISK}1  /${DISK}1
  cd /${DISK}1
  rm -rf *
  sync

  echo -e "\n\t>>>>>############# Install grub to /dev/${DISK}1 ################"
  grub-install --no-floppy --root-directory=/${DISK}1 /dev/${DISK}  1> /dev/null	###--root-directory=/xxx/(boot/grub/)
  #update-grub
  sync

  echo -e "\n\t>>>>>############# Unzip files to /dev/${DISK}1  ################"
  tar -zxvf ${NAME} 1> /dev/null || exit 0
  sync
  #cp /mnt/xj_file/fstab/fstab /${DISK}1/etc/fstab

  cd /
  umount /dev/${DISK}1
  rmdir /${DISK}1
  sync

  echo -e $"\n\033[36m#############System install finished! ################\033[0m"

}
```


### insmod-drive {#insmod-drive}

```shell
insmod_drive (){

if [ -d /lib/modules/$(uname -r)/kernel/extra/ ]; then
    for module_p in /lib/modules/$(uname -r)/kernel/extra/*;
  do
        module=${module_p##*/} 				# delete the path
        module=${module%.ko}				# delete the ".ko"
        module=`lsmod|grep $module`
        if [ "$module" == "" ]; then
            /sbin/insmod -f $module_p file=/dev/mmcblk0p1 stall=0 removable=1
        fi
    done
fi
}
```


### disk-search {#disk-search}


#### search-desk-disk0 {#search-desk-disk0}

```shell
search_dest_disk0 ()
{
    DISK=
    DISK_SIZE=$(( 1000 * 1000 * 1000 * 16384 )) # 16T bytes

    for i in `ls -d /sys/class/block/sd*`;
    do
        # ignore disk partitions
        test -f $i/partition && continue;

        # ignore removable disks
        [ `cat $i/removable` -ne 0 ] && continue;

        size=$(( `cat $i/queue/hw_sector_size` * `cat $i/size`))
        if [ $DISK_SIZE -gt $size ]; then
            DISK_SIZE=$size;
            DISK=$i;
        fi
        # echo $(basename $i) `cat $i/queue/logical_block_size`  `cat $i/size`
    done

    DISK=/dev/$(basename $DISK)
    echo "$DISK --- $DISK_SIZE bytes"
}

###################
```


#### search_dest_disk {#search-dest-disk}

```shell
search_dest_disk ()
{
    # $DEST_DISK
    cd /sys/class/block
  local nr=0
  local dest_disk_0=
  local dest_disk_1=

  echo -e "\n\033[32m>>>>>>>>#****************** Identifing Disk ******************\033[0m"
  echo -e "List of disks:"
    for disk in $(ls);
    do
        if [ ! -L $disk ]; then
            # not a symlink
            continue;
        fi

        if [ -e ${disk}/partition ]; then
            # $disk is a partition, ignore it
            continue;
        fi

        if [ -e ${disk}/removable ];  then
            if [ "$(cat ${disk}/removable)" -eq 1 ]; then
                # $disk is a removable one, USB disk or CDROM driver,
                continue;
            fi
        fi

    if [ ! -e ${disk}/device ]; then
            # $disk is a loop partition, ignore it
            continue;
        fi

    echo -ne "\t$disk"

    if [ -z "$dest_disk_0" ];then
      dest_disk_0=$(basename $disk)
    fi

    if [ ${nr} -ne 0 ];then
      dest_disk_1=$(basename $disk)
    fi
    nr=$(( $nr + 1 ))
            #break;
    done

  if [ "${dest_disk_1}" != "" ];then

    if [ $(blockdev --getsize64 /dev/${dest_disk_0}) -le $(blockdev --getsize64 /dev/${dest_disk_1}) ];then
      SYS_DISK=${dest_disk_0}
      DAT_DISK=${dest_disk_1}
    else
      SYS_DISK=${dest_disk_1}
      DAT_DISK=${dest_disk_0}
    fi
  else
    #return dest_disk_0
    SYS_DISK=${dest_disk_0}
  fi

  local size_sys=$(get_size ${SYS_DISK})
  local size_dat=$(get_size ${DAT_DISK})
  local unit_sys=$(get_unit ${SYS_DISK})
  local unit_dat=$(get_unit ${DAT_DISK})

  echo ""
  echo -e "\n\033[32mConform Disk:\033[0m"
  if [ "$DAT_DISK" != "" ];then
    echo -e "\t SYS_DISK: ${SYS_DISK} ==>> ${size_sys} ${unit_sys}"
    echo -e "\t DAT_DISK: ${DAT_DISK} ==>> ${size_dat} ${unit_dat}\n"
  else
    echo -e "\t SYS_DISK: ${SYS_DISK} ==>> ${size_sys} ${unit_sys}\n"
  fi

  sleep 1
    cd - > /dev/null
}
```


#### get-unit {#get-unit}

```sh
get_unit(){
local disk=$1
fdisk -l 2> /dev/null | grep "Disk /dev/${disk}" | cut -f 4 -d " " | cut -f 1 -d ','
}
```


#### get-size {#get-size}

```shell
get_size (){
  local disk=$1
  fdisk -l 2> /dev/null | grep "Disk /dev/${disk}" | cut -f 3 -d " " | cut -f 1 -d .
}
```


#### search-desk-disk2 {#search-desk-disk2}

```shell

search_dest_disk2 () {
    local dest_disk=

    local disk0_dev=
    local disk1_dev=
    local disk0_size=0
    local disk1_size=0

    local nr_disks=0

    for i in /sys/class/block/*;
    do
        # ignore the loop/nbd device
        if (readlink -f $i | grep virtual/block > /dev/null); then
            continue;
        fi

        # ignore disk partitions
        if [ -f $i/partition ]; then
            continue;
        fi

        # ignore removable devices
        if [ -f $i/removable -a $(cat $i/removable) -ne 0 ]; then
            continue;
        fi

        case $nr_disks in
            0)
                disk0_dev=/dev/$(basename $i);
                disk0_size=$(blockdev --getsize64 $disk0_dev);
                ;;
            1)
                disk1_dev=/dev/$(basename $i);
                disk1_size=$(blockdev --getsize64 $disk1_dev);
                ;;
            *)
                # do nothing
                ;;
        esac
        nr_disks=$(($nr_disks + 1));
    done

    case $nr_disks in
        1)
            # only one hard disk found
            BLKDEV_OS=$disk0_dev
            BLKDEV_DATA=$disk0_dev
            export DEST_DISK=$disk0_dev
            return;
            ;;
        2)
            # 2 hard disk found, more steps need
            ;;
        *)
            echo "Wrong disks"
            export DEST_DISK=
            return;
            ;;
    esac
}
```


#### search_dest_disk_3 {#search-dest-disk-3}

```shell

search_dest_disk_3 () {
#   local disk_size=$((100<<40)) # 100TiB, no disk is so large
    local disk_dev=

    # find SATA controller
    for i in /sys/class/block/*;
    do
        # ignore loop/nbd device
        if (readlink -f $i | grep virtual/block > /dev/null); then
            continue;
        fi

        # ignore disk partitions
        if [ -f $i/partition ]; then
            continue;
        fi

        # ignore removable devices
        if [ -f $i/removable -a $(cat $i/removable) -ne 0 ]; then
            continue;
        fi

        tmp=$(blockdev --getsize64 /dev/$(basename $i))
        if [ $disk_size -gt $tmp ]; then
            disk_size=$tmp;
            disk_dev=/dev/$(basename $i);
        fi
    done

    export DEST_DISK=$disk_dev
    return;
}
```


#### search_usb_disks {#search-usb-disks}

```shell

search_usb_disks  (){
    # find all removeable disks/partitions that contains FS
    # the resault save in var USB_BLKDEV_FS

    local usb_disks=
    local usb_disk_parts=

    ### find the all of the USB disks
    for blkdev in $(ls /sys/class/block/);
    do
        [ ! -f /sys/class/block/$blkdev/removable ] && continue;

        if [ `cat /sys/class/block/$blkdev/removable` -ne 0 ]; then
            usb_disks="$blkdev $usb_disks"
        fi
    done

    ### find all of the USB disk partitions
    for i in $usb_disks;
    do
        for x in `(cd /sys/class/block; ls -d ${i}?*)`;
        do
            if [ -f /sys/class/block/$x/partition ]; then
                usb_disk_parts="$x $usb_disk_parts"
            fi
        done
    done

    ### find the blkdev on USB disk which has FS
    for i in $usb_disk_parts $usb_disks;
    do
        [ ! -b /dev/$i ] && continue; # not a block dev
        if (blkid | grep "^/dev/$i:" > /dev/null); then
            # OK, this blkdev has FS
            USB_BLKDEV_FS="/dev/$i $USB_BLKDEV_FS"
        fi
    done
}
```


### disk-part {#disk-part}


#### create_part_fdisk {#create-part-fdisk}

```shell

create_part_fdisk (){
    loop_idx=1;
    (while [ $loop_idx -le $(($data_part_nr + 1)) ];
     do
         echo -ne "t\n"
         echo -ne "$loop_idx\n"
         echo -ne "${part_uuid}\n"
         loop_idx=$(( $loop_idx + 1 ));
     done; echo -ne "w\n") | fdisk $disk

    partprobe $disk; fdisk -l $disk
    parted -a opt $disk u b p
    partprobe -s $disk
    sync

  #parted -s /dev/${DISK} mkpart primary ext3 0% 20G
  #parted -s /dev/${DISK} mkpart primary ext3 20G 100%
}
```


#### create_part_eof {#create-part-eof}

```shell

create_part_eof (){
#1）
fdisk ${DEST_DISK} << EOF
n
e
4
227
7780
n
7701
7780
t
7
82
w
EOF

#2）
  parted $1 mkpart primary ext2 ${csize}GB ${msize}GB <<EOF
  ignore
EOF

#3）
parted /dev/${DISK} --script "mktable msdos"
START3=750
parted --align optimal /dev/${DISK} --script "mkpart primary ext3 ${START3}${UNIT} 100%"
}

```


#### clean-disk {#clean-disk}

```sh

_clean_disk (){
  local disk=$1

  echo -e "\033[31mClean the dest disk\033[0m"
  local disk_flag=$(fdisk -l /dev/${disk}|grep /dev/${disk} |wc -l)
  if [ $disk_flag -eq 1 ];then
    echo -e "\tDest disk no partition!"
  else
    echo -e "\tExist partition,and clean!"
    dd if=/dev/zero  of=/dev/${disk}  bs=512 count=1  &> /dev/null
    #echo "y" | mkfs.ext3 /dev/${disk} &> /dev/null;
  fi
}

```


#### create-partition {#create-partition}

```shell

_create_partitions  () {
  ###$0 DISK  part_nr
    local disk=$1

### Clean Disk
  _clean_disk $disk

  echo -e "\n\t>>>>>>>>#***********\033[31m Now Formate Data Partition \033[0m"
    local disk_size=`blockdev --getsize64 /dev/$disk`
  #local disk_size=4000000000000 #
  local disk_size_rootfs=$(( 1 << 20 )) ### 2GiB rootfs partition
  #local disk_size_rootfs=$(0xfffffe00000) ### 2GiB rootfs partition
  local data_part_nr=$2
    local data_part_size=
    local pos_begin=
    local pos_end=

    local loop_idx=

    ### destory the disk partition, danger!!
    dd if=/dev/zero of=/dev/$disk bs=64K count=1 &> /dev/null

    parted -s /dev/$disk mklabel gpt

  data_part_size=$(( ( $disk_size - $disk_size_rootfs ) / $data_part_nr ))
  data_part_size=$(( $data_part_size & 0xfffffe00000)); # align to 2MiB

  pos_begin=$(( 1<<20 ))
  pos_end=$(($data_part_size - 1 ))

  # the first partition
  echo ""
  echo -ne "\033[32m the 1 part: \033[0m"
  echo -e "parted -s /dev/$disk "mkpart primary ext3  ${pos_begin}B  ${pos_end}B"";
    parted -s  /dev/$disk "mkpart primary ext3  ${pos_begin}B  ${pos_end}B"  2> /dev/null;

    # loop to create disk partitions
    loop_idx=2;
    while [ $loop_idx -le $data_part_nr ];
    do
        pos_begin=$(( $pos_end + 1 ));
        pos_end=$(( $pos_begin + $data_part_size - 1 ));
    echo -ne "\033[32m the $loop_idx part part: \033[0m"
        echo -e "parted -s /dev/$disk "mkpart primary ext3  ${pos_begin}B  ${pos_end}B"";
        echo "Yes || Ignore" |
    eval parted -s /dev/$disk "mkpart primary ext3  ${pos_begin}B  ${pos_end}B" 2> /dev/null;
    sleep 1

        loop_idx=$(( $loop_idx + 1 ));
    done

  partprobe  /dev/$disk
    parted -s  /dev/$disk u b p &> /dev/null
    #partprobe -s  /dev/$disk
    sync

  #parted -s  /dev/$disk print
  echo ""
  echo -e "\t>>>>>>>>#*********** Partition Information"
  parted -s /dev/${disk} print | tail -$(( $NR + 5 )) > ./dat_disk.flag
  while read line;
    do
        echo -e "\t\033[33m$line\033[0m"
    done < ./dat_disk.flag
    rm ./dat_disk.flag
}
```


#### delete_partition {#delete-partition}

```shell
delete_partition (){
    echo -e "\n>>>>>> Delete Partitions.\n"
    local disk=$1
    local part=`fdisk -l 2> /dev/null | grep "^/dev/${disk}" | awk '{print (}' | wc -l`
    while [ ${part} -ge 1 ]
    do
        echo "Delete Partiton: /dev/${Disk}${part}"
        if [ ${part} -ne 1 ];then
            echo -ne "d\n${part}\nw\n" | fdisk /dev/${disk} &> /dev/null
        else
            echo -ne "d\nw\n" | fdisk /dev/${disk} &> /dev/null
        fi
        part=`expr ${part} - 1`
    done
    return 0
}

```


### uuid-gen {#uuid-gen}

```shell
uuid_gen ()
{
    # stupid, but works!
    # our simple linux system has no uuidgen tool

    # 064bb9ff-7a05-44af-a55e-a9e8f1011426

    local tmp_0=$(head -c 16 /dev/urandom | md5sum | head -c 8)
    local tmp_1=$(head -c 16 /dev/urandom | md5sum | head -c 4)
    local tmp_2=$(head -c 16 /dev/urandom | md5sum | head -c 4)
    local tmp_3=$(head -c 16 /dev/urandom | md5sum | head -c 4)
    local tmp_4=$(head -c 16 /dev/urandom | md5sum | head -c 12)

    echo ${tmp_0}-${tmp_1}-${tmp_2}-${tmp_3}-${tmp_4}

  UUID=`echo ${tmp_0}-${tmp_1}-${tmp_2}-${tmp_3}-${tmp_4}`
  #UUID=`uuidgen`

}
```


### uuid-set {#uuid-set}

```shell
uuid_se() {
  local uuid=`blkid   /dev/sd|awk -F'"' '{print $2}'`

    if grep -q "/dev/sd$i" /etc/fstab;then
        sed -i "s/\/dev\/sd$i/UUID=$uuid/" /etc/fstab
  elif ! grep -q "$uuid" /etc/fstab;then
        echo "UUID=$uuid	/mnt	ext4    defaults	0 0" >> /etc/fstab
    fi

  ##mkfs.ext3 -U $uuid /dev/${DISK}1
  ##tune2fs /dev/sda1 -U $uuid

  ##xfs_admin  /dev/${DISK}1 -U $uuid  ##default xfs_filesystem
}
```


### menu.lst {#menu-dot-lst}

```shell
menu_lst (){
  local KERNEL=$(basename $(ls boot/vmlinuz* | head -1))
  local INITRD=$(basename $(ls boot/initrd*  | head -1))

echo "# grub.conf generated by anaconda
#
# Note that you do not have to rerun grub after making changes to this file
# NOTICE:  You do not have a /boot partition.  This means that
#          all kernel and initrd paths are relative to /, eg.
#          root (hd0,0)
#          kernel /boot/vmlinuz-version ro root=/dev/hdb1
#          initrd /boot/initrd-version.img
#boot=/dev/hdb
default=0
timeout=5
splashimage=(hd0,0)/boot/grub/splash.xpm.gz
#hiddenmenu

title Red Hat Enterprise Linux Server (2.6.32-2-686)
  root (hd0,0)
  kernel /boot/${KERNEL} ro root=UUID=${UUID} ro 8250.nr_uarts=18 noirqdebug
  initrd /boot/${INITRD}

title Red Hat Enterprise Linux Server (2.6.18-92.el5)
  root (hd0,0)
  kernel /boot/${KERNEL} ro root=UUID=${UUID}
  initrd /boot/${INITRD}" > boot/grub/menu.lst
}
```


### grub2 {#grub2}

<https://www.cnblogs.com/yinheyi/p/7279508.html>

```shell

Grub2(){
# grub.cfg”这个是系统自动生成的文件,不建议直接修改，“/etc/grub.d”和“/etc/default/grub”
# “/etc/grub.d”是操作系统菜单目录，一般由系统生成，我们无需修改，可以改/etc/default/grub

root# grub-editenv list
saved_entry=CentOS Linux 7 (AltArch)
root# grub-set-default "CentOS Linux 7 (AltArch)"


/etc/default/grub
GRUB_DEFAULT=0
#GRUB_DEFAULT=“7>3” 第7项第3个子项启动
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
GRUB_CMDLINE_LINUX_DEFAULT="quiet"
GRUB_CMDLINE_LINUX=""

# Uncomment to enable BadRAM filtering, modify to suit your needs
# This works with Linux (no patch required) and with any kernel that obtains
# the memory map information from GRUB (GNU Mach, kernel of FreeBSD ...)
#GRUB_BADRAM="0x01234567,0xfefefefe,0x89abcdef,0xefefefef"

# Uncomment to disable graphical terminal (grub-pc only)
#GRUB_TERMINAL=console

# The resolution used on graphical terminal
# note that you can use only modes which your graphic card supports via VBE
# you can see them in real GRUB with the command `vbeinfo'
#GRUB_GFXMODE=640x480

# Uncomment if you don't want GRUB to pass "root=UUID=xxx" parameter to Linux
#GRUB_DISABLE_LINUX_UUID=true

# Uncomment to disable generation of recovery mode menu entries
#GRUB_DISABLE_RECOVERY="true"

# Uncomment to get a beep at grub start
#GRUB_INIT_TUNE="480 440 1"
}
```


### mount {#mount}


#### mount-fat32 {#mount-fat32}

```shell

mount_Fat32 () {

until [ -f /mnt/boot/initrd/filesys ] || [ -f /mnt/isolinux/filesys ]
do
  fdisk -l | grep "Win95\ FAT32" | awk '{print $1}' | cut -d / -f 3 | grep 4 > /partition
  INPUT_FILE="/partition"
  while [ -z `cat $INPUT_FILE` ]
  do
    echo -e $"*************      Please Wait 3 Second         ************"
    sleep 3
          fdisk -l | grep "Win95\ FAT32" | awk '{print $1}' | cut -d / -f 3 | grep 4 > /partition
  done
  cat $INPUT_FILE | while read PARTITION
          do
                  mkdir /$PARTITION
                  mount /dev/$PARTITION /$PARTITION
                  if [ -f /$PARTITION/boot/initrd/filesys ] || [ -f /$PARTITION/isolinux/filesys ];then
                    umount /dev/$PARTITION
                          rmdir /$PARTITION
                    mount /dev/$PARTITION /mnt
        echo -e $"***********    Auto mount /dev/$PARTITION to /mnt   **********"
      else
        umount /dev/$PARTITION
        rmdir /$PARTITION
      fi
    done
  rm -rf /partition
done

# ****************************************************************************************
# *********************               Execute Uset Script                    *************
# ****************************************************************************************
if [ -f /mnt/UserScript/autostart ];then
  echo -e $"***********   Auto Run User Script /mnt/UserScrip/autostart   ***********"
  chmod a+x /mnt/UserScript/*
  /mnt/UserScript/autostart
fi
}
```


#### mount-doart {#mount-doart}

```shell
mount_dpart ()
{
  lsblk  | grep part | awk -F - '{print $2}' | awk '{print $1 " " $7}' > ./part.tmp
  cat ./part.tmp |  while read line;
  do
    mpoint=$(echo $line | awk '{print $2}')
    if [ -z $mpoint ];then
      part=$line
      mkdir -p /dpart/$part
      mount /dev/$part /dpart/$part 2> /dev/null
    fi
  done
  rm ./part.tmp

}

mount_point (){

readlink /etc/sysconfig/tcedir > /etc/sysconfig/usbdir
if [ "`cat /etc/sysconfig/usbdir | grep '^/mnt/'`" != "" ];then
    sed -i 's/\/tce//g' /etc/sysconfig/usbdir
    USBDIR=`cat /etc/sysconfig/usbdir`
    PART=`mount | grep "${USBDIR}" | cut -f 1 -d " "`
    ln -sfv `cat /etc/sysconfig/usbdir` /root/usb &> /dev/null
    echo "Device ${PART} mount on ${USBDIR}."
fi
}

```


#### mount-iso-apt {#mount-iso-apt}

```shell
mount_iso_apt(){

### mount Udisk iso
mount /dev/sdx  /mnt
mkdir /media/cdrom
mount -o loop -t iso9660 /mnt/xx.iso  /media/cdrom  #(/cdrom  apt-get required

### apt-get  iso
apt-cdrom -m -d /media/cdrom/ add
apt-get update
#apt-get upgrade && apt-get dist-upgrade  #更新工具

cat /etc/apt/sources.lst

apt-get install  snmpd  ##(-f


 /etc/snmp/snmpd.conf  #安装成功后生成
}

```


### mountpoint {#mountpoint}

```shell
# - 检查文件夹是否挂载
# 1. grep
if grep -qs '/mnt/foo' /proc/mounts; then
    echo "It's mounted."
else
    echo "It's not mounted."
fi

# 2. mountpoint
if mountpoint -q /mnt/foo
then
   echo "mounted"
else
   echo "not mounted"
fi
```


### debian7 {#debian7}

```shell
debian7(){

###ali
deb http://mirrors.aliyun.com/debian/ wheezy main non-free contrib
deb http://mirrors.aliyun.com/debian/ wheezy-proposed-updates main non-free contrib
deb-src http://mirrors.aliyun.com/debian/ wheezy main non-free contrib
deb-src http://mirrors.aliyun.com/debian/ wheezy-proposed-updates main non-free contrib

###163
deb http://mirrors.163.com/debian wheezy main non-free contrib
deb http://mirrors.163.com/debian wheezy-proposed-updates main contrib non-free
deb http://mirrors.163.com/debian-security wheezy/updates main contrib non-free
deb-src http://mirrors.163.com/debian wheezy main non-free contrib
deb-src http://mirrors.163.com/debian wheezy-proposed-updates main contrib non-free
deb-src http://mirrors.163.com/debian-security wheezy/updates main contrib non-free
如果有问题，注释掉以下三行
#deb http://http.us.debian.org/debian wheezy main contrib non-free
#deb http://non-us.debian.org/debian-non-US wheezy/non-US main contrib non-free
#deb http://security.debian.org wheezy/updates main contrib non-free
}
```


### debian8.1 {#debian8-dot-1}

```shell
debian8_1(){
#snmp
deb http://mirrors.163.com/debian/ jessie main non-free contrib
deb http://mirrors.163.com/debian/ jessie-updates main non-free contrib
deb http://mirrors.163.com/debian/ jessie-backports main non-free contrib
deb-src http://mirrors.163.com/debian/ jessie main non-free contrib
deb-src http://mirrors.163.com/debian/ jessie-updates main non-free contrib
deb-src http://mirrors.163.com/debian/ jessie-backports main non-free contrib
deb http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib
deb-src http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib

apt-get update
apt-get install snmpd #snmpd exe progress


deb http://mirrors.cloud.aliyuncs.com/debian stable main contrib non-free
deb http://mirrors.cloud.aliyuncs.com/debian stable-proposed-updates main contrib non-free
deb http://mirrors.cloud.aliyuncs.com/debian stable-updates main contrib non-free
deb-src http://mirrors.cloud.aliyuncs.com/debian stable main contrib non-free
deb-src http://mirrors.cloud.aliyuncs.com/debian stable-proposed-updates main contrib non-free
deb-src http://mirrors.cloud.aliyuncs.com/debian stable-updates main contrib non-free

deb http://mirrors.aliyun.com/debian stable main contrib non-free
deb http://mirrors.aliyun.com/debian stable-proposed-updates main contrib non-free
deb http://mirrors.aliyun.com/debian stable-updates main contrib non-free
deb-src http://mirrors.aliyun.com/debian stable main contrib non-free
deb-src http://mirrors.aliyun.com/debian stable-proposed-updates main contrib non-free
deb-src http://mirrors.aliyun.com/debian stable-updates main contrib non-free
}
```


### zhcon-unicode {#zhcon-unicode}

```shell
zhcon_unicode()
{
    #默认终端控制台tty不支持中文显示，需要安装支持中文显示的软件，例如zhcon/fbterm
    #字符界面在不用帧缓冲的中文支持环境时。是根本不可能支持 cjk 显示的.

    #配置locales
    #aptitude install locales
    dpkg-reconfigure locales
    zh_CN GB2312 zh_CN.GBK GBK ;zh_CN.UTF-8 UTF-8  ; en_US.UF8（defaults）

    #安装字体
    #修改源 && apt-get update
    apt-get install xfonts-intl-chinese
    #apt-get install xfonts-wqy （非必要

    #安装输入法
    apt-get install scim
    apt-get install scim-pinyin
    reboot
    zhcon
    kbd_mode -a

    export LANG=zh_CN.GBK
}
```


### snmp {#snmp}

```shell
snmp (){

    dpkg --configure -a

    # Q: Package libkrb53 is not configured yet.
    #stackoverflow
    # A:run apt-get update / apt-get dist-upgrade, accept the failures, then reboot, then run both again. Now its OK.
}
```


### x11 {#x11}

```sh
x11(){
    apt-get install xorg
    apt-get install openbox

    #apt-get install x-window-system-core
    startx #可启动桌面

    apt-get install xfce4 #桌面管理系统

    xinit #启动图形，不含窗口管理器 twm（修改窗口的大小，最大化，最小化，移动）
    #startx 启动的时候会包含 twm

    rc.local 中启动 x service
    cat >> /etc/rc.local << EOL
    X&
    export DISPLAY=:0.0
    xterm
    EOL

    # X Client 部分值得考虑一下的就是 DISPLAY 环境变量。它主要用于远程 X Client 的使用。
    # 该变量表示输出目的地的位置，由三个要素组成：
    [host]:display[.screen]
    # host 指网络上远程主机的名称，可以是主机名、IP 地址等。默认的 host 是本地系统。
    # display 代表输出画面的编号。
    # screen 代表屏幕的编号
    #DISPLAY=:0.0


    xinit /usr/bin/xclock -- /usr/bin/X :0
    # 该例子将启动 X server ， 同时将会启动 xclock
    # 在 HOME 下新建 .xinitrc 文件，并加入以下几行：
    xsetroot -solid gray &
    xclock -g 50x50-0+0 -bw 0 &
    xterm -g 80x24+0+0 &
    xterm -g 80x24+0-0 &
    twm   #不能后台，否则所有命令后台 xinit 会退出
    # 当 xinit 启动时，它会先启动 X server ，然后启动一个 clock ，两个 xterm ，最后启动窗口管理器 twm



    # 1)启动 Xserverp
    user@host:~$X :0 &
    # 2)在 Xserver 上启动 xterm
    user@host:~$xterm -display :0 &
    # 在 Xserver 上的 xterm 中执行以初始化一个简单的窗口管理器
    user@host:~$metacity &

    # startx 的默认启动过程为：
    # startx 调用并将系统文件 /etc/X11/xinit/xinitrc 和 /etc/X11/xinit/xserverrc 作为参数传给 xinit ，\
           # xinit 就会先执行系统文件 /etc/X11/xinit/xserverrc 以启动 X Server ，然后执行 /etc/X11/xinit/xinitrc ，\
           # 而 xinitrc 则会执行脚本 /etc/X11/Xsession ，而 Xsession 则会按顺序调用执行 /etc/X11/Xsession.d 目录下的文件
}
```


### qt {#qt}

```sh
qt(){
    /usr/local/Trolltech/Qt-4.8.6/demos/mainwindow

    qmake
    make
    ./mainwindow -qws
}

qt5.3.2(){
    aptitude install gcc g++ build-essential make automake autogen autoconf

    chmod +x qt-opensource-linux-x64-5.6.3.run
    ./qt-opensource-linux-x64-5.6.3.run
    aptitude install mesa-common-dev  #安装OpenGL库
    aptitude install libglu1-mesa-dev #freeglut3-dev #系统缺少链接库

    vim /etc/profile
    #启动QtCreator
    export QTDIR=/opt/Qt5.6.3/Tools/QtCreator
    export PATH=$QTDIR/bin:$PATH
    export MANPATH=$QTDIR/man:$MANPATH
    export LD_LIBRARY_PATH=$QTDIR/lib:$LD_LIBRARY_PATH

    卸载
    /opt/Qt5.3.2/MaintenanceTool
}
```


## System {#system}


### debian9 {#debian9}

```sh
Debian9  (){
    ##1change eth  或者加在 内核启动行
    /etc/default/grub
    GRUB_CMDLINE_LINUX="net.ifnames=0 biosdevname=0"

    grub-mkconfig -o /boot/grub/grub.cfg
}
```


### apt-source {#apt-source}

```sh
apt_source(){
    ###163 源
    deb http://mirrors.163.com/debian/ jessie main non-free contrib
    deb http://mirrors.163.com/debian/ jessie-updates main non-free contrib
    deb http://mirrors.163.com/debian/ jessie-backports main non-free contrib
    deb-src http://mirrors.163.com/debian/ jessie main non-free contrib
    deb-src http://mirrors.163.com/debian/ jessie-updates main non-free contrib
    deb-src http://mirrors.163.com/debian/ jessie-backports main non-free contrib
    deb http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib
    deb-src http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib

    ###中科大源
    deb http://mirrors.ustc.edu.cn/debian jessie main contrib non-free
    deb-src http://mirrors.ustc.edu.cn/debian jessie main contrib non-free
    deb http://mirrors.ustc.edu.cn/debian jessie-proposed-updates main contrib non-free
    deb-src http://mirrors.ustc.edu.cn/debian jessie-proposed-updates main contrib non-free
    deb http://mirrors.ustc.edu.cn/debian jessie-updates main contrib non-free
    deb-src http://mirrors.ustc.edu.cn/debian jessie-updates main contrib non-free}
```


### Ubuntu16 {#ubuntu16}

```sh
Ubuntu16(){
    # 1)root login

    sudo passwd root

    gedit /usr/share/lightdm/lightdm.conf/50-unity-greeter.conf
    add
    greeter-show-manual-login=true	#手工输入登陆系统的用户名和密码
    all-guest=false	#禁用 guest 用户
    autologin-user=root #启动后以 root 身份自动登录

    /etc/pam.d/gdm-autologin
    #auth required pam_succeed_if.so user != root quiet_success
    /etc/pam.d/gdm-password
    #auth required pam_succeed_if.so user != root quiet_success
    /root/.profile
    tty -s&&mesg n || true
}

extlinux(){
    LABEL Linux with (Multi-users)
    kernel  ../../vmlinuz net.ifnames=0 biosdevnames=0 video=DP-1:e  #解决 kvm 切换后，不唤醒的问题
    initrd  ../../initrd.img
    append  root=/dev/${disk}1 ro
    EOF
}
```


### gnome {#gnome}

```sh
gnome(){
卸载 gnome 桌面
apt-get remove gnome-shell  #gnome-shell 主程序
apt-get remove gnome
apt-get autoremove	#不需要的依赖关系
apt-get purge gnome	#gnome 相关配置

apt-get autoclean #安装时遗留的缓存软件包
apt-get clean	#安装时遗留的缓存软件包

}
```


### autologin {#autologin}

```sh
autoLogin(){
    /etc/lightdm/lightdm.conf，找到[SeatDefaults]，下面追加两行：
    autologin-user=root
    autologin-session=true
    # 结合$HOME/.xsessionrc，就可以实现 root 自动登录并自动运行某图形应用。可以用/usr/bin/eog 来验证。
    #自启动应用应该在需要登录的用户的$HOME/.xsessionrc 中追加命令
}
```


### win-mac-linux {#win-mac-linux}

```sh
Windows_Mac_Linux(){
  ASUS:Esc+F10
  LENOVO:F12
}
```


### ftp-mode {#ftp-mode}

```sh

ftp_model(){
# ====登陆指定目录，可 cd 到其他目录
#vim /etc/vsftpd/vsftpd.conf
  user_config_dir=/etc/vsftpd/persure   [添加这一行]
#mkdir /etc/vsftpd/persure
#vim /etc/vsftpd/persure/suername
    local_root=/dir

# ====可以登陆指定目录,且不可以 cd 到其他目录
#vim /etc/vsftpd/vsftpd.conf
    chroot_list_enable=YES
    chroot_list_file=/etc/vsftpd.d/chroot_list
#vim /etc/vsftpd.d/chroot_list
  username

 # ,*********************
chroot_local_user=YES #将所有本地用户限制在自家目录中，NO 则不限制。
chroot_list_enable=YES #是否允许 vsftpd 读取一个提供了用户名的文件
  #如果 chroot_local_user 指令是 YES 的话，则该文件中的用户不会被限制在自家主目录中
  #如果 chroot_local_user 是 NO 的话，则这些用户会被限制。

chroot_list_file=/etc/vsftpd.d/chroot_list
chroot_list_enable=YES
/etc/vsftpd.chroot_list
# 写用户  1.加了用户指定目录  限定在指定的目录里  不可以 cd
        # 2. 没加用户指定目录  【 登录失败: 500 OOPS: vsftpd: refusing to run with writable root inside chroot()】
# 不写用户   不管是否加用户目可以登陆  可以 cd
chroot_list_enable=NO

ftp [IP] [PORT]
ftp> ?;help
  dir;ls
  cd;lcd
  get;mget
  put;mput
  rename;delete;mdelete;rmdir
  quit

}
```


### group {#group}

```cfg
/etc/passwd 用户的信息文件。信息格式为“用户名称：密码：uid：gid：说明：家目录：shell”
/etc/group 用户组的信息文件。信息格式为"组名称：组密码：组 id：组成员"
/etc/shadows 认证信息文件
/etc/skel/.* 默认开启 shell 的配置，用户的骨文件
/home/username 用户的家目录
```


### netbind {#netbind}

```sh
net(){
# 1）一个网口绑定多个 IP
  ip addr add/del 192.168.1.100/24 dev eth0


# 2）多网口绑定一个 IP
　　insmod bonding
　　ifconfig eth0 down
　　ifconfig eth1 down
　　ifconfig bond0 ipaddress
　　ifenslave bond0 eth0
　　ifenslave bond0 eth1

   }
```


### auto-allowhotplug {#auto-allowhotplug}

```sh
auto_allowHotplug(){

    auto eth0
    allow-hotplug eth0
    iface eth0 inet dhcp
    iface eth0 inet static
    address 192.0.2.7
    netmask 255.255.255.0
    gateway 192.0.2.254

    auto #在系统启动的时候启动网络接口,无论网络接口有无连接(插入网线),\
        #如果该接口配置了 DHCP,则无论有无网线,系统都会去执行 DHCP,如果没有插入网线,则等该接口超时后才会继续。
    allow-hotplug #当内核从该接口检测到热插拔事件后才启动该接口。
}
```


### systemctl-journalctl {#systemctl-journalctl}

```sh

systemctl_journalctl(){
  https://www.cnblogs.com/zwcry/p/9602756.html

  systemctl status/start/stop  ${service}
  service  ${service} status/start/stop

  sudo systemctl rescue  # 启动进入救援状态（单用户状态）
  sudo systemd-analyze               		 # 查看启动耗时
  sudo systemd-analyze blame 				 #查看每个服务的启动耗时
  sudo systemd-analyze critical-chain	     #显示瀑布状的启动过程流
  sudo hostnamectl					# 显示当前主机的信息
  sudo hostnamectl set-hostname rhel7 #设置主机名。

  systemctl list-units (--all (--state=inactive)) #列出 正在运行｜所有 |没有运行的服务
  systemctl list-units --type=service
  systemctl list-dependencies  #命令列出一个 Unit 的所有依赖。
  systemctl list-dependencies --all nginx.service

  chkconfig foo on	systemctl enable foo.service		开机自动启动
  chkconfig foo off	systemctl disable foo.service		开机不自动启动
  chkconfig foo		systemctl is-enabled foo.service	查看特定服务是否为开机自动启动
  chkconfig --list	systemctl list-unit-files --type=service

  systemctl is-active application.service # 显示某个 Unit 是否正在运行
  systemctl is-failed application.service # 显示某个 Unit 是否处于启动失败状态
  systemctl is-enabled application.service # 显示某个 Unit 服务是否建立了启动链接

  sudo systemctl kill apache.service
  sudo systemctl reload apache.service  #重新加载一个服务的配置文件
  sudo systemctl daemon-reload ## 重载所有修改过的配置文件
    #一旦修改配置文件，就要让 SystemD 重新加载配置文件，然后重新启动，否则修改不会生效。
  systemctl cat  ? #命令可以查看配置文件的内容。

  #Target 与 传统 RunLevel 的对应关系如下。
  Traditional runlevel      New target name     Symbolically linked to...
  Runlevel 0           |    runlevel0.target -> poweroff.target
  Runlevel 1           |    runlevel1.target -> rescue.target
  Runlevel 2           |    runlevel2.target -> multi-user.target
  Runlevel 3           |    runlevel3.target -> multi-user.target
  Runlevel 4           |    runlevel4.target -> multi-user.target
  Runlevel 5           |    runlevel5.target -> graphical.target
  Runlevel 6           |    runlevel6.target -> reboot.target

  /etc/inittab ->/ etc/systemd/system/default.target
  /etc/init.d  ->/ /lib/systemd/system 和/etc/systemd/system

  sudo journalctl  #-k   查看内核日志（不显示应用日志
  sudo journalctl -b #查看系统本次启动的日志
  sudo journalctl -n 20 #显示尾部指定行数的日志
  sudo journalctl -f # 实时滚动显示最新日志
  sudo journalctl --disk-usage  # 显示日志占据的硬盘空间

  # journalctl -b -u systemd-networkd
  networkctl list	#列出系统上所有设备
}
```


### USB forbiden {#usb-forbiden}

```sh

USB(){
    #禁止
    usbcore.nousb=1

    # m2:
    /lib/modules/`uname -r`/kernel/drivers/usb/storage/usb-storage.ko #usb-storage.ko.bak
}
```


## Kernel {#kernel}


### compile {#compile}

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


### makefile {#makefile}

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


## Tools {#tools}


### VMwareTools {#vmwaretools}

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


### VMwareUdisk {#vmwareudisk}

```sh
add send disk(sata) as boot disk，change bios queen；
del Udisk for error "\\.\PhysicalDrive1"

VMwareClearDisk
~/.cache/vmware/drag_and_drop$ du -d 1 -h

```