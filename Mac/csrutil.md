# SIP 

Mac电脑的“系统完整性保护”机制（SIP）

## 1.查看SIP状态

在终端中输入csrutil status，就可以看到是enabled还是disabled。

## 2. 关闭SIP

- 1  重启MAC，按住cmd+R直到屏幕上出现苹果的标志和进度条，进入Recovery模式；
- 2  在屏幕最上方的工具栏打开终端，输入：csrutil disable；
- 3  关掉终端，重启mac；
- 4  重启以后可以在终端中查看状态确认。

## 3. 开启SIP

与关闭的步骤类似，只是在终端中输入csrutil enable即可。

