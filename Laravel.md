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

## 一、视图

### 数据共享给所有视图

在 `AppServiceProvider ` 的 `boot` 方法使用

```
use Illuminate\Support\Facades\View;

View::share('key', 'value');
```

视图中如此取得

```
{{ $key }}
```

### 视图合成器

新建 `App\Providers\ComposerServiceProvider.php`，添加至 `config\app.php` 的 `providers` 数组中。

在 `ComposerServiceProvider` 的 `boot` 方法里写入

```
View::composer(
    'profile', 'App\Http\ViewComposers\ProfileComposer'
);
```

新建 `App\Http\ViewComposers\ProfileComposer.php`，在 `__construct` 中注入依赖 `UserRepository`，在 `compose` 方法里借助 `$view` 给视图绑定数据。

```
public function compose(View $view)
{
    return $view->with('users', $this->users->getAllUsers());
}
```

每次 `profile` 视图渲染时，都会执行 `ProfileComposer@compose` 方法。

将视图合成器作用于多个视图，使用

```
视图合成器附加到多个视图
```

### 视图塑造器

视图塑造器与视图合成器非常相似，不同之处在于：视图塑造器在视图实例化时执行，而视图合成器在视图渲染时执行。

```
View::creator('profile', 'App\Http\ViewCreators\ProfileCreator');
```

## 二、Blade 模板

### 模板继承

布局文件

```
@yield('title')

@section('sidebar')
     Master sidebar
@show

<div class="container">
    @yield('content')
</div>
```

子文件

```
@extends('layouts.app')

@section('title', 'Page Title')

@section('sidebar')
    @parent
    <p>Son sidebar.</p>
@endsection

@section('content')
    <p>This is my body content.</p>
@endsection
```

`@parent` 继承父模板 sidebar section 的内容，而非直接覆盖父模板中这部分的内容。

### 显示数据

