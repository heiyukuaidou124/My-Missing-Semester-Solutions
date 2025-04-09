# 1.Solution-课程概览与 shell
>
> 1.创建了名为tianwu的虚拟机,完成了基本配置。
> 2.询问助教解决了无法联网的问题。

## 做题过程及运算结果

### 1.在 /tmp 下新建一个名为 missing 的文件夹。
![img](./img/image.png)

### 2. 用 man 查看程序 touch 的使用手册
![img](./img/image-1.png)

### 3. 用 touch 在 missing 文件夹中新建一个叫 semester 的文件。
![img](./img/image-2.png)

### 4. 将以下内容一行一行地写入 semester 文件：
> #!/bin/sh
> curl --head --silent https://missing.csail.mit.edu

### 5. 尝试执行这个文件。即，将该脚本的路径（./semester）输入到您的 shell 中并回车
>刚开始没有运行成功，下载了curl后运行成功了，这一步忘记截图了，下面是成功执行后的结果。
![img](./img/image-3.png)

### 6. 查看 chmod 的手册(例如，使用 man chmod 命令)，并使用chmod命令来改变权限使./semester 能够成功执行
![img](./img/image-4.png)

### 7. 使用 | 和 > ，将 semester 文件输出的最后更改日期信息，写入主目录下的 last-modified.txt 的文件中。
![img](./img/image-5.png)

### 8. 写一段命令来从 /sys 中获取笔记本的电量信息，或者台式机 CPU 的温度。
> 由于VMware 虚拟机默认无法直接访问宿主机的电池信息（虚拟机通常模拟无电池的硬件），所以这项任务未能显示。
![img](./img/image-6.png)
