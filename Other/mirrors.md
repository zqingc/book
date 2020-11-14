设置镜像加速器

- 登录阿里云 进入镜像容器服务

- 镜像中心 镜像加速器，开通服务后可以得到加速器地址

- 在 docker desktop  中 进入设置 Docker Engine 项
  右侧json 配置文件中输入 registry-mirrors
  
  ```
  {
    "experimental": false,
    "debug": true,
    "registry-mirrors": [
      "https://wcbuu4n8.mirror.aliyuncs.com"
    ]
  }
  ```

