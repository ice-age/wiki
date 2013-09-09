##Ext2

###Blocks and Fragments(碎片)

Blocks是组成文件系统的基本单位.

如果文件的大小不是block大小的整数倍,会有一个block的空间被浪费掉.为了规避这个问题,引入fragments.

Fragments节省空间,尤其是有很多小文件的时候.但是增加了磁头的移动和寻道时间.

Louis-Dominique Dubeau写的关于ext2架构分析的文章,有点老了1998年之前写的.

http://undergraduate.csse.uwa.edu.au/units/CITS1002/fs-ext2/

##Ext3
 
ext3不支持block fragmentation,因此一个1B大的文件会占用整个块的空间.UFS文件系统支持每个块分成四个fragments.fragments是计划中的特性,现在还没实现.

http://unix.stackexchange.com/questions/16307/what-is-a-fragment-size-in-an-ext3-filesystem