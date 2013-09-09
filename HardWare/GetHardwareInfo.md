##1.查看机器所有硬件信息:
* dmidecode |more
* dmesg |more

* 查看服务器型号：dmidecode |grep 'Product Name'
* 查看系统序列号：sudo dmidecode -s system-serial-number

dmidecode -t 1,13 or dmidecode -t bios

bios 0,13

system 1,12,32

baseboard 2,41（很多个）

——————————————————————————————

Desc    DMI Type    type

——————————————————————————————

bios    0,13

——————————————————————————————

system    1,12,32

——————————————————————————————

baseboard    2,41    Ethernet

——————————————————————————————

    dmidecode -t slot|grep Type|sort|uniq -c
    ssh 10.10.54.19 "echo -en \"\t\"  $HOSTNAME && echo -en \"\t\"  $(ifconfig|grep 10.10.54|awk '{print $2}'|awk -F : '{print $2}') &&  echo  -en \"\t\"  $(dmidecode -t system |grep "Serial Number"|awk '{print $3}') && echo -en \"\t\" $(dmidecode -t system |grep "Product Name" |awk '{print $3,$4}') && echo -en \"\t\" $(dmidecode -t memory|grep -E "Speed: 1600 MHz"|sort|uniq -c|awk '{print $1}') echo -en \"\t\" $(/opt/MegaRAID/MegaCli/MegaCli64 -PDList -aALL|grep "Raw Size"|sort|uniq -c|awk '{print $4,$5,"*"$1}')"
    

* lshw(Hardware Lister)是另外一个可以查看硬件信息的工具，不仅如此，它还可以用来做一些硬件的benchmark。

这个工具其实就是用/proc里面读取一些文件来显示相关的信息，它用到了如下文件和目录(下的文件)：
    /proc/cpuinfo  显示CPU信息
    /proc/bus/pci  显示pci信息
    /proc/scsi   显示scsi信息
    /proc/net/dev  显示网络设备信息
    /proc/kcore   从内存映像读取相关信息
    /proc/ide   显示IDE设备信息
    /proc/devices
/proc/mounts
/proc/fstab

##2.查看CPU信息
* cat /proc/cpuinfo |more
* dmesg | grep CPU
* lscpu

* 查看cpu频率：cat /proc/cpuinfo |grep 'cpu MHz'
* 查看一个物理CPU有几个核：cat /proc/cpuinfo |grep  cores
* 查看一个物理CPU有几个逻辑CPU：cat /proc/cpuinfo |grep  siblings
* 查看cpu型号：cat /proc/cpuinfo |grep  name|cut -f2 -d: |uniq -c
* 查看cpu个数：cat /proc/cpuinfo |grep 'physical id'|uniq -c


###查看CPU的位数
* getconf LONG_BIT

##3.查看Mem信息
* cat /proc/meminfo
* free -m
* top

##4.查看磁盘信息
* fdisk -l 可以看到系统上的磁盘(包括U盘)的分区以及大小相关信息。
* cat /proc/partitions
* hdparm -i /dev/sda

##5.查看网卡信息
* ethtool eth0 采用此命令可以查看到网卡相关的技术指标不一定所有网卡都支持此命令）
* ethtool -i eth1 加上 -i 参数查看网卡驱动   可以尝试其它参数查看网卡相关技术参数
* cat /etc/sysconfig/network-scripts/ifcfg-eth0 可以看到当前的网卡配置包括IP、网关地址等信息。
* ifconfig
* 查看网卡型号 lspci ｜grep Eth ; lspci -vv
*  modinfo pcnet32 （所有版本的网卡驱动基本上都在 /lib/modules/2.6.18-194.el5/kernel/drivers/net）

##6.如何查看主板信息？
* lspci 命令来列举所有的 PCI 设备

* 主板支持最大内存：sudo dmidecode -t 16 |grep Maximum

##7.如何挂载ISO文件
mount -o loop *.iso mount_point

##8.如何查看光盘相关信息

插入CD光碟后，在本人的RHEL5系统里，光碟文件是 /dev/cdrom，因此只需 mount /dev/cdrom mount_point 即可。

##9.如何查看USB设备相关

方法一：

其实通过 fdisk -l 命令可以查看到接入的U盘信息，本人的U盘信息如下：
 
   Disk /dev/sda: 2012 MB, 2012217344 bytes
   16 heads, 32 sectors/track, 7676 cylinders
   Units = cylinders of 512 * 512 = 262144 bytes
 
      Device Boot      Start         End      Blocks   Id  System
   /dev/sda1   *          16        7676     1961024    b  W95 FAT32
 
   U盘的设备文件是 /dev/sda，2G大小，FAT32格式。
 
   如果用户登陆的不是Linux图形界面，U盘不会自动挂载上来。
   此时可以通过手工挂载(mount)：
   mount /dev/sda1 mount_point
   以上命令将U盘挂载到当前目录的 mount_point 目录，注意挂的是 sda1 不是 sda。
   卸载命令是 umount mount_point
 
   Linux默认没有自带支持NTFS格式磁盘的驱动，但对FAT32支持良好，挂载的时候一般不需要 -t vfat 参数 。
   如果支持ntfs，对ntfs格式的磁盘分区应使用 -t ntfs 参数。
   如果出现乱码情况，可以考虑用 -o iocharset=字符集 参数。
 
   可以通过 lsusb 命令查看 USB 设备信息哦：
 
   [root@miix tmp]# lsusb
   Bus 001 Device 001: ID 0000:0000
   Bus 002 Device 001: ID 0000:0000
   Bus 003 Device 001: ID 0000:0000
   Bus 004 Device 002: ID 0951:1613 Kingston Technology
   Bus 004 Device 001: ID 0000:0000

