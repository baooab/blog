> 以下是我在使用 Laravel 过程中，所有知识点的整理。

在继续看下去之前，先看这篇文章：[使用 Laravel 前的准备工作](https://baooab.wordpress.com/2016/12/31/%e4%bd%bf%e7%94%a8-laravel-%e5%89%8d%e7%9a%84%e5%87%86%e5%a4%87%e5%b7%a5%e4%bd%9c/)。
## 目录

- [Composer 部分](#Composer)
- [`php artisan` 命令](#PHPArtisanCommand)
- [`laravel` 命令](#LaravelCommand)
- [`Laravel` 文档拾遗](#LaravalDocStudy)
- [琐碎](#foo)

<a name="Composer">
## Composer 部分

- 安装依赖

```
composer install
```

- 更新依赖

```
composer update
```

- Composer 中文文档

http://docs.phpcomposer.com/

重点看命令行部分

http://docs.phpcomposer.com/03-cli.html

- 手动删除迁移文件问题

执行

```
composer dump-autoload
```
命令可复位composer自动加载文件，解决手动删除迁移文件问题。

<a name="PHPArtisanCommand">
## `php artisan` 命令

- 查看所有可以使用的 Laravel 命令即当前项目使用的 Laravel 版本：

```
php artisan list
```

得（经常使用、中药的部分翻译成中文）

```

Laravel Framework version 5.2.22 当前项目使用的 Larvel 版本是 5.2.22

Usage:
  command [options] [arguments]

Options（对应“Usage”的第二个可选值）:
  -h, --help            显示当前命令的帮助信息。例如显示 `make:model` 的帮助信息，用 `php artisan make:model -h`，等同于 `php artisan help make:model` 命令
  -q, --quiet           Do not output any message
  -V, --version         显示当前项目使用的 Laravel 版本。无论 command 有无或者为何，都是输出 Laravel 版本，比如“Laravel Framework version 5.2.22”。
      --ansi            Force ANSI output
      --no-ansi         Disable ANSI output
  -n, --no-interaction  Do not ask any interactive question
      --env[=ENV]       The environment the command should run under.
  -v|vv|vvv, --verbose  啰嗦显示出执行结果的信息

Available commands（对应“Usage”的第一项）:
  clear-compiled      Remove the compiled class file
  down                Put the application into maintenance mode
  env                 Display the current framework environment
  help                显示帮助信息。`php artisan help migrate` 等同于 `php artisan migrate -h`
  list                所有可用命令清单
  migrate             执行数据库迁移文件
  optimize            Optimize the framework for better performance
  serve               Serve the application on the PHP development server
  tinker              Interact with your application
  up                  Bring the application out of maintenance mode
 app
  app:name            Set the application namespace
 auth
  auth:clear-resets   Flush expired password reset tokens
 cache
  cache:clear         Flush the application cache
  cache:table         Create a migration for the cache database table
 config
  config:cache        Create a cache file for faster configuration loading
  config:clear        Remove the configuration cache file
 db
  db:seed             Seed the database with records
 event
  event:generate      Generate the missing events and listeners based on registr
ation
 key
  key:generate        Set the application key
 make
  make:auth           ✪创建一个基本的登录、注册小系统。
  make:console        Create a new Artisan command
  make:controller     创建一个控制器类
  make:event          Create a new event class
  make:job            Create a new job class
  make:listener       Create a new event listener class
  make:middleware     Create a new middleware class
  make:migration      Create a new migration file
  make:model          创建一个模型类，后跟 `-m` 参数可附带生成迁移文件，非常便捷。
  make:policy         Create a new policy class
  make:provider       Create a new service provider class
  make:request        Create a new form request class
  make:seeder         Create a new seeder class
  make:test           Create a new test class
 migrate
  migrate:install     在数据库中创建迁移记录表 `migrations`
  migrate:refresh     Reset and re-run all migrations
  migrate:reset       回滚所有迁移记录
  migrate:rollback    回滚最近一次的迁移记录
  migrate:status      Show the status of each migration
 queue
  queue:failed        List all of the failed queue jobs
  queue:failed-table  Create a migration for the failed queue jobs database tabl
e
  queue:flush         Flush all of the failed queue jobs
  queue:forget        Delete a failed queue job
  queue:listen        Listen to a given queue
  queue:restart       Restart queue worker daemons after their current job
  queue:retry         Retry a failed queue job
  queue:table         Create a migration for the queue jobs database table
  queue:work          Process the next job on a queue
 route
  route:cache         Create a route cache file for faster route registration
  route:clear         Remove the route cache file
  route:list          List all registered routes
 schedule
  schedule:run        Run the scheduled commands
 session
  session:table       Create a migration for the session database table
 vendor
  vendor:publish      Publish any publishable assets from vendor packages
 view
  view:clear          清除所有已编译的视图文件，在目录 `storage\framework\views` 中
```
<a name="LaravelCommand">
## `laravel` 命令

执行

```
laravel
```

得

```
Laravel Installer 1.3.3

Usage:
  command [options] [arguments]

Options:
  -h, --help            Display this help message
  -q, --quiet           Do not output any message
  -V, --version         Display this application version
      --ansi            Force ANSI output
      --no-ansi         Disable ANSI output
  -n, --no-interaction  Do not ask any interactive question
  -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output,
 2 for more verbose output and 3 for debug

Available commands:
  help  显示帮助信息
  list  所有可使用命令清单
  new   创建一个新的 Laravel 项目
```

其中最好用命令绝对是

```
laravel new blog
```

这样就轻松创建了一个名为 `blog` 项目，里面包含完整 Laravel 版本包！

这条命令等同于 Composer 命令的

```
composer create-project --prefer-dist laravel/laravel blog
```
<a name="LaravalDocStudy">
## `Laravel` 文档拾遗



<a name="foo">
## 琐碎

```bash
php artisan make:model Wiki -m

php artisan make:controller WikiController --resource

Soft Deleting

composer dump-autoload

php artisan migrate:rollback

php artisan vendor:publish --tag=laravel-pagination
在 resources/views/vendor/pagination 文件夹下修改分页样代码
```

（完）
