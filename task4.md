# 4.数据整理
> 本章有较多问题较难完成，不是很会做，部分用了ai
## 笔记
### 正则表达式
> /.*Disconnected from /
/.../：通常表示正则表达式的边界（在sed、awk、Perl等工具中）
.*：匹配任意字符（除换行外）0次或多次
Disconnected from ：精确匹配这段文字
组合起来表示："匹配以任意内容开头，后接'Disconnected from '的文本"
1. 常见模式
> . 除换行符之外的 “任意单个字符”
'*' 匹配前面字符零次或多次
'+' 匹配前面字符一次或多次
'+'和'*'在默认情况下为贪婪模式
[abc] 匹配 a, b 和 c 中的任意一个
(RX1|RX2) 任何能够匹配 RX1 或 RX2 的结果
^ 行首
$ 行尾

2.sed正则表达式需要在以上模式前添加\或-E选项

3.可给*或+增加？后缀变为非贪婪模式(sed并不支持此后缀)或切换为perl命令行模式
> perl -pe 's/.*?Disconnected from //'

4. regex debugger(正则表达式在线调试工具)

5.捕获组的内容可以在替换字符串时使用（有些正则表达式的引擎甚至支持替换表达式本身）如 \1、 \2、\3 等等
> | sed -E 's/.*Disconnected from (invalid |authenticating )?user (.*) [^ ]+ port [0-9]+( \[preauth\])?$/\2/'

### 回到数据整理
1. sed((使用 i 命令)，打印特定的行 (使用 p 命令)，基于索引选择特定行)
> ssh myserver journalctl
 | grep sshd
 | grep "Disconnected from"
 | sed -E 's/.*Disconnected from (invalid |authenticating )?user (.*) [^ ]+ port [0-9]+( \[preauth\])?$/\2/'

 2. sort可对其输入数据进行排序,uniq -c 会把连续出现的行折叠为一行并使用出现次数作为前缀
 > ssh myserver journalctl
 | grep sshd
 | grep "Disconnected from"
 | sed -E 's/.*Disconnected from (invalid |authenticating )?user (.*) [^ ]+ port [0-9]+( \[preauth\])?$/\2/'

 sort -n 会按照数字顺序对输入进行排序（默认情况下是按照字典序排序 -k1,1 则表示“仅基于以空格分割的第一列进行排序”。

 3. awk(一种编程语言-另一种编辑器)

 ### 分析数据
 1. R语言-编程语言，适用于数据分析和绘制图表
 2. 利用R语言中的st获取统计数据
 > ssh myserver journalctl
 | grep sshd
 | grep "Disconnected from"
 | sed -E 's/.*Disconnected from (invalid |authenticating )?user (.*) [^ ]+ port [0-9]+( \[preauth\])?$/\2/'
 | sort | uniq -c
 | awk '{print $1}' | R --slave -e 'x <- scan(file="stdin", quiet=TRUE); summary(x)'

### 利用数据整理来确定参数
xargs-利用数据整理技术从一长串列表里找出你所需要安装或移除的东西

### 整理二进制数据
用 ffmpeg 从相机中捕获一张图片，将其转换成灰度图后通过 SSH 将压缩后的文件发送到远端服务器，并在那里解压、存档并显示。
> ffmpeg -loglevel panic -i /dev/video0 -frames 1 -f image2 -
 | convert - -colorspace gray -
 | gzip
 | ssh mymachine 'gzip -d | tee copy.jpg | env DISPLAY=:0 feh -'

 ### 问题
 1. ![img](./img/image.png)
 此处查找数据为手动下载，寻找数据集部分花费了很多时间
 2. 部分课后习题未完成
 3. 正则表达式并未基本学会