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

<table>
   <tr>
      <td>Color</td>
      <td>Foreground</td>
      <td>Background</td>
   </tr>
   <tr>
      <td>black</td>
      <td>30</td>
      <td>40</td>
   </tr>
   <tr>
      <td>red</td>
      <td>31</td>
      <td>41</td>
   </tr>
   <tr>
      <td>green</td>
      <td>32</td>
      <td>42</td>
   </tr>
   <tr>
      <td>yellow</td>
      <td>33</td>
      <td>43</td>
   </tr>
   <tr>
      <td>blue</td>
      <td>34</td>
      <td>44</td>
   </tr>
   <tr>
      <td>magenta</td>
      <td>35</td>
      <td>45</td>
   </tr>
   <tr>
      <td>cyan</td>
      <td>36</td>
      <td>46</td>
   </tr>
   <tr>
      <td>white</td>
      <td>37</td>
      <td>47</td>
   </tr>
</table>