---
title: "SYSTEM"
lastmod: "2022-12-10 12:13:46"
categories: ["Shell"]
draft: false
toc: true
---

## debian9 {#debian9}

```sh
Debian9  (){
    ##1change eth  或者加在 内核启动行
    /etc/default/grub
    GRUB_CMDLINE_LINUX="net.ifnames=0 biosdevname=0"

    grub-mkconfig -o /boot/grub/grub.cfg
}
```


## apt-source {#apt-source}

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


## Ubuntu16 {#ubuntu16}

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


## gnome {#gnome}

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


## autologin {#autologin}

```sh
autoLogin(){
    /etc/lightdm/lightdm.conf，找到[SeatDefaults]，下面追加两行：
    autologin-user=root
    autologin-session=true
    # 结合$HOME/.xsessionrc，就可以实现 root 自动登录并自动运行某图形应用。可以用/usr/bin/eog 来验证。
    #自启动应用应该在需要登录的用户的$HOME/.xsessionrc 中追加命令
}
```


## win-mac-linux {#win-mac-linux}

```sh
Windows_Mac_Linux(){
  ASUS:Esc+F10
  LENOVO:F12
}
```


## ftp-mode {#ftp-mode}

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


## group {#group}

```cfg
/etc/passwd 用户的信息文件。信息格式为“用户名称：密码：uid：gid：说明：家目录：shell”
/etc/group 用户组的信息文件。信息格式为"组名称：组密码：组 id：组成员"
/etc/shadows 认证信息文件
/etc/skel/.* 默认开启 shell 的配置，用户的骨文件
/home/username 用户的家目录
```


## netbind {#netbind}

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


## auto-allowhotplug {#auto-allowhotplug}

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


## systemctl-journalctl {#systemctl-journalctl}

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


## USB forbiden {#usb-forbiden}

```sh

USB(){
    #禁止
    usbcore.nousb=1

    # m2:
    /lib/modules/`uname -r`/kernel/drivers/usb/storage/usb-storage.ko #usb-storage.ko.bak
}
```