# 在 Windows 10 系统中安装 WNMP 环境

WNMP 又称 WEMP，即 Windows 系统下的 Nginx、MariaDB 和 PHP 环境搭建。

这份教程的最后，我们将 WNMP 环境统一搭建在了 `D:\wnmp` 目录下，这份目录的清单是这样的。

```
wnmp/
├── php/
│   └── 7.1.6/
|		├── php.ini
|		├── php-cgi.exe
|		└── php.exe
├── nginx/
│   └── 1.13.1/
|   	└── conf/
|			└── nginx.conf
└── www/
    └── index.html
```

## 原料

1. PHP

下载地址：[php.net][1]。

[1]: http://windows.php.net/download

要注意的是，Nginx 需使用 PHP 的 FastCGI Server 模块，下载的 PHP 版本是“Non Thread Safe”的。

比如：我下载的 PHP 版本文件名为 `php-7.1.6-nts-Win32-VC14-x64.zip`。

2. Nginx

下载地址：[nginx.org][2]。

[2]: http://nginx.org/en/download.html

我下载的 Nginx 版本文件名为 `nginx-1.13.1.zip`。

3. RunHiddenConsole

这是一个 exe 文件，是为了保证之后编写的启动 Nginx 服务器的 `start_nginx.bat` 脚本和关闭 Nginx 服务器的 `stop_nginx.bat` 脚本执行后立即关闭，隐藏于后台。

下载地址：[lighttpd.net][3]。

[3]: http://redmine.lighttpd.net/attachments/660/RunHiddenConsole.zip

文件名即为 `RunHiddenConsole.zip`。

4. MariaDB

下载地址：[mariadb.org][4]。

[4]: https://downloads.mariadb.org/

我下载的 MariaDB 版本文件名为 `mariadb-10.2.6-winx64.msi`。

## 安装 PHP

因为 PHP 版本是 7.1.6，将 `php-7.1.6-nts-Win32-VC14-x64.zip` 里的内容解压到 `D:\wnmp\php\7.1.6` 目录下。

### 修改配置

将 `php.ini-development` 重命名为 `php.ini`。进入修改三处。 

1. 指定 PHP 扩展目录

PHP 扩展就放在 ext 文件夹下。指定扩展目录时，使用绝对路径。

```
; 去掉注释，指定扩展目录

; On windows:
extension_dir = "C:/wnmp/php7.1.5/ext"
```

2. 启用扩展

默认许多扩展并没有开启，比如 mysqli、 openSSL。所以需要手动去掉注释，启用一些扩展。

为了方便日后使用，把下面的扩展去掉注释。

```
; 像下面这样去掉注释，指定启用的扩展目录

; Windows Extensions
; Note that ODBC support is built in, so no dll is needed for it.
; Note that many DLL files are located in the extensions/ (PHP 4) ext/ (PHP 5+)
; extension folders as well as the separate PECL DLL download (PHP 5+).
; Be sure to appropriately set the extension_dir directive.
;
extension=php_bz2.dll
extension=php_curl.dll
extension=php_fileinfo.dll
;extension=php_ftp.dll
extension=php_gd2.dll
extension=php_gettext.dll
extension=php_gmp.dll
extension=php_intl.dll
extension=php_imap.dll
;extension=php_interbase.dll
extension=php_ldap.dll
extension=php_mbstring.dll
extension=php_exif.dll      ; Must be after mbstring as it depends on it
extension=php_mysqli.dll
;extension=php_oci8_12c.dll  ; Use with Oracle Database 12c Instant Client
extension=php_openssl.dll
;extension=php_pdo_firebird.dll
extension=php_pdo_mysql.dll
;extension=php_pdo_oci.dll
;extension=php_pdo_odbc.dll
;extension=php_pdo_pgsql.dll
extension=php_pdo_sqlite.dll
;extension=php_pgsql.dll
;extension=php_shmop.dll

; The MIBS data available in the PHP distribution must be installed.
; See http://www.php.net/manual/en/snmp.installation.php
;extension=php_snmp.dll

extension=php_soap.dll
extension=php_sockets.dll
extension=php_sqlite3.dll
;extension=php_tidy.dll
extension=php_xmlrpc.dll
extension=php_xsl.dll
```

