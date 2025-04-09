# 调试及性能分析

## 做题过程及运算结果

### 调试
1. 使用 Linux 上的 journalctl 或 macOS 上的 log show 命令来获取最近一天中超级用户的登录信息及其所执行的指令。如果找不到相关信息，您可以执行一些无害的命令，例如 sudo ls 然后再次查看。


2. 学习 这份 pdb 实践教程并熟悉相关的命令。更深入的信息您可以参考 这份 教程。




3. 安装 shellcheck 并尝试对下面的脚本进行检查。这段代码有什么问题吗？请修复相关问题。在您的编辑器中安装一个 linter 插件，这样它就可以自动地显示相关警告信息。
> #!/bin/sh
> ##Example: a typical script with several problems
>for f in $(ls *.m3u)
do
  grep -qi hq.*mp3 $f \
    && echo -e 'Playlist $f contains a HQ file in mp3 format'
done




4. (进阶题) 请阅读 可逆调试 并尝试创建一个可以工作的例子（使用 rr 或 RevPDB）。



### 性能分析
1. 这里 有一些排序算法的实现。请使用 cProfile 和 line_profiler 来比较插入排序和快速排序的性能。两种算法的瓶颈分别在哪里？然后使用 memory_profiler 来检查内存消耗，为什么插入排序更好一些？然后再看看原地排序版本的快排。附加题：使用 perf 来查看不同算法的循环次数及缓存命中及丢失情况。



2. 这里有一些用于计算斐波那契数列 Python 代码，它为计算每个数字都定义了一个函数：
> #!/usr/bin/env python
def fib0(): return 0
def fib1(): return 1
s = """def fib{}(): return fib{}() + fib{}()"""
if __name__ == '__main__':
    for n in range(2, 10):
        exec(s.format(n, n-1, n-2))
    # from functools import lru_cache
    # for n in range(10):
    #     exec("fib{} = lru_cache(1)(fib{})".format(n, n))
    print(eval("fib9()"))
将代码拷贝到文件中使其变为一个可执行的程序。首先安装 pycallgraph 和 graphviz(如果您能够执行 dot, 则说明已经安装了 GraphViz.)。并使用 pycallgraph graphviz -- ./fib.py 来执行代码并查看 pycallgraph.png 这个文件。fib0 被调用了多少次？我们可以通过记忆法来对其进行优化。将注释掉的部分放开，然后重新生成图片。这回每个 fibN 函数被调用了多少次？




3. 我们经常会遇到的情况是某个我们希望去监听的端口已经被其他进程占用了。让我们通过进程的 PID 查找相应的进程。首先执行 python -m http.server 4444 启动一个最简单的 web 服务器来监听 4444 端口。在另外一个终端中，执行 lsof | grep LISTEN 打印出所有监听端口的进程及相应的端口。找到对应的 PID 然后使用 kill <PID> 停止该进程。




4. 限制进程资源也是一个非常有用的技术。执行 stress -c 3 并使用 htop 对 CPU 消耗进行可视化。现在，执行 taskset --cpu-list 0,2 stress -c 3 并可视化。stress 占用了 3 个 CPU 吗？为什么没有？阅读 man taskset 来寻找答案。附加题：使用 cgroups 来实现相同的操作，限制 stress -m 的内存使用。



5. (进阶题) curl ipinfo.io 命令或执行 HTTP 请求并获取关于您 IP 的信息。打开 Wireshark 并抓取 curl 发起的请求和收到的回复报文。（提示：可以使用 http 进行过滤，只显示 HTTP 报文）