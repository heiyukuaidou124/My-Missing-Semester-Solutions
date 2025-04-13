# 版本控制(git)
> 想到之前用给虚拟机拍快照的部分，虽然没什么太大的关联

### 笔记

### git的数据类型
#### 快照
##### Git 将顶级目录中的文件和文件夹作为集合，并通过一系列快照来管理其历史记录。在 Git 的术语里，文件被称作 Blob 对象（数据对象），也就是一组数据。目录则被称之为“树”，它将名字与 Blob 对象或树对象进行映射（使得目录中可以包含其他目录）。快照则是被追踪的最顶层的树。
> <root> (tree)
|
+- foo (tree)
|  |
|  + bar.txt (blob, contents = "hello world")
|
+- baz.txt (blob, contents = "git is wonderful")

此树名为foo，包含blob 对象 “bar.txt，以及一个 blob 对象 “baz.txt”

#### 历史记录建模：关联快照
在 Git 中，这些快照被称为“提交”。
> o <-- o <-- o <-- o
            ^
             \
              --- o <-- o
其中的 o 表示一次提交（快照）

Git 中的提交是不可改变的

#### 数据模型及其伪代码表示
伪代码形式
> // 文件就是一组数据
type blob = array<byte>
// 一个包含文件和目录的目录
type tree = map<string, tree | blob>
// 每个提交都包含一个父辈，元数据和顶层树
type commit = struct {
    parents: array<commit>
    author: string
    message: string
    snapshot: tree
}

#### 对象和内存寻址
1. git中的对象可以为 blob、树或提交
> type object = blob | tree | commit

2. Blobs、树和提交都一样，它们都是对象
3. 本身会包含一些指向其他内容的指针，例如 baz.txt (blob) 和 foo (树)。如果我们用 git cat-file -p 4448adbf7ecd394f42ae135bbeed9676e894af85，即通过哈希值查看 baz.txt 的内容，会得到以下信息：
> git is wonderful

#### 引用
Git 可以使用诸如 “master” 这样人类可读的名称来表示历史记录中某个特定的提交，而不需要在使用一长串十六进制字符了
> references = map<string, string>
def update_reference(name, id):
    references[name] = id
def read_reference(name):
    return references[name]
def load_reference(name_or_id):
    if name_or_id in references:
        return load(references[name_or_id])
    else:
        return load(name_or_id)

#### 仓库
git仓库定义:对象和引用
如果希望修改提交树，例如“丢弃未提交的修改和将 ‘master’ 引用指向提交 5d83f9e 时，有什么命令可以完成该操作（针对这个具体问题，可以使用
> git checkout master; git reset --hard 5d83f9e

### 暂存区
指定下次快照中要包括的改动

### Git的命令行接口

#### 基础
> git help <command>: 获取 git 命令的帮助信息
git init: 创建一个新的 git 仓库，其数据会存放在一个名为 .git 的目录下
git status: 显示当前的仓库状态
git add <filename>: 添加文件到暂存区
git commit: 创建一个新的提交
如何编写 良好的提交信息!
为何要 编写良好的提交信息
git log: 显示历史日志
git log --all --graph --decorate: 可视化历史记录（有向无环图）
git diff <filename>: 显示与暂存区文件的差异
git diff <revision> <filename>: 显示某个文件两个版本之间的差异
git checkout <revision>: 更新 HEAD 和目前的分支

#### 分支和合并
> git branch: 显示分支
git branch <name>: 创建分支
git checkout -b <name>: 创建分支并切换到该分支
相当于 git branch <name>; git checkout <name>
git merge <revision>: 合并到当前分支
git mergetool: 使用工具来处理合并冲突
git rebase: 将一系列补丁变基（rebase）为新的基线

#### 远端操作
> git remote: 列出远端
git remote add <name> <url>: 添加一个远端
git push <remote> <local branch>:<remote branch>: 将对象传送至远端并更新远端引用
git branch --set-upstream-to=<remote>/<remote branch>: 创建本地和远端分支的关联关系
git fetch: 从远端获取对象/索引
git pull: 相当于 git fetch; git merge
git clone: 从远端下载仓库
撤销

#### 撤销
> git commit --amend: 编辑提交的内容或信息
git reset HEAD <file>: 恢复暂存的文件
git checkout -- <file>: 丢弃修改
git restore: git2.32 版本后取代 git reset 进行许多撤销操作

### GIt高级操作
> git config: Git 是一个 高度可定制的 工具
git clone --depth=1: 浅克隆（shallow clone），不包括完整的版本历史信息
git add -p: 交互式暂存
git rebase -i: 交互式变基
git blame: 查看最后修改某行的人
git stash: 暂时移除工作目录下的修改内容
git bisect: 通过二分查找搜索历史记录
.gitignore: 指定 故意不追踪的文件

### 杂项
> 图形用户界面: Git 的 图形用户界面客户端 有很多，但是我们自己并不使用这些图形用户界面的客户端，我们选择使用命令行接口
Shell 集成: 将 Git 状态集成到您的 shell 中会非常方便。(zsh, bash)。Oh My Zsh 这样的框架中一般已经集成了这一功能
编辑器集成: 和上面一条类似，将 Git 集成到编辑器中好处多多。fugitive.vim 是 Vim 中集成 Git 的常用插件
工作流: 我们已经讲解了数据模型与一些基础命令，但还没讨论到进行大型项目时的一些惯例 ( 有 很多 不同的 处理方法)
GitHub: Git 并不等同于 GitHub。 在 GitHub 中您需要使用一个被称作 拉取请求（pull request） 的方法来向其他项目贡献代码
其他 Git 提供商: GitHub 并不是唯一的。还有像 GitLab 和 BitBucket 这样的平台。

### 问题
1. 克隆仓库部分并不太熟练
2. 本章知识点过多比较难记