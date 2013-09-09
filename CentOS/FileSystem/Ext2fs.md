
###Blocks and Fragments

Blocks是组成文件系统的基本单位.

如果文件的大小不是block大小的整数倍,会有一个block的空间被浪费掉.为了规避这个问题,引入fragments.


Louis-Dominique Dubeau写的关于ext2架构分析的文章,有点老了1998年之前写的.

http://undergraduate.csse.uwa.edu.au/units/CITS1002/fs-ext2/