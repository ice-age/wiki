##1.Read-only file system
###引起文件系统只读的原因:
* 硬盘问题
* 硬盘IO太高

如果在挂载时指定errors=remount-ro,当文件系统遇到问题时,就会进入Read-only状态.

###解决办法
查看dmesg

umount

最好远程备份

fsck:sudo fsck -Af -M(-M不去检测已挂载的文件系统)

mount

还不行reboot

(单用户,卸载,fsck,挂载)

还不行换盘

还可以remount,但是不推荐,一个原因是没法找出是否是硬件故障,第二个原因是可能没法remount

(mount -o remount rw / )

##2.去掉一块硬盘,但是没有修改/etc/fstab,启动报错

    Give root password for maintenance
    (or type Control-D to continue):

ctrl+d,输入root密码后
    
    mount -o remount,rw /

然后修改/etc/fstab   