Blade `{{ }}` 语法会自动调用 PHP [`htmlentities` 函数](http://www.w3school.com.cn/php/func_string_htmlentities.asp) 来避免 XSS 攻击。

三目操作符在 Blade 中的简写形式。

```
{{ $name or 'Default' }}
```

使用 `Hello, @{{ name }}.` ，`{{}}` 会原样输出。

```
Hello, {{ name }}.
``` 

有大片区域需要原样显示，使用 `@verbatim` 指令。

```
@verbatim
    <div class="container">
        Hello, {{ name }}.
    </div>
@endverbatim
```

### 控制结构

`@unless` 除了。

```
@unless (Auth::check())
    你尚未登录。
@endunless
```

如果用户登录成功了，`Auth::check()` 返回 `true`。与`@unless` 结合使用， 指除了用户登录成功的情况，不显示`Auth::check()` 里的提示；登录未成功的情况，都会显示`Auth::check()` 里的提示（呵呵）。

### 循环

```
@forelse ($users as $user)
    <li>{{ $user->name }}</li>
@empty
    <p>没有用户</p>
@endforelse
```

当 `$users` 为空时，就会显示 `@empty` 下面的内容。

忽略当前迭代，接着往下循环 `@continue`、结束整个循环 `@break`。

```
@foreach ($users as $user)
    @if ($user->type == 1)
        @continue
    @endif

    <li>{{ $user->name }}</li>

    @if ($user->number == 5)
        @break
    @endif
@endforeach
```

简单点的话，这样写。

```
@foreach ($users as $user)
    @continue($user->type == 1)

    <li>{{ $user->name }}</li>

    @break($user->number == 5)
@endforeach
```

### [循环变量](https://laravel-china.org/docs/5.3/blade#loops)

可以在循环内访问 `$loop` 变量。这个变量可以提供一些有用的信息，比如当前循环的索引，当前循环是不是首次迭代，又或者当前循环是不是最后一次迭代。

```
@foreach ($users as $user)
    @if ($loop->first)
        This is the first iteration.
    @endif

    @if ($loop->last)
        This is the last iteration.
    @endif

    <p>This is user {{ $user->id }}</p>
@endforeach
```

如果你是在一个嵌套的循环中，你可以通过使用 `$loop` 变量的 `parent` 属性来获取父循环中的 `$loop` 变量：

```
@foreach ($users as $user)
    @foreach ($user->posts as $post)
        @if ($loop->parent->first)
            This is first iteration of the parent loop.
        @endif
    @endforeach
@endforeach
```

### 注释

```
{{-- 此注释将不会出现在渲染后的 HTML --}}
```

### 引入子视图

```
@include('shared.errors')

@include('view.name', ['some' => 'data'])
```

所有在父视图的可用变量在被引入的视图中都是可用的。

### 为集合渲染视图

```
// record/list.blade.php
<ul>
    @each('record.item', $records, 'record', 'record.no-items')
</ul>

// record/item.blade.php
<li>{{ $record->title }}</li>

// record/no-items.blade.php
<li>Sorry Charlie, No posts here.</li>
```

第一个参数是要渲染的视图；第二个参数是要迭代的数组或集合；第三个参数是在子视图中使用的迭代变量；第四个参数指一个视图，当要迭代数组或集合为空时，将使用这个参数提供的视图来渲染。

### 堆栈

master

```
<head>
    @stack('scripts')
</head>
```

son

```
@push('scripts')
    <script src="/example.js"></script>
@endpush
```

### 服务注入

（无）

### 扩充 Blade 命令

你甚至可以在 `AppServiceProvider` 的 `boot` 方法中使用 `Blade::directive` 注册自己的命令。

```
use Illuminate\Support\Facades\Blade;

Blade::directive('datetime', function($expression) {
    return "<?php echo $expression->format('m/d/Y H:i'); ?>";
});
```

这样使用。

```
@datetime($user->created_at)
```

报错

```
Trying to get property of non-object
```

## 三、国际化

### 简介

```
/resources
    /lang
        /en
            messages.php
        /es
            messages.php
```

```
App::setLocale($locale);

$locale = App::getLocale();

if (App::isLocale('en')) {
    //
}
```

### 提取语句

```
{{ trans('messages.welcome') }}

@lang('messages.welcome')
```

### 参数替换

```
# resources/lang/en/message.php
'welcome' => 'Welcome, :name',

# resources/lang/views/welcome.php
{{ trans('messages.welcome', ['name' => 'dayle']) }}
```

效果

```
Welcome, dayle
```

### 复数

```
'apples' => '{0} There are none|[1,19] There are some|[20,Inf] There are many',

{{ trans_choice('messages.apples', 10) }}
```

得

```
There are some
```

### 重写扩展包的语言包

（无）

## 四、编译资源文件 (Laravel Elixir)

Elixir 支持许多常见的 CSS 与 JavaScript 预处理器，例如 `Sass` 和 `Webpack`。

```
# gulpfile.js
elixir(mix => {
    mix.sass('app.scss')
       .webpack('app.js');
});
```

`app.scss` 默认地址 `resources\assets\sass\app.scss`，生成的 CSS 会在 `public/css/app.css`。

`app.js` 默认地址 `resources\assets\js\app.js`，生成的 CSS 会被在 `public/js/app.js`。


### 安装 Node

```
node -v
npm -v
```

### 安装 gulp

```
npm install --global gulp-cli
```

### 安装 Elixir

```
npm install
```

### 运行 Elixir

```
// 运行所有任务...
gulp

// 运行所有任务并压缩所有 CSS 及 JavaScript...
gulp --production
```

### 使用样式

合并多个 scss 文件至指定目录（使用 `sass` 方法）。

```
elixir(function(mix) {
    mix.sass([
        'app.scss',
        'controllers.scss'
    ], 'public/assets/css');
});
```

合并纯 CSS 文件（使用 `styles` 方法）

```
elixir(function(mix) {
    mix.styles([
        'normalize.css',
        'main.css'
    ], 'public/assets/css/site.css');
});
```
此方法的默认路径为 `resources/assets/css` 目录，而生成的 CSS 会被放置于 `public/css/all.css`，这里被放在了 `public/assets/css/site.css` 里。

### 关闭 Source Map

```
elixir.config.sourcemaps = false;

elixir(function(mix) {
    mix.sass('app.scss');
});
``` 

### [使用脚本](https://laravel-china.org/docs/5.3/elixir#working-with-scripts)

与使用样式非常类似。比如，想要把 `app/assets/js/app.js` 编译至 `public/dist/app.js`：

```
elixir(function(mix) {
    mix.webpack(
        './app/assets/js/app.js',
        './public/dist'
    );
});
```

多个 JavaScript 文件合并至单个文件，你可以使用 `scripts` 方法。这个方法可以自动生成 source maps，合并和压缩文件。

scripts 方法假设所有的路径都相对于 `resources/assets/js` 目录，且默认会将生成的 JavaScript 放置于 `public/js/all.js`：

```
elixir(function(mix) {
    mix.scripts([
        'order.js',
        'forum.js'
    ]);
});
```

调用多个 `scripts`，生成多个合并后的脚本文件（比如，下面生成了两个合并后的脚本文件）。

```
elixir(function(mix) {
    mix.scripts(['app.js', 'controllers.js'], 'public/js/app.js')
       .scripts(['forum.js', 'threads.js'], 'public/js/forum.js');
});
```

不再赘述。

### 资源版本

```
elixir(function(mix) {
    mix.version('css/app.css');
});
```
`version` 方法接收一个相对于 `public` 目录的文件名称，接着为你的文件名称加上唯一的哈希值，以防止文件被缓存。举例来说，生成出来的文件名称可能像这样：`all-16d570a7.css`

编译后的文件在 `/public/build/css` 或 `/public/build/js`  中。

```
{{ elixir('css/app.css') }}
```

被解析为

```
/build/css/app-86ff5d31a2.css
```

在页面中这样引入

```
<link rel="stylesheet" href="{{ asset(elixir('css/app.css')) }}">
```

`asset` 方法解析静态资源的绝对路径，相对于 `public` 目录，即 `{{ asset('demo.css') }}` 被解析为 `http://localhost/another/public/demo.css`。

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
