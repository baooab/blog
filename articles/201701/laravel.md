## 使用 Laravel

基于 Laravel 5.3 。

### 目录

- [软删除](#Soft Deleting)
- [迁移文件](#Migrations)

### [Soft Deleting](https://laravel.com/docs/5.3/eloquent#soft-deleting)

Model ：

```php
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\SoftDeletes;

class Flight extends Model
{
    use SoftDeletes;

    /**
     * The attributes that should be mutated to dates.
     *
     * @var array
     */
    protected $dates = ['deleted_at'];
}
```

Migration ：

```
Schema::table('flights', function ($table) {
    $table->softDeletes();
});
```

restore ：

```
App\Flight::withTrashed()
        ->where('airline_id', 1)
        ->restore();
```

truly remove ：

```
$flight->forceDelete();
```

### [Migrations](https://laravel.com/docs/5.3/migrations#columns)

#### #1. 创建迁移文件

并指明要创建的表明。

```
$ php artisan make:migration create_employees_table --create=employees
```

创建字段和字段修饰的写法看 [这里](https://laravel-china.org/docs/5.3/migrations#columns) 。

表是否存在。

```
if (Schema::hasTable('users')) {
    //
}
```

```
# 1. 运行迁移
$ php artisan migrate

# 2. 回滚迁移
$ php artisan migrate:rollback
```

[修改字段](https://laravel-china.org/docs/5.3/migrations#modifying-columns) 需要下载依赖 `doctrine/dbal` 。

```
$ composer require doctrine/dbal
```

### 尾牙

```
$ composer dump-autoload
```