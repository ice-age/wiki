##存储设备发展

* 2000年Seagate推出第一款15000RPM硬盘Cheetah X15。

sata硬盘，串行可以热插拔，成本低，在桌面级系统，对性能要求不是很高的可以使用
scsi 速度略高于sata，对性能稳定性要求高的服务器

##硬盘参数

* 转速
* 直径
* 盘片数
* 磁头数
* 缓存
* Bandwidth  
* 功耗

##衡量硬盘性能的几个方面

* IOPS (Input/Output Per Second):每秒读写次数.随机读写、IO密集型应用更看重IOPS，如搜索、在线游戏等。
* Throughput：吞吐量，单位时间内最大的I/O流量，xxMbps。在大量顺序读写的情境下，更看重吞吐量，如视频。区别于Bandwidth 。
* Latency:
* 平均无故障时间：

#接口

* sata1  1.5Gb/s
* sata2  3Gb/s
* sata3  6Gb/s
* sas2   6Gb/s

##寻道、延时

Average cost time = command overhead + seek time + Rotational latency + Transmission time.

Rotational latency = 60/RPM/2*1000

一般情况下寻道时间：

* 7.2k平均寻道时间=8.5/9.5ms
* 10k平均寻道时间=3.6/4.2ms
* 15k平均寻道时间=3.4/3.9ms

IOPS = 1000 ms/ (Tseek + Troatation)

##IOPS、吞吐量测试

测试工具：iozone Iometer fio dd

要测试吞吐量主要是测试顺序读写情况下磁盘的读写性能，文件块要大一些，如64k、128k等。测试IOPS则是要测试随机读写小文件的性能，文件要小一些，如4k。

### 1.fio 

fio -name=test -rw=randrw -bs=4k -size=100M -iodepth=1 -ioengine libaio -directory=/data/8 -fsync=1

### 2.dd

dd bs=1M count=128 if=/dev/zero of=test oflag=dsync

dd bs=1M count=128 if=/dev/zero of=test conv=sync 

bs=同时读写的字节数。ibs、obs

if=读取的文件

of=输出的文件

conv有：
* sync   pad every input block with NULs to ibs-size; when used with block or unblock, pad with spaces rather than NULs
* fdatasync physically write output file data before finishing。结束时写入到磁盘
* fsync  likewise, but also write metadata



oflag/iflag有：
* dsync  use synchronized I/O for data。同步写入到磁盘
* sync   likewise, but also for metadata


* /dev/zero:当你读它的时候，它会提供无限的空字符(NULL, ASCII NUL, 0x00)。
* /dev/null:空设备，是一个特殊的设备文件，它丢弃一切写入其中的数据
* /dev/random
* /dev/mem

http://romanrm.ru/en/dd-benchmark

##RAID


##相关工具

### 1.fdisk

### 2.mkfs

mkfs -t ext4 -m 1 -O dir_index,extent,sparse_super /dev/sdk1


### 3.tune2fs

tune2fs -l /dev/sdk1

### 4.smartmontools

smartmontools包含smartctl和smartd，它通过使用自我监测、分析及报告技术控制、监控存储系统。可以使用来多数现代硬盘包括(P)ATA, Serial ATA and SCSI等。可以在硬盘完全故障之前，做出预警。

现在的硬盘基本上都支持SMART技术，通过命令可以检测是否支持。

smartctl -i /dev/sdd

启用SMART

smartctl --smart=on --offlineauto=on --saveauto=on /dev/sdd


-a 显示所有信息
-i
-A
-H 

手工对硬盘进行测试的方法有以下四种：
smartctl -t short     后台检测硬盘，消耗时间短
smartctl -t long       后台检测硬盘，消耗时间长
smartctl -C -t short  前台检测硬盘，消耗时间短
smartctl -C -t long   前台检测硬盘，消耗时间长
smartctl -l selftest /dev/sdd 结果