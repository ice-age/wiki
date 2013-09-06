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