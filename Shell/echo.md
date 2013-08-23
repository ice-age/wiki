在很多操作系统中都有echo命令，如Unix、类Unix、Ms windows。可以讲字符串输出到中断。

下面只说linux中的echo。

## 输出带有颜色、背景色的字符串
### Q1 怎样输出带颜色的字符串
echo -e "\033[1;31;43m你好"

### Q2 颜色代码有哪些
* 0-9 控制字体的效果
* 31-39 控制字体颜色
* 41-49 控制背景颜色

0 关闭所有属性
1 设置高亮度
4 下划线
5 闪烁
7 反显
8 消隐

rminal emulators.


Color	Foreground	Background
black	30	40
red	31	41
green	32	42
yellow	33	43
blue	34	44
magenta	35	45
cyan	36	46
white	37	47