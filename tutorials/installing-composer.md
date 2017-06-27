# 在 Windows 10 系统中安装 Composer

## 简介

Composer 是 PHP 的一个依赖包管理工具，它允许你在 `composer.json` 文件中声明项目所依赖的包，在你使用 `composer install` 后为你的项目安装它们。

## 安装 Composer

在安装 Composer 前请务必确保已经正确安装了 PHP――打开命令行窗口并执行 `php -v` 查看是否正确输出版本号。

### 下载 Composer

从 [getcomposer.org][1] 下载 `composer.phar`（我下载的是 1.4.2 版本的）。并将该文件放置在与 `php.exe` 同级的目录下（我的地址为 `D:\wnmp\php\7.1.6`）。键入 `php composer.phar -V`，如果正确输出 composer 版本号，说明安装成功。

```
$ php composer.phar -V
Composer version 1.4.2 2017-05-17 08:17:52
```

### 全局配置

像上面那样这样操作，还是很麻烦，能全局直接使用 `composer` 命令是再好不过的了。接下来就实现。

新建 `composer.bat` 文件，放置于与 `php.exe` 同级的目录下。内容如下：

```
@php "%~dp0composer.phar" %*
```

接下来打开命令行界面，输入 `composer` 指令。如果正确输出 composer 版本号，说明 Composer 全局配置成功！

```
C:\Users\zhangb>composer -V
Composer version 1.4.2 2017-05-17 08:17:52
```

[1]: https://getcomposer.org/download/