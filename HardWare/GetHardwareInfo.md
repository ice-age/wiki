##1.查看机器所有硬件信息:
* dmidecode |more
* dmesg |more

##2.查看CPU信息
* cat /proc/cpuinfo |more
* dmesg | grep CPU

###查看CPU的位数
* getconf LONG_BIT

##3.查看Mem信息
* cat /proc/meminfo
* free -m
* top

##4.查看磁盘信息
* fdisk -l 可以看到系统上的磁盘(包括U盘)的分区以及大小相关信息。
* cat /proc/partitions

##5.查看网卡信息
* ethtool eth0 采用此命令可以查看到网卡相关的技术指标不一定所有网卡都支持此命令）
* ethtool -i eth1 加上 -i 参数查看网卡驱动   可以尝试其它参数查看网卡相关技术参数
* cat /etc/sysconfig/network-scripts/ifcfg-eth0 可以看到当前的网卡配置包括IP、网关地址等信息。
* ifconfig

##6.如何查看主板信息？
lspci

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