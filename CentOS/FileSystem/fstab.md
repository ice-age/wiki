##一./etc/fstab
fsck、mount、umount的等命令都利用该文件。

cat /etc/fstab

    # /etc/fstab
    # Created by anaconda on Tue Aug  6 11:49:21 2013
    #
    # Accessible filesystems, by reference, are maintained under '/dev/disk'
    # See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
    #
    UUID=ab6092ae-8c1f-4971-925e-4fe2380ef8fe /                       ext4    defaults        1 1
    UUID=2ca94743-485f-4c55-adbd-786660e6c291 /boot                   ext4    defaults        1 2
    UUID=b21d8f99-c0b9-4e5b-9a86-d74f3aaba0e0 /data                   ext4    defaults        1 2
    UUID=cbafb92f-74eb-43ec-a7d1-d75335fa3569 /tmp                    ext4    defaults        1 2
    UUID=be11020a-0cfa-4148-abb7-7f700fe705e8 /usr                    ext4    defaults        1 2
    UUID=33a48769-2a9b-4ee5-8768-d5e23ee04326 /var                    ext4    defaults        1 2
    UUID=5c1000a5-9c2d-41a4-a63f-1f0396bdb52c swap                    swap    defaults        0 0
    tmpfs                   /dev/shm                tmpfs   defaults        0 0
    devpts                  /dev/pts                devpts  gid=5,mode=620  0 0
    sysfs                   /sys                    sysfs   defaults        0 0
    proc                    /proc                   proc    defaults        0 0
    /dev/sdb1	/data/1	ext4	noatime,nodiratime	1 2
    /dev/sdc1	/data/2	ext4	noatime,nodiratime	1 2

* 第一列:要挂载的设备,可以是远程文件系统.可以是设备路径(如/dev/sdb1),也可以是UUID或者volume label.
* 第二列:挂载到哪个位置,swap特殊
* 第三列:文件系统类型
* 第四列:挂载参数

###一.第一列
第一列设备路径(如/dev/sdb1),也可以是UUID或者volume label.参见:e2label

/dev/sda1

LABEL=Boot

UUID=3e6be9de-8139-11d1-9106-a43f08d823a6

###二.第二列


###三.第三列
参见:/proc/filesystems

###四.第四列
参见:mount

####auto / noauto
With the auto option, the device will be mounted automatically at bootup or when the mount -a command is issued. auto is the default option. If you do not want the device to be mounted automatically, use the noauto option in /etc/fstab. With noauto, the device can be only mounted explicitly.
####dev / nodev
Interpret/do not interpret block special devices on the filesystem.
####exec / noexec
exec lets you execute binaries that are on that partition, whereas noexec does not let you do that. noexec might be useful for a partition that contains no binaries, like /var, or contains binaries you do not want to execute on your system, or that cannot even be executed on your system, as might be the case of a Windows partition.
####rw / ro
Mount the filesystem in either read write or read only mode. Explictly defining a file system as rw can alleviate some problems in file systems that default to read only, as can be the case with floppies or Ntfs partitions.
####sync / async
How the input and output to the filesystem should be done. sync means it is done synchronously. If you look at the example fstab, you will notice that this is the option used with the floppy. In plain English, this means that when you, for example, copy a file to the floppy, the changes are physically written to the floppy at the same time you issue the copy command.
####suid / nosuid
Permit/Block the operation of suid, and sgid bits.
####user / users / nouser
user permits any user to mount the filesystem. This automatically implies noexec, nosuid, nodev unless overridden. If nouser is specified, only root can mount the filesystem. If users is specified, every user in group users will be able to unmount the volume.
####defaults
Use default settings. Default settings are defined per file system at the file system level. For ext3 file systems these can be set with the tune2fs command. The normal default for Ext3 file systems is equivalent to rw,suid,dev,exec,auto,nouser,async(no acl support). Modern Red Hat based systems set acl support as default on the root file system but not on user created Ext3 file systems. Some file systems such as XFS enable acls by default. Default file system mount attributes can be overridden in /etc/fstab.
####owner (Linux-specific)
Permit the owner of device to mount.
####atime / noatime / relatime / strictatime (Linux-specific)
The Unix stat structure records when files are last accessed (atime), modified (mtime), and changed (ctime). One result is that atime is written every time a file is read, which has been heavily criticized for causing performance degradation and increased wear. However, atime is used by some applications and desired by some users, and thus is configurable as atime (update on access), noatime (do not update), or (in Linux) relatime (update atime if older than mtime). Through Linux 2.6.29, atime was the default; as of 2.6.30 (9 June 2009), relatime is the default.[1] 
####errors={continue|remount-ro|panic}
Define  the  behaviour  when an error is encountered.  (Either ignore errors and just mark the filesystem erroneous and continue, or remount the filesystem read-only, or panic and halt the system.)  The default is set in the filesystem superblock, and can be changed using tune2fs(8).
####sync / async  
sync所有的I/O将以同步方式进行
async  所有的I/O将以非同步方式进行
####iocharset＝
在＝号后面加入你的本地编码，似乎在这个设备（分区）中做文件IO的时候就会自动做编码的格式转换。例如：你的某个分区是编码是utf8，而设备中文件的编码是gb2312，当是复制你设备中的文件到你的这个分区时，它将自动做编码转换。  
####nls=
在=号后面加入你的本地编码，你的中文就不会出现乱码。
####exec /noexec
####user /nouser
####suid /nosuid







##/proc/filesystems

##e2label

