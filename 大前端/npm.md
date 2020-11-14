### npm 和 cnpm 的区别



NPM（Node Package Manager，节点包管理器）是NodeJS的包管理器，用于节点插件的管理（包括安装，卸载和管理依赖等）。NPM是随同新版的NodeJS一起安装的包管理工具，所以我们需要安装NodeJS。



1.基本上每个js项目根目录下都有一个package.json文件，定义了该项目所需要的各种模块依赖，以及项目的配置信息(比如名称/版本/许可证等元数据). npm install 会根据这个配置文件自动下载所需木块即配置项目所需的运行和开发环境
2.package.json 可以手动编写，也可以使用npm init命令自动生成, 两者并没有什么区别



cnpm 是淘宝团队提供的一个npm国内替代工具，但是一定有点需要注意就是不要cnpm 跟 npm不要混用，虽然官网上说两者表现一致，但内部实现还是有点区别的，最好的方式应该是使用npm但是切换成淘宝镜像

执行以下命令就可以使用cnpm了

```
npm set registry https://registry.npm.taobao.org
```



安装完成后可以使用cnpm -v命令查看版本号，要使用cnmp命令的话最好在安装后重新打开CMD命令行控制台。

cnpm的用法和npm的用法一致，只是在执行命令的时候将npm改为cnpm。



（1） 两者之间只是 node 中包管理器的不同

（2） npm是node官方的包管理器。cnpm是个中国版的npm，是淘宝定制的 [cnpm](https://github.com/cnpm/cnpm) (gzip 压缩支持) 命令行工具代替默认的 `npm`:

（3）如果因为网络原因无法使用npm下载，那cnpm这个就派上用场了。





npm i element-ui -S  报错



![image-20200703215219592](/Users/zhangchao/Library/Application Support/typora-user-images/image-20200703215219592.png)



以上错误显示某个地方重复调用，不过用cnpm 确实就成功了（手动狗头）

使用  cnpm i element-ui -S  安装成功

 

