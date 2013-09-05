记录shell脚本中用到的命令或者小技巧.

1.tar打包时排除文件

tar -cvf data.tar $(find /home/oracle/data/ ! -name "*.unl")