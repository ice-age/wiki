lvm

lvm增强了存储的可扩展性,但是可靠性和安全性降低了.lvm适用于虚拟化或者云存储.

（1）LVM优点：

    文件系统可以跨多个磁盘，因此大小不会受物理磁盘的限制。
    可以在系统运行状态下动态地扩展文件系统大小。
    可以增加新磁盘到 LVM 的存储池中。
    可以以镜像的方式冗余重要数据到多个物理磁盘上。
    可以很方便地导出整个卷组，并导入到另外一台机器上。

（2）LVM缺点

    在从卷组中移除一个磁盘时必须使用 reducevg，否则会出问题。
    当卷组中的一个磁盘损坏时，整个卷组都会受影响。
    仅支持有限个文件系统类型的减小操作（ext3不支持减少文件系统大小的操作）。
    因为加入了额外的操作，存储性能会受影响（使用 Stripe 的情况另当别论）