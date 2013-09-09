##一.Ext2

###Blocks and Fragments(碎片)

Blocks是组成文件系统的基本单位.

如果文件的大小不是block大小的整数倍,会有一个block的空间被浪费掉.为了规避这个问题,引入fragments.

Fragments节省空间,尤其是有很多小文件的时候.但是增加了磁头的移动和寻道时间.

http://en.wikipedia.org/wiki/File_system_fragmentation

Louis-Dominique Dubeau写的关于ext2架构分析的文章,有点老了1998年之前写的.

http://undergraduate.csse.uwa.edu.au/units/CITS1002/fs-ext2/

##二.Ext3

ext3是一个日志文件系统(Journaling file system),既当发生变化时,先把相关信息写入到日志区域,再把变化写入到主文件系统的文件系统.当文件系统发生故障(如内核崩溃或者断电)时,日志文件系统更容易保持一致性,可以较快恢复.

Block size 	Maximum file size 	Maximum file system size

1 KiB 	16 GiB 	2 TiB

2 KiB 	256 GiB 	8 TiB

4 KiB 	2 TiB 	16 TiB

8 KiB 	2 TiB 	32 TiB

ext3不支持block fragmentation,因此一个1B大的文件会占用整个块的空间.UFS文件系统支持每个块分成四个fragments.fragments是计划中的特性,现在还没实现.

http://unix.stackexchange.com/questions/16307/what-is-a-fragment-size-in-an-ext3-filesystem

##三.Ext4 
###特性
####兼容ext3

####更大的文件系统和单个文件大小
* 文件系统最大:1EB=1024PB=1024^2TB
* 单个文件最大:16TB

####子目录的扩展性
每个目录最能能有64000个子目录,ext3最大支持32000

####Extents
连续的块

####Multiblock allocation

####Delayed allocation

####Fast fsck

####Journal checksumming 

####"No Journaling" mode 

####Online defragmentation 

####Inode-related features 

####Persistent preallocation 

####Barriers on by default 


##四.维护工具e2fsprogs
###1.e2fsprogs是用以维护ext2，ext3和ext4文件系统的工具程序集,包括:
* e2fsck:一个fsck程序,用来检查和纠正不一致
* mke2fs:用来创建ext2，ext3和ext4文件系统
* resize2fs:扩展或者缩小ext2，ext3和ext4文件系统的大小
* tune2fs:修改文件系统参数
* dumpe2fs:打印superblock和block group信息
* debugfs:用于手动查看或者修改文件系统的内部结构
* filefrag:奥文件fragmentation
* logsave:将一个命令的输出保存到一个日志文件
* e2undo:replay undo日志
* e2label:修改label
* findfs:通过label或者UUID查找文件系统呢
* badblocks:搜索坏块
* blkid:定位/打印块设备属性
* e2freefrag:报告空余空间fragmentation信息
* e2image:save critical ext2/ext3/ext4 filesystem metadata to a file
* e4defrag:只针对ext4,在线碎片整理
* findsuper:搜索ext2 superblocks
* lsattr:列出文件的属性
* chattr:修改文件的属性

###2.fsck  

* -A /etc/fstab中所有的分区
* -a 自动修复(这个选项比较危险)
* -f 强制检测
* -M 不去检测已挂载的文件系统
* -c 检测硬盘坏道
* -y 
* -t 类型.fsck -t ext4相当于fsck.ext4
* fdisk -A -a

This command tells fdisk to run through /etc/fstab and check each partition entered there (-A), and to automatically fix any errors without confirmation (-a). Given my choice of ext4 and mount options, there's a small chance I've lost some writes in this process. Be careful when choosing automatic repairs (-a) -- make sure that's really what you want!
###3.mkfs

###4.fdisk