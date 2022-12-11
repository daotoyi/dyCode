---
title: "SHELL"
lastmod: "2022-12-10 11:59:27"
categories: ["Shell"]
draft: false
toc: true
---

## basic {#basic}


### whiptail {#whiptail}

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


### get-path {#get-path}

```sh
DIR_PWD=$(dirname $(readlink -f "$0"))
DIR_PWD=$(cd `dirname $0` && pwd)
DIR_PWD=$(cd `dirname $0` ; pwd)
```


### note/comment {#note-comment}

```sh
: << !
!

: << 'COMMENT'

COMMENT

: '

'
```


### linux-version {#linux-version}

```sh
lsb_release -a
cat /etc/issue

cat /etc/redhat-release
cat /etc/debian_version

cat /proc/version
```


### delay-loop {#delay-loop}

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


### check-machine {#check-machine}

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


### source.lst {#source-dot-lst}

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


## sys-install {#sys-install}

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


## insmod-drive {#insmod-drive}

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


## disk-search {#disk-search}


### search-desk-disk0 {#search-desk-disk0}

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


### search_dest_disk {#search-dest-disk}

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


### get-unit {#get-unit}

```sh
get_unit(){
local disk=$1
fdisk -l 2> /dev/null | grep "Disk /dev/${disk}" | cut -f 4 -d " " | cut -f 1 -d ','
}
```


### get-size {#get-size}

```shell
get_size (){
  local disk=$1
  fdisk -l 2> /dev/null | grep "Disk /dev/${disk}" | cut -f 3 -d " " | cut -f 1 -d .
}
```


### search-desk-disk2 {#search-desk-disk2}

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


### search_dest_disk_3 {#search-dest-disk-3}

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


### search_usb_disks {#search-usb-disks}

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


## disk-part {#disk-part}


### create_part_fdisk {#create-part-fdisk}

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


### create_part_eof {#create-part-eof}

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


### clean-disk {#clean-disk}

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


### create-partition {#create-partition}

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


### delete_partition {#delete-partition}

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


## uuid-gen {#uuid-gen}

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


## uuid-set {#uuid-set}

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


## menu.lst {#menu-dot-lst}

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


## grub2 {#grub2}

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


## mount {#mount}


### mount-fat32 {#mount-fat32}

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


### mount-doart {#mount-doart}

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


### mount-iso-apt {#mount-iso-apt}

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


## mountpoint {#mountpoint}

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


## debian7 {#debian7}

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


## debian8.1 {#debian8-dot-1}

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


## zhcon-unicode {#zhcon-unicode}

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


## snmp {#snmp}

```shell
snmp (){

    dpkg --configure -a

    # Q: Package libkrb53 is not configured yet.
    #stackoverflow
    # A:run apt-get update / apt-get dist-upgrade, accept the failures, then reboot, then run both again. Now its OK.
}
```


## x11 {#x11}

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


## qt {#qt}

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