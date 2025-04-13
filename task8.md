# 元编程

### 笔记
### 构建系统
1. make为最常用的构建系统之一
当执行 make 时，它会去参考当前目录下名为 Makefile 的文件。所有构建目标、相关依赖和规则都需要在该文件中定义
> paper.pdf: paper.tex plot-data.png
	pdflatex paper.tex
plot-%.png: %.dat plot.py
	./plot.py -i $*.dat -o $@

使用不带参数的 make，这便是最终的构建结果。或者，您可以使用这样的命令来构建其他目标：
> make plot-data.png。

2. 规则中的 % 是一种模式，它会匹配其左右两侧相同的字符串
> $ make
make: *** No rule to make target 'paper.tex', needed by 'paper.pdf'.  Stop.

> $ touch paper.tex
$ make
make: *** No rule to make target 'plot-data.png', needed by 'paper.pdf'.  Stop.

构建文件
> 
![img](./1b195da7f52f2a4ccffa711df0777d77.png)

执行make
> $ make
make: 'paper.pdf' is up to date.

修改 paper.tex 后再重新执行 make：
> $ vim paper.tex
$ make
pdflatex paper.tex
...

 make 并没有重新构建 plot.py，；plot-data.png 的所有依赖都没有发生改变

 ### 依赖管理和持续集成系统

1. 一个相对比较常用的标准是 语义版本号，这种版本号具有不同的语义，它的格式是这样的：主版本号.次版本号.补丁号。相关规则有：
> 如果新的版本没有改变 API，请将补丁号递增；
如果您添加了 API 并且该改动是向后兼容的，请将次版本号递增；
如果您修改了 API 但是它并不向后兼容，请将主版本号递增。

2. 持续集成（Continuous integration），或者叫做 CI 是一种雨伞术语（umbrella term，涵盖了一组术语的术语），它指的是那些“当您的代码变动时，自动运行的东西”

#### 测试简介
>测试方法与术语 
测试套件（Test suite）：所有测试的统称。
单元测试（Unit test）：一种“微型测试”，用于对某个封装的特性进行测试。
集成测试（Integration test）：一种“宏观测试”，针对系统的某一大部分进行，测试其不同的特性或组件是否能 协同 工作。
回归测试（Regression test）：一种实现特定模式的测试，用于保证之前引起问题的 bug 不会再次出现。
模拟（Mocking）: 使用一个假的实现来替换函数、模块或类型，屏蔽那些和测试不相关的内容。例如，您可能会“模拟网络连接” 或 “模拟硬盘”。

### 问题
1.未完成对仓库所有文件开启 proselint 或 write-good
2. 本章文本内容较多，有些难懂
3. Rust的构建系统的依赖管理未完全学会

