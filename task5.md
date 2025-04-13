# 5.命令行环境

### 基本操作
#####   
            1 ^c发送sigint信号中止软件进程。
            2 ^-\发送sigquit结束进程。
            3 kill - <pid>杀死进程。
            4 bg在后台继续运行，fg在前台继续运行。
            5 可以使用nohub把挂起的程序继续运行。
            6 jobs 列出进程
### tmux操作
#####
            1"tmux"打开一个新的窗口，可以通过tmux new -s name指定名称打开窗口，也可以tmux a 连接窗口。
            2 tmux ls 列出所有窗口.
            3 切换窗口（c-b n）跳到第n个窗口，p为切换前一个窗口，n为切换下一个窗口，w列出所以窗口。
            4 c-b “  分割窗口  % 垂直分割 
            5 alias别名更换 例如 alias cd=dc
### 配置文件与远端设备
##### 
            1 可以通过打开工具的文件进行配置
            2 通过ssh name+@服务器name连接服务器。
            3 设置服务器密钥 ssh-key.gen
            4 通过服务器进行复制文件cat localfile | ssh remote_server tee serverfile
### 问题
            1.没有搞懂服务器没法进行实际操作，没有完成课后习题。
            2 tmux没有记牢。
            3 没有搞好框架。
