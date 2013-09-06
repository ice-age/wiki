##1.Read-only file system
###引起文件系统只读的原因:
* 硬盘问题
* 硬盘IO太高
###解决办法
umount

fdisk

mount

还不行reboot

还不行换盘

还可以remount,但是不推荐,一个原因是没法找出是否是硬件故障,第二个原因是可能没法remount

(mount -o remount rw / )