# 版本控制(git)

## 做题过程及运算结果

### 1.如果您之前从来没有用过 Git，推荐您阅读 Pro Git 的前几章，或者完成像 Learn Git Branching 这样的教程。重点关注 Git 命令和数据模型相关内容；


### 2.克隆 本课程网站的仓库
> 1. 将版本历史可视化并进行探索
> 2. 是谁最后修改了 README.md 文件？（提示：使用 git log 命令并添加合适的参数）
> 3. 最后一次修改 _config.yml 文件中 collections: 行时的提交信息是什么？（提示：使用 git blame 和 git show）


### 3. 使用 Git 时的一个常见错误是提交本不应该由 Git 管理的大文件，或是将含有敏感信息的文件提交给 Git 。尝试向仓库中添加一个文件并添加提交信息，然后将其从历史中删除 ( 这篇文章也许会有帮助)；


### 4. 从 GitHub 上克隆某个仓库，修改一些文件。当您使用 git stash 会发生什么？当您执行 git log --all --oneline 时会显示什么？通过 git stash pop 命令来撤销 git stash 操作，什么时候会用到这一技巧？



### 5. 与其他的命令行工具一样，Git 也提供了一个名为 ~/.gitconfig 配置文件 (或 dotfile)。请在 ~/.gitconfig 中创建一个别名，使您在运行 git graph 时，您可以得到 git log --all --graph --decorate --oneline 的输出结果；


### 6. 您可以通过执行 git config --global core.excludesfile ~/.gitignore_global 在 ~/.gitignore_global 中创建全局忽略规则。配置您的全局 gitignore 文件来自动忽略系统或编辑器的临时文件，例如 .DS_Store；


### 7. Fork 本课程网站的仓库，找找有没有错别字或其他可以改进的地方，在 GitHub 上发起拉取请求（Pull Request）；
