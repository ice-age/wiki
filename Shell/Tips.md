记录shell脚本中用到的命令或者小技巧.

####1.tar打包时排除文件

tar -cvf data.tar $(find /home/oracle/data/ ! -name "*.unl")

####2.dirname 与 basename

* dirname 获取文件的目录,如果只给文件名,则返回"."
* basename 获取文件名字,不包含路径

${pathname%/*}也可以获取文件的路径
pathname=/usr/bin/free;echo ${pathname%/*}

进入到脚本所在的目录
cd $(dirname "$0") || exit 1
####3.$x

    $# 是传给脚本的参数个数
    $0 是脚本本身的名字
    $1 是传递给该shell脚本的第一个参数
    $2 是传递给该shell脚本的第二个参数
    $@ 是传给脚本的所有参数的列表
    $* 是以一个单字符串显示所有向脚本传递的参数，与位置变量不同，参数可超过9个
    $$ 是脚本运行的当前进程ID号
    $? 是显示最后命令的退出状态，0表示没有错误，其他表示有错误
    $! Shell最后运行的后台Process的PID
    $- 使用Set命令设定的Flag一览





###3.调用syslog

logger 

###4.用awk命令抽取输出第三列第5个字符

    awk '{print substr($3,5,1)}'  filename
    awk 'NR==2{print $3|"cut -b4"}' filename

###5.小数除法,13/2保留两位小数

正确答案:

    average=`echo "scale=2;13/2"|bc`;echo $average
    6.50

错误答案:

    average=`expr 13 / 2`;echo $average
    6