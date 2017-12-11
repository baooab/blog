## 用 Chrome 冲浪

在中国是使用不了 Google 搜索的，所以就有了对策。

### #1. 搭建个人 SS 服务

我使用 Arukas.io ，因为免费。在 [这里](https://app.arukas.io/) 注册。

注册成功后。点击「Create a new application」，填写的内容参考 [这里](http://www.iqcni.com/other/12.html) 。

在 application 「Running」之后，在详情页看到 「Port」和「CMD」。类似

```
Port http://seaof-153-120-229-220.jp-tokyo-20.arukascloud.io:32157 (8888/tcp)
CMD  ssserver -p 8888 -k 123456 -m aes-256-cfb
```

这是代理服务器信息：

```
IP：153.120.229.220
端口：32157
密码：123456
```

## #2. 下载扩展程序 SwitchyOmega

地址：https://github.com/FelisCatus/SwitchyOmega/releases

导入浏览器，点击应用 > 「选项」 > 「导入/导出」 > 「在线恢复」 > 贴入地址 「https://github.com/FelisCatus/SwitchyOmega/wiki/GFWList.bak」

（也可以参考 [这里](https://github.com/FelisCatus/SwitchyOmega/wiki/GFWList) 的教程）

## #3. 使用 ShadowsocksR

在 [这里](https://github.com/shadowsocksr/shadowsocksr-csharp/releases) 下载。

打开，将 「#1」 部分新建的代理服务器的信息填入。

下面是软件和代理服务器对照字段：

```
服务器 IP  <=> IP
服务器端口 <=> 端口
密码       <=> 密码
```

## #4. Surfing！

（完）