3. 设置 cgi.fix_pathinfo。

```
; 去掉注释，将 cgi.fix_pathinfo 设置为 1

cgi.fix_pathinfo=1
```

### 设置全局变量

将路径 `D:\wnmp\php\7.1.6` 设置到系统全局环境变量 `PATH` 里。

进入命令界面，输入如下命令，如果正确输出版本号，说明设置成功。

```
$ php -v
PHP 7.1.6 (cli) (built: Jun  8 2017 01:52:52) ( NTS MSVC14 (Visual C++ 2015) x64
 )
Copyright (c) 1997-2017 The PHP Group
Zend Engine v3.1.0, Copyright (c) 1998-2017 Zend Technologies
```

## 安装 Nginx

解压 `nginx-1.13.1.zip` 文件中内容到 `D:\wnmp\nginx\1.13.1` 目录下。

## 修改配置

进入 `conf` 目录，编辑配置文件 `nginx.conf`。修改 80 端口的 Server 配置信息，具体如下。

```
location / {
    root   html;
    index  index.html index.htm;
}

# 改为

location / {
    root   D:/wnmp/www;
    index  index.php index.html index.htm;
}
```

```
# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
#
#location ~ \.php$ {
#    root           html;
#    fastcgi_pass   127.0.0.1:9000;
#    fastcgi_index  index.php;
#    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
#    include        fastcgi_params;
#}

# 改为

# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
#
location ~ \.php$ {
    root           D:/wnmp/www;
    fastcgi_pass   127.0.0.1:9000;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
    include        fastcgi_params;
}
```

要注意两点：

1. 我们将网站根目录设置到了 `D:/wnmp/www` 目录中，所以**务必要创建 `D:/wnmp/www` 目录**！

2. 最后一部分配置内容是将 `.php` 后缀的文件都交给 PHP 开在 9000 端口的 FastCGI Server 处理。

## 开启 Nginx 服务器

第一步，解压 `RunHiddenConsole.zip` 文件得到 `RunHiddenConsole.exe`，将它放在与 `php.exe` 同级的目录，就是本教程的 `D:\wnmp\php\7.1.6` 目录。

我们已经说过，`RunHiddenConsole.exe` 的作用为了保证启动 Nginx 服务器的 `start_nginx.bat` 脚本和关闭 Nginx 服务器的 `stop_nginx.bat` 脚本执行后立即关闭，隐藏于后台的。

接下来，我们来编写启动和关闭 Nginx 服务器的脚本，它们放在与 `nginx.exe` 同级的目录中，就是本教程的 `D:\wnmp\nginx\1.13.1` 目录。

### 启动 Nginx 的脚本

启动 Nginx 的脚本名为 `start_nginx.bat`。内容如下：

```
@echo off

REM 每个进程处理的最大请求数，或设置为 Windows 环境变量
set PHP_FCGI_MAX_REQUESTS=1000

echo Starting PHP FastCGI...
RunHiddenConsole php-cgi -b 127.0.0.1:9000 -c D:/wnmp/php/7.1.6/php.ini

echo Starting nginx...
RunHiddenConsole ./nginx.exe -p D:/wnmp/nginx/1.13.1
```

### 关闭 Nginx 的脚本

关闭 Nginx 的脚本名为 `stop_nginx.bat`。内容如下：

```
@echo off
echo Stopping nginx...  
taskkill /F /IM nginx.exe > nul
echo Stopping PHP FastCGI...
taskkill /F /IM php-cgi.exe > nul
exit
```

### 浏览器访问

在 `D:/wnmp/www` 中创建文件 `index.php`。

```
<?php
	phpinfo();
>
```

点击 `start_nginx.bat` 文件，浏览器输入 http://localhost/ ，如果出现如下界面，表示服务器安装成功！

![phpinfo][5]

[5]: images/Installing-WNMP/phpinfo.png

## MariaDB 

MariaDB 数据库安装过程非常简单，这里不再赘述了。:-D
