# 调试及性能分析

### 调试代码
            1 cat /var/log/messages（查看所有日志）
            less /var/log/messages（逐页查看）
            tail -n x /var/log/messages(查看x条日志)
            journalctl --since time（按时间查看）
### 调试器与资源监控
            1 可以进行程序一步步进行查看错误python调试器（pdb）
            2 pdb常见的命令 “l”显示当前行11的命令
            “s"执行当前的代码，并在可能错误的地方停止
            “b"设置断点进行检查，“q"退出调试器。
            3 sudo strace -e lstat ls -l > /dev/null 这个工具能显示lstat系统调用的信息并传入到指定文件夹
### 性能分析算法优化与内存
            1 时间会被多个进程而导致不准确 可以使用grep抓取，建立一个程序进行准确的分析，并通过ls -l进行排列。
            2 数组不注意会内存溢出可以用perf list查看可以被追踪的事件，通过perf stat COMMAND ARG1 ARG2收集然后perf record COMMAND ARG1 ARG2进行统计最后perf report - 格式化并打印 perf.data 中的数据。
### 问题
            1 资源监控目前不太懂，不太会用此类工具
            2 很多次这个问题不知道如何安装习题的工具例如（shellcheck，pycallgraph 和 graphviz）没有进行实践。
            3 taskset --cpu-list 0,2 stress -c 3  （3个进程被安排了两个cpu）
            4 排序算法代码有点不太懂（插入更好的原因ai说是不需要大量的辅助空间，代码执行更快）