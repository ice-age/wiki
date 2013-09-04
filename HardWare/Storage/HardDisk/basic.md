##存储设备发展

* 2000年Seagate推出第一款15000RPM硬盘Cheetah X15。

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

##

Average cost time = command overhead + seek time + Rotational latency + Transmission time.

##IOPS、吞吐量测试

测试工具：iozone fio dd

要测试吞吐量主要是测试顺序读写情况下磁盘的读写性能，文件块要大一些，如64k、128k等。测试IOPS则是要测试随机读写小文件的性能，文件要小一些，如4k。

##RAID