##查看raid信息
###软件raid
cat /proc/mdstat 可以看到raid级别，状态等信息。

###硬件raid
* 最佳的办法是通过已安装的raid厂商的管理工具来查看.Adaptec公司的硬件卡就可以通过下面的命令进行查看：/usr/dpt/raidutil -L all
* dmesg |grep -i raid
* cat /proc/scsi/scsi
* lspci

转一篇megacli用法的文档,找不到出处了
##MegaCli

###1.命令使用：

    MegaCli -AdpAllInfo -aALL 查raid卡信息
    MegaCli -AdpBbuCmd -aAll 查看电池信息
    MegaCli -FwTermLog -Dsply -aALL 查看raid卡日志
    MegaCli -adpCount 【显示适配器个数】
    MegaCli -AdpGetTime –aALL 【显示适配器时间】
    MegaCli -LDInfo -LALL -aAll    【显示所有逻辑磁盘组信息】
    MegaCli -PDList -aAll    【显示所有的物理信息】
    MegaCli -AdpBbuCmd -GetBbuStatus -aALL |grep ‘Charger Status’ 【查看充电状态】
    MegaCli -AdpBbuCmd -GetBbuStatus -aALL【显示BBU状态信息】
    MegaCli -AdpBbuCmd -GetBbuCapacityInfo -aALL【显示BBU容量信息】
    MegaCli -AdpBbuCmd -GetBbuDesignInfo -aALL    【显示BBU设计参数】
    MegaCli -AdpBbuCmd -GetBbuProperties -aALL    【显示当前BBU属性】
    MegaCli -cfgdsply -aALL    【显示Raid卡型号，Raid设置，Disk相关信息】

###2.磁带状态的变化，从拔盘，到插盘的过程中。
    Device       |Normal|Damage|Rebuild|Normal
    Virtual Drive   |Optimal|Degraded|Degraded|Optimal
    Physical Drive   |Online|Failed –> Unconfigured|Rebuild|Online

###3.更新
新版本的 MegaCli-1.01.24-0.i386.rpm 会把程序安装在/opt下，可以自定义安装目录，例如：
rpm –relocate /opt/=/usr/sbin/ -i MegaCli-1.01.24-0.i386.rpm.即把安装目录 /opt 替换成 /usr/sbin。

###4.查看磁盘缓存策略

    MegaCli -LDGetProp -Cache -L0 -a0
    MegaCli -LDGetProp -Cache -L1 -a0
    MegaCli -LDGetProp -Cache -LALL -a0
    MegaCli -LDGetProp -Cache -LALL -aALL
    MegaCli -LDGetProp -DskCache -LALL -aALL

###5、设置磁盘缓存策略
缓存策略解释：

    WT    (Write through
    WB    (Write back)
    NORA (No read ahead)
    RA    (Read ahead)
    ADRA (Adaptive read ahead)
    Cached
    Direct
例子：

    MegaCli -LDSetProp WT|WB|NORA|RA|ADRA -L0 -a0
    MegaCli -LDSetProp -Cached|-Direct -L0 -a0
    MegaCli -LDSetProp -EnDskCache|-DisDskCache -L0 -a0

###6.创建/删除 阵列
####1 创建一个 raid5 阵列，由物理盘 2,3,4 构成，该阵列的热备盘是物理盘 5

    MegaCli -CfgLdAdd -r5 [1:2,1:3,1:4] WB Direct -Hsp[1:5] -a0
####2 创建阵列，不指定热备

    MegaCli -CfgLdAdd -r5 [1:2,1:3,1:4] WB Direct -a0
####3 删除阵列

    MegaCli -CfgLdDel -L1 -a0
####4 在线添加磁盘

    MegaCli -LDRecon -Start -r5 -Add -PhysDrv[1:4] -L1 -a0

意思是，重建逻辑磁盘组1，raid级别是5，添加物理磁盘号：1:4。重建完后，新添加的物理磁盘会自动处于重建(同步)状态，这个 时候 fdisk -l是看不到阵列的空间变大的，只有在系统重启后才能看见。如果该阵列下只有一个分区的话，那么该分区也直接增大，如果有多个分区，不知道该怎么分配新增空间了？有空试试看，呵呵

###7查看阵列初始化信息
####1 阵列创建完后，会有一个初始化同步块的过程，可以看看其进度。

    MegaCli -LDInit -ShowProg -LALL -aALL
或者以动态可视化文字界面显示

    MegaCli -LDInit -ProgDsply -LALL -aALL
####2 查看阵列后台初始化进度

    MegaCli -LDBI -ShowProg -LALL -aALL
或者以动态可视化文字界面显示

    MegaCli -LDBI -ProgDsply -LALL -aALL
###8.创建全局热备
####指定第 5 块盘作为全局热备

    MegaCli -PDHSP -Set [-EnclAffinity] [-nonRevertible] -PhysDrv[1:5] -a0
####也可以指定为某个阵列的专用热备

    MegaCli -PDHSP -Set [-Dedicated [-Array1]] [-EnclAffinity] [-nonRevertible] -PhysDrv[1:5] -a0
###9.删除全局热备

    MegaCli -PDHSP -Rmv -PhysDrv[1:5] -a0
###10.将某块物理盘下线/上线

    MegaCli -PDOffline -PhysDrv [1:4] -a0
    MegaCli -PDOnline -PhysDrv [1:4] -a0
###11.查看物理磁盘重建进度

    MegaCli -PDRbld -ShowProg -PhysDrv [1:5] -a0
或者以动态可视化文字界面显示

    MegaCli -PDRbld -ProgDsply -PhysDrv [1:5] -a0

##监控温度
* lm-sensor