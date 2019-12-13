---
description: Git使用规范
---

# Git使用规范 {#article-title}

##一. Windows上安装Git {#8geppk}

访问官网[https://git-scm.com/download/win](https://git-scm.com/download/win)下载对应版本的安装包。  
安装完成后，从`开始菜单`---&gt;`Git`---&gt;`Git Bash`，打开命令行工具。  
为了确认是否安装成功，我们执行`version`命令，如果正常显示Git的版本号就表示Git已经成功安装了。

```
git --version
```

_输出：git version 2.9.0.windows.1_

## 二. Git 全局设置 {#zkzioo}

### 1.初始配置 {#vimopy}

在使用Git之前，我们对Git做一个初始配置，我们需要设置用户名和电子邮箱。以便之后我们提交了代码后，Git能跟踪和标记是谁做了修改。  
在命令行工具中，依次执行如下命令进行设置：

```
git config --global user.name "<使用者名字>"

git config --global user.email "<电子邮箱>"
```

_注意：替换掉命令中的_`<使用者名字>`_和_`<电子邮箱>`_，注意保留命令中的双引号。强烈推荐您使用与远程代码库中相同的用户名和电子邮箱_  
配置完成后，我们也可以执行以下命令进行查看：

```
git config --global user.name

git config --global user.email
```

### 2.Windows控制台无法显示中文 {#ydvuxt}

Windows上的控制台遇到中文名称的时候会显示为类似"\346\226\260\350\246..."这样的字符，执行以下命令让它显示出正确的中文：

```
git config --global core.quotepath off
```

### 3.Windows上拉取的文件编程修改状态 {#29gart}

**问题：**

在Windows系统上，可能会遇到，从git上拉取服务端代码后，发现新拉取的文件都编程修改状态。这是git自动转换换行符导致的问题。

**原因：**

不同操作系统使用的换行符是不一样的。Unix/Linux使用的是LF，Mac后期也采用了LF，但Windows一直使用CRLF【回车\(CR, ASCII 13, \r\) 换行\(LF, ASCII 10, \n\)】作为换行符。而git入库的代码采用的是LF格式，它考虑到了跨平台协作的场景，提供了“换行符自动转换”的功能：如果在Windows下安装git，在拉取文件时，会自动将LF换行符替换为CRLF；在提交时，又会将CRLF转回LF。但是这个转换是有问题的：有时提交时，CRLF转回LF可能会不工作，尤其是文件中出现中文字符后有换行符时。

**解决方法：**

需要禁用git的自动换行功能：

```
git config --global core.autocrlf false
git config --global core.filemode false
git config --global core.safecrlf true
```

## 三. 配置 SSH 公钥 {#4ktrgm}

推荐使用 SSH 协议来访问 Git 仓库。

### 1. 生成公钥 {#9i5get}

打开命令行终端输入

```
ssh-keygen -t rsa -b 4096 -C <your_email@example.com>
```

输出如下信息，并提示，连续点击 Enter 键即可。

```
# Creates a new ssh key, using the provided email as a label
# Generating public/private rsa key pair.

Enter file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]  // 推荐使用默认地址
Enter passphrase (empty for no passphrase):   //此处点击 Enter 键即可，也可以填写密码，填写密码后每次使用 SSH 方式推送代码时都会要求输入密码，由于这个 Key 也不是用于军事目的，所以也无需设置密码。
```

成功之后显示如下信息：

```
Your identification has been saved in /Users/you/.ssh/id_rsa.
# Your public key has been saved in /Users/you/.ssh/id_rsa.pub.
# The key fingerprint is:
# 01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@example.com
```

公钥文件`id_rsa.pub`创建成功后，默认是存储在用户目录`.ssh`中  
_Window系统用户目录：_`C:\Users\Administrator\.ssh\id_rsa.pub`

## 四. 分支管理 {#o1m7ef}

代码库中存在两个固定分支：

* master 主分支，只用于发布系统的正式版本；

* develop （默认）开发分支，日常的开发工作都只能在该分支上进行。

这两个分支都属于保护分支，禁止直接推送代码。

### 1. 克隆代码到本地 {#cwxanc}

通过命令克隆代码到本地目录

```
git clone git@git.coding.net:xxx
```

### 2. 拉取最新代码 {#agqnkx}

克隆下来的代码，默认为`develop`分支，首先保证该分支下的代码是最新的。  
使用如下命令从远程库中拉取最新代码到本地：

```
git pull

// 获取远端分支
git pull origin <branch>   

// 从远端拉去本地没有的分支并新建本地分支
git checkout -b newbranch origin/newbranch   
```

### 2. 创建功能分支 {#9blbek}

由于不能直接在`develop`分支上修改代码，  
需要从`develop`分支上创建一个功能分支，命名为`feature-xxx`

```
git checkout -b feature-xxx develop
```

现在可以在 feature-xxx 功能分支上进行开发。

### 3. 将修改的文件添加到缓存区 {#gob4mg}

当我们新增或编辑了代码，我们需要将文件添加到缓存区。  
在命令行中执行以下命令:

```
git add .
```

最后的“.”符号的意思是仓库下的“所有文件、文件夹和子文件夹”。  
假如我们只想要把特定文件添加到源代码控制中去，我们可以显示的指定它们，使用命令`git add <filename>`：

```
git add my_file, my_other_file
```

### 4. 提交文件改动 {#tyciso}

使用如下命令，将改动提交到本地`HEAD`区，此时还并没有同步到远程代码库：

```
git commit -m "代码提交信息"
```

_输入提交信息时，如果需要输入中文，则使用_`-m`_参数_  
_注意：提交我们的文件时，总是附带着有意义的注释，描述了它们现在的状态。_

现在我们随时都可以回滚到这个提交状态。如果你有需要检查你现在的已加载（staged）和未加载（unstaged）文件的状态、提交等，你可以询问git的状态：

```
git status
```

### 5. 推送到远程代码库 {#x56bez}

执行如下命令以将这些改动提交到远端仓库：

```
git push origin feature-xxx
```

推送完成后在远程库中创建对应的合并请求，管理员会将新提交的代码合并到`develop`分支中。

### 6. 删除本地的`feature`分支 {#y2b5ms}

首先得切换回`develop`分支下：

```
git checkout master
```

查看当前存在哪几个分支

```
git branch
```

强制删除分支

```
git branch -D feature-xxx
```

## 五. 合并分支 {#gg8gdu}

如果要将其他分支的修改合并到 master 分支。

先切换到 master 分支下

```
git checkout master
```

拉取 master 最新代码

```
git pull
```

进行合并 注意这里使用`--squash`参数，用来把一些不必要commit进行压缩

```git
git merge --squash feature-xxx
```

提交合并后的代码

```
git commit -m "修改xxx"
```

最后推送到远程代码库

```
git push
```

Git 暂存代码

```
git stash 
```

取出暂存

```Git
git stash pop
```

1.添加tag 标签

``` 
git tag <name>  // 打标签
```

加上-a参数来创建一个带备注的tag，备注信息由-m指定。如果你未传入-m则创建过程系统会自动为你打开编辑器让你填写备注信息

```
git tag -a tagName -m "my tag"
```

2.列出已有的tag

```
git tag
```

3.给指定的某个commit号加tag

```javascript
git tag -a v1.2 9fceb02 -m "my tag"
```

4.将tag同步到远程服务器

```javascript
git push origin v1.0
```

5.推送所有：

```javascript
git push origin --tags
```
