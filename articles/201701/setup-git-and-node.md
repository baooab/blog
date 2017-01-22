# 安装 Git 和 Node

> 下面内容节选自阮一峰 [「全栈工程师培训材料」](https://github.com/ruanyf/jstraining)

## 安装 Git

请到官网 [git-scm.com](https://git-scm.com/) 或国内的下载站，下载安装包。

## 安装 Node

请到 Node 官网[nodejs.org](https://nodejs.org)，或者国内镜像[npm.taobao.org/mirrors/node](https://npm.taobao.org/mirrors/node)，下载安装包。推荐安装最新的稳定版，目前是v6.x。

安装完成后，命令行执行下面的命令，确认是否安装成功。

```bash
$ node -v
v6.9.2
```

Node 的模块管理器 npm 会一起安装好。由于 Node 的官方模块仓库网速太慢，模块仓库需要切换到阿里的源。

```bash
$ npm config set registry https://registry.npm.taobao.org/
```

执行下面的命令，确认是否切换成功。

```bash
$ npm config get registry
```

（完）
