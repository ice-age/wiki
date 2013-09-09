###mount 用法:
mount [-参数] [设备名称] [挂载点]

参数:
* -a --all 挂载/etc/fstab中所有的设备
* -f --fake 伪装去挂载
* -v --verbose 打印挂载信息
* -t 挂载类型
* mount --bind olddir newdir
* mount--move olddir newdir
* mount -o loop disk1.iso /mnt/disk 挂载iso
###umount用法

* -n     Unmount without writing in /etc/mtab
* -f 强制卸载
* -l Lazy unmount. Detach the filesystem  from  the  filesystem  hierarchy now,  and  cleanup  all references to the filesystem as soon as it is  not busy anymore.如果umount时提示"device is busy",可以使用-l参数.

