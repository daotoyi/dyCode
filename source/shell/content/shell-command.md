---
title: "COMMAND"
lastmod: "2022-12-10 16:26:05"
categories: ["Shell"]
draft: false
toc: true
---

## skill {#skill}

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


## apt {#apt}

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


## ag {#ag}

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


## lsof {#lsof}

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


## crontab {#crontab}

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


## cpio {#cpio}

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


## dpkg-deb {#dpkg-deb}

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


## tar {#tar}

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


## dd {#dd}

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


## dd-Swap {#dd-swap}

```sh

dd if=/dev/zero of=/swapfile bs=1024 count=262144 #创建一个足够大的文件（此处为 256M）
mkswap /swapfile #把这个文件变成 swap 文件
swapon /swapfile #启用这个 swap 文件
/swapfile swap swap defaults 0 0 #在每次开机的时候自动加载 swap 文件, 需要在 /etc/fstab 文件中增加一行
```


## blockdev {#blockdev}

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


## jobs {#jobs}

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


## nohup {#nohup}

> 使用 &amp; 命令后，作业被提交到后台运行，当前控制台没有被占用，但是一但把当前控制台关掉 (退出帐户时)，作业就会停止运行。
> nohup 命令可以在你退出帐户之后继续运行相应的进程。nohup 就是不挂起的意思 ( no hang up)。该命令的一般形式为：
> nohup command &amp;
> 如果使用 nohup 命令提交作业，那么在缺省情况下该作业的所有输出都被重定向到一个名为 nohup.out 的文件中，除非另外指定了输出文件：
> nohup command &gt; myout.file 2&gt;&amp;1 &amp;


## trap {#trap}

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


## bomb {#bomb}

\#+begin_src sh

bomb (){

	bomb | bomb &amp;
}


## dos2unix {#dos2unix}

\#+begin_src sh

\_dos2unix (){

vim
	:set ff?　查看文件格式
	:%s/^M//g	#注意同时按 Ctrl -v -m 输入 ^M
	:%s//r//g	#
	:set ff=unix

	sed 's/^M//' filename &gt; tmp_filename
	tr -d "\\015" dos_file.txt
	cat dos_file.txt | perl -pe '~s/\r//g' &gt; dos_file.txt
}


## cp {#cp}

\#+begin_src sh

-   cp

cp _home/usr/dir/{file1,file2,file3,file4} /home/usr/destination_

-   conman pre./

cp _home/usr/dir/file{1..4} ._


## mv {#mv}

\#+begin_src sh

移动多个文件

-   参数 t

$ mv a b c -t d
$ mv -t d a b c


## rpm {#rpm}

\#+begin_src sh

\_rpm(){
rpm -ivh --nodeps --force XXX
}


## stty {#stty}

\#+begin_src sh

\_stty (){
	stty -F /dev/ttyS5 ispeed 115200 ospeed 115200 raw -echo
	stty -F /dev/ttyS2 peed 115200 parodd

　　RAW 模式简单的来说，是发送端发动的二进制码原封不动的被接收端接收
    非 RAW 模式下，系统会对串口收到的数据中某些具有特殊意义的字符或组合进行转义.
    在 Linux 下系统的 tty 模式为非 RAW 模式，如果要调试单片机这种嵌入式设备，则需要将串口 设置为 RAW 模式。

stty -F /dev/ttyS0 speed 115200  cs8 -parenb -cstopb

其中"-"表示未设置状态，因此该串口设备默认的参数是： ****9600bps 波特率、8位数据位、无校验、1位停止位、无硬件流控****

exec &gt; /dev/ttyS5
exec &lt; /dev/ttyS5

while true;
do read line
done

	stty -F /dev/ttySx  raw -echo
}


## case {#case}

\#+begin_src sh

\_case (){
case "${UTC}" in
	yes|true|1)
		;;
	no|false|0)
		;;
	\*)
		;;
esac

