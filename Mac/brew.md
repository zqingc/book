## brew

brew 是 Mac 下的一个包管理工具，作用类似于 `centos` 下的 `yum`。

brew 可以用一条命令，就可以在mac上安装、卸载、更新各种软件包，因为brew的使用方便，如今已成为使用mac电脑的程序员的必备工具

### 安装brew

安装brew也很简单，一条命令即可:

```powershell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### brew基本用法

brew作为使用mac电脑的程序员的必备工具，基本用法也很简单，小白同学只需要记住安装、更新、卸载三条就行：

### 安装软件

brew的安装目录在 `/usr/local/Cellar`，我们以安装`nodejs`为例子，只需要执行：

```text
brew install nodejs
```

就安装完了，就这么简单

### 更新软件

```text
brew upgrade nodejs
```

### 卸载软件

```text
brew remove nodejs
```

全是一条命令。

在介绍几条其他命令：

```text
shell script brew list      # 列出当前安装的软件 
brew search nodejs          # 查询与 nodejs 相关的可用软件 
brew info nodejs            # 查询 nodejs 的安装信息
```

如果需要安装指定版本的软件，执行 `brew search` 查看有没有需要的版本 在 @ 后面指定版本号，例如 brew install thrift@0.9

### brew services

brew services 是一个非常强大的工具，可以管理软件，进行停止、重启等

```text
brew install elasticsearch          # 安装 elasticsearch
brew services start elasticsearch   # 启动 elasticsearch
brew services stop elasticsearch    # 停止 elasticsearch
brew services restart elasticsearch # 重启 elasticsearch
brew services list                  # 列出当前的状态
```

开始你的brew之旅吧！