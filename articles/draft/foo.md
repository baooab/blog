## 流水操作

## 2017/2/23
 
现在不懂的地方：
 
- 权限管理系统的设计
- 分级评论的实现
- API 是怎么写的

## 2017/2/15

```javascript
function addEvent(t, e, n) {
  window.attachEvent ? t.attachEvent("on" + e, n) : window.addEventListener && t.addEventListener(e, n, !1)
}
```

## 2017/1/20

[Arukas.io（樱花docker）免费搭建个人SS服务](http://www.iqcni.com/other/12.html)

[SwitchyOmega for Chromium](/FelisCatus/SwitchyOmega/releases)

[ShadowsocksR](/shadowsocksr/shadowsocksr-csharp/releases)

## 2017/1/19

JSONP 使用 script 标签 url 进脚本，这个脚本会调用本地的一个方法（相当于模拟了一个回调），被调用的本地方法的名字是 script 标签 url 进脚本时 url 中参数指明的，如：`?jsonp=callback`。

short and to the point 简短而中肯

weed out any bugs that might’ve snuck through 剔除所有悄悄通过的 bug

看了 jQuery 官方的博客，从 2006 年初看到 2011 年 5 月份。下面是我的笔记：

```
http://blog.jquery.com/2006/06/30/jquery-10-alpha-release/
http://blog.jquery.com/2006/08/26/jquery-10/

http://blog.jquery.com/2007/01/14/jquery-birthday-11-new-site-new-docs/
jQuery 一周年发布 1.1 版本。
引入新方法 .parents() .css() .attr() .one() .unbind() 代替旧方法，体积减小 40% 多。

http://blog.jquery.com/2007/08/24/jquery-114-faster-more-tests-ready-for-12/
jQuery 1.1.4 是 1.1.x 分支的最后一个版本。 
引入 $.noConflict()。
当你使用

var jq=$.noConflict();

原来可使用的 $ 和 jQuery 都无效，有效的仅是 jq。
.slice()  :has()
.extend() 递归 merge，加参数 true 会更深一层 merge。
宣布了一些过时的函数以及替代函数。

http://blog.jquery.com/2007/09/10/jquery-1-2-released/
$.getScript 
$.getJSON (using JSONP) 是 jsonp 的话，在查询字符串里添加「=?」。 
.height() / .width() for document and window
:header 匹配所有的标题 （h1, h2, h3, h4, h5, 和 h6 标签元素）。
jQuery 1.2 Full Release Notes → http://blog.jquery.com/2007/09/10/jquery-12-jqueryextendawesome/

jQuery 1.2.1 
.eq() 方法回归，因为有大量插件依赖。起先提供的替代方法 .slice() 使用的并不优雅。

jQuery in Action 2007.10

jQuery 1.2.3 命名事件
$("div").bind("click.plugin", function(){}); 这个 click 事件的名字叫 plugin。解绑用 $("div").unbind(".plugin")

jQuery 1.2.6 忽略了 1.2.4  和 1.2.5 版本，因为 built incorrectly。 

2008 年 jQuery 是荒年，纠缠在 1.2.2 之后版本中，感觉无进步，就是在改 bug。

http://blog.jquery.com/2009/01/14/jquery-13-and-the-jquery-foundation/
使用 Sizzle 引擎（从 jQuery 中独立出的），模块重写和修正。优化了。.1 .2 版本 bug 局部修复。

http://blog.jquery.com/2009/03/13/this-week-in-jquery-vol-1/
This Week in jQuery  每周一次报道
一直到 2010 底，出到 jQuery 1.4.4  版本，就没有什么大动作了。

jQuery中的.bind()、.live()和.delegate()之间区别分析？？

http://blog.jquery.com/2011/01/31/jquery-15-released/
完全重写 Ajax 模块，引入延迟对象。jQuery.ajax 返回 jqXHR 对象。

var jqxhr = $.ajax({ url: "example.php" })
    .success(function() { alert("success"); })
    .error(function() { alert("error"); })
    .complete(function() { alert("complete"); });

http://blog.jquery.com/2011/05/03/jquery-16-released/
重写了 Attribute 模块。
https://code.jquery.com/jquery/

http://motherrussia.polyester.se/jquery-plugins/tablesorter
```

## 2017/1/18

```javascript
// http://www.ruanyifeng.com/blog/2013/05/jquery-free.html
function $$(selector, context) {
    context = context || document;
    var elements = context.querySelectorAll(selector);
    return Array.prototype.slice.call(elements);
}
```

## 2017/01/16 

### 软删除

以 `User` 为例：

User Model：

```
use Illuminate\Database\Eloquent\SoftDeletes;

use SoftDeletes;

/**
 * The attributes that should be mutated to dates.
 *
 * @var array
 */
protected $dates = ['deleted_at'];
```

User Migration：

```
$table->softDeletes();
```

## 2017/01/15 使用 PDO 从 MySQL 中 SELECT 出数据

### 参考资料

1. [PHP Data Objects]()，from php.net
2. [PHP MySQL Querying data using simple SELECT statement](http://www.mysqltutorial.org/php-querying-data-from-mysql-table/)，from mysqltutorial.org 

### 创建查询表格 `empployees`

```
php artisan make:migration create_employees_table
```

得 `database\migrations\2017_01_15_115717_create_employees_table.php`：

```php
Schema::create('employees', function (Blueprint $table) {
    $table->increments('id');
    $table->string('firstname');
    $table->string('lastname');
    $table->string('jobtitle');
    $table->timestamps();
});

Schema::dropIfExists('employees');
```

```
php artisan make:seeder EmployeesTableSeeder
```

得 `database\seeds\EmployeesTableSeeder.php`：

```php
factory(App\Employee::class, 20)->create();
```

`database\seeds\DatabaseSeeder.php`：

```php
$this->call(EmployeesTableSeeder::class);
```

`database\factories\ModelFactory.php`（[写法看这里](https://github.com/fzaninotto/Faker)）：

```
$factory->define(App\Employee::class, function (Faker\Generator $faker) {

    return [
        'firstname' => $faker->firstName,
        'lastname' => $faker->lastName,
        'jobtitle' => $faker->jobTitle,
    ];
});
```

执行

```
php artisan make:model Employee
```

得 `app\Employee.php`。

```
php artisan migrate

php artisan migrate:rollback

php artisan db:seed
```

### 查询数据库表数据

看这个就够了 → [PHP MySQL Querying data using simple SELECT statement](http://www.mysqltutorial.org/php-querying-data-from-mysql-table/)，from mysqltutorial.org 

## 2017/01/15 使用 PDO 向 MySQL 插入数据

```
php artisan make:model Task -m
```

迁移文件内容（写法参考→[这里](https://laravel.com/docs/5.3/migrations#columns)）：

```
Schema::create('tasks', function (Blueprint $table) {
    $table->increments('id');
    $table->string('subject', 45);
    $table->date('start_date');
    $table->date('end_date');
    $table->string('description', 200);
    $table->timestamps();
});
```

创建种子文件：

```
php artisan make:seeder TasksTableSeeder
```
种子文件注册到 `DatabaseSeeder`：

```
$this->call(TasksTableSeeder::class);
```

种子文件内容：

```
factory(App\Task::class, 20)->create();
```

修改 `ModelFactory`：

```
$factory->define(App\Task::class, function (Faker\Generator $faker) {

    return [
        'subject' => $faker->text(45),
        'start_date' => $faker->date,
        'end_date' => $faker->date,
        'description' => $faker->text(200),
    ];
});
```

执行

```
php artisan db:seed
```

## 使用 PDO 调用 MySQL 存储过程

http://www.mysqltutorial.org/php-calling-mysql-stored-procedures/
