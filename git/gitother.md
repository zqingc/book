## GIT 其他命令



有时候我们想忽略某些文件，不过已经commit 一次，这个时候在.gitignore 文件中进行忽略，是不起作用的

需要用如下命令，去掉已经托管的文件，然后重新提交：

```
git rm --cached application/database.php
```

