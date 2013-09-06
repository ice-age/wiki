##1.Read-only file system
###引起文件系统只读的原因:
* 硬盘问题
* 硬盘IO太高

如果在挂载时指定errors=remount-ro,当文件系统遇到问题时,就会进入Read-only状态.

###解决办法
查看dmesg

umount

fsck:sudo fsck -Af -M(-M不去检测已挂载的文件系统)

mount

还不行reboot

还不行换盘

还可以remount,但是不推荐,一个原因是没法找出是否是硬件故障,第二个原因是可能没法remount

(mount -o remount rw / )