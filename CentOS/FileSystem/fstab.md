
/etc/fstab


auto / noauto
    With the auto option, the device will be mounted automatically at bootup or when the mount -a command is issued. auto is the default option. If you do not want the device to be mounted automatically, use the noauto option in /etc/fstab. With noauto, the device can be only mounted explicitly.
dev / nodev
    Interpret/do not interpret block special devices on the filesystem.
exec / noexec
    exec lets you execute binaries that are on that partition, whereas noexec does not let you do that. noexec might be useful for a partition that contains no binaries, like /var, or contains binaries you do not want to execute on your system, or that cannot even be executed on your system, as might be the case of a Windows partition.
rw / ro
    Mount the filesystem in either read write or read only mode. Explictly defining a file system as rw can alleviate some problems in file systems that default to read only, as can be the case with floppies or Ntfs partitions.
sync / async
    How the input and output to the filesystem should be done. sync means it is done synchronously. If you look at the example fstab, you will notice that this is the option used with the floppy. In plain English, this means that when you, for example, copy a file to the floppy, the changes are physically written to the floppy at the same time you issue the copy command.
suid / nosuid
    Permit/Block the operation of suid, and sgid bits.
user / users / nouser
    user permits any user to mount the filesystem. This automatically implies noexec, nosuid, nodev unless overridden. If nouser is specified, only root can mount the filesystem. If users is specified, every user in group users will be able to unmount the volume.
defaults
    Use default settings. Default settings are defined per file system at the file system level. For ext3 file systems these can be set with the tune2fs command. The normal default for Ext3 file systems is equivalent to rw,suid,dev,exec,auto,nouser,async(no acl support). Modern Red Hat based systems set acl support as default on the root file system but not on user created Ext3 file systems. Some file systems such as XFS enable acls by default. Default file system mount attributes can be overridden in /etc/fstab.
owner (Linux-specific)
    Permit the owner of device to mount.
atime / noatime / relatime / strictatime (Linux-specific)
    The Unix stat structure records when files are last accessed (atime), modified (mtime), and changed (ctime). One result is that atime is written every time a file is read, which has been heavily criticized for causing performance degradation and increased wear. However, atime is used by some applications and desired by some users, and thus is configurable as atime (update on access), noatime (do not update), or (in Linux) relatime (update atime if older than mtime). Through Linux 2.6.29, atime was the default; as of 2.6.30 (9 June 2009), relatime is the default.[1] 