while true
do
  read -r -p "**\***, are you sure? [y/n] " input

		case $input in
			[yY][eE][sS]|[yY])
				;;
			[nN][oO]|[nN])
				;;
			\*)
				;;
		esac
}


## shift {#shift}

\#+begin_src sh

\_shift (){
echo "参数个数为：$#,其中："
for i in $(seq 1 $#)
do
  eval j=\\$$i
  echo "第\\(i 个参数(\\)"$i")：$j"
done

shift 3

echo "执行 shift 3 操作后："
echo "参数个数为：$#,其中："
for i in $(seq 1 $#)
do
  #通过 eval 把 i 变量的值($i)作为变量 j 的名字
  eval j=\\$$i
  echo "第\\(i 个参数(\\)"$i")：$j"
done
}
\_eval (){
    if [ -f $config_file ]; then

cp -v \\(config\_file  /tmp/
        config\_file=/tmp/\\)(basename $config_file)
dos2unix $config_file

while read line;
do

echo $line | grep '^ \*#' &gt; /dev/null &amp;&amp; continue;

[ -z $line ] &amp;&amp; continue;

    eval "export $line";
done &lt; $config_file;

        rm $config_file
    fi
}


## set {#set}

\#+begin_src sh

\_set (){
set -o nounset  # -u
set -o errexit  # -e
}


## sed {#sed}

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


## PS1 {#ps1}

\#+begin_src sh

\_PS1 (){

\\[\e[32;40m\\] {\u} \\[\e[0m\\]
\e[32;40m\\] {\u} \e[0m\\]

	export PS1="\\[\e[37;40m\\][\\[\e[32;40m\\]\u\\[\e[37;40m\\]@\\[\e[33;40m\h\e[0m \e[36;40m\\]\w\\[\e[0m\\]]\\\\$ "
}


## mount {#mount}

\#+begin_src sh

\_mount (){
mount -t vfat -o iocharset=cp936 /dev/sdd1 /mnt/usb   #若汉字文件名显示为乱码或不显示
	-o options 主要用来描述设备或档案的挂接方式。常用的参数有：
	loop：用来把一个文件当成硬盘分区挂接上系统
	ro：采用只读方式挂接设备
	rw：采用读写方式挂接设备
	iocharset：指定访问文件系统所用字符集

}

remount(){
mount -o remount,rw /
mount -o remount,rw /dev/sda1
}


## top {#top}

\#+begin_src sh

\_top(){
sh -c top -b -n 2|grep Cpu |cut -d "," -f 1|cut -d ":" -f 2
}


## vim {#vim}

\#+begin_src sh

\_vi_vim(){
yy---复制当前；
p---粘贴当前
dd---删除当前行
nyy---复制多行(比如 3yy，复制 3 行)
ndd---删除多行
np---复制多遍
}


## ethtool {#ethtool}

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


## tmux {#tmux}

\#+begin_src sh

\_tmux(){
Ctrl-B d， detach
Ctrl+b %：划分左右两个窗格。
Ctrl+b '"'：划分上下两个窗格。
Ctrl+b &lt;arrow key&gt;：光标切换到其他窗格。&lt;arrow key&gt;是指向要切换到的窗格的方向键，比如切换到下方窗格，就按方向键↓。
Ctrl+b ;：光标切换到上一个窗格。
Ctrl+b o：光标切换到下一个窗格。
Ctrl+b {：当前窗格左移。
Ctrl+b }：当前窗格右移。
Ctrl+b Ctrl+o：当前窗格上移。
Ctrl+b Alt+o：当前窗格下移。
Ctrl+b x：关闭当前窗格。
Ctrl+b !：将当前窗格拆分为一个独立窗口。
Ctrl+b z：当前窗格全屏显示，再使用一次会变回原来大小。
Ctrl+b Ctrl+&lt;arrow key&gt;：按箭头方向调整窗格大小。
Ctrl+b q：显示窗格编号。

}