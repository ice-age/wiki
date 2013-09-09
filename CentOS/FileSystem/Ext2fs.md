##Ext2

###Blocks and Fragments(碎片)

Blocks是组成文件系统的基本单位.

如果文件的大小不是block大小的整数倍,会有一个block的空间被浪费掉.为了规避这个问题,引入fragments.

Fragments节省空间,尤其是有很多小文件的时候.但是增加了磁头的移动和寻道时间.

http://en.wikipedia.org/wiki/File_system_fragmentation

Louis-Dominique Dubeau写的关于ext2架构分析的文章,有点老了1998年之前写的.

http://undergraduate.csse.uwa.edu.au/units/CITS1002/fs-ext2/

##Ext3
 
ext3不支持block fragmentation,因此一个1B大的文件会占用整个块的空间.UFS文件系统支持每个块分成四个fragments.fragments是计划中的特性,现在还没实现.

http://unix.stackexchange.com/questions/16307/what-is-a-fragment-size-in-an-ext3-filesystem

##Ext4 
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
