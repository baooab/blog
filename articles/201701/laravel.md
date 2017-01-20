# 使用 Laravel

基于 Laravel 5.3 。

## 目录

- 一、[软删除](#soft-deleting)
- 二、[迁移和种子](#migrations-and-seeder)

## 一、[Soft Deleting](https://laravel.com/docs/5.3/eloquent#soft-deleting)

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

```php
Schema::table('flights', function ($table) {
    $table->softDeletes();
});
```

restore ：

```php
App\Flight::withTrashed()
        ->where('airline_id', 1)
        ->restore();
```

truly remove ：

```php
$flight->forceDelete();
```

## 二、[Migrations and Seeder](https://laravel.com/docs/5.3/migrations#columns)

### 2.1 创建迁移文件

创建迁移文件并指明要创建的表名：

```
$ php artisan make:migration create_employees_table --create=employees
```

创建字段和字段修饰的写法看 [这里](https://laravel-china.org/docs/5.3/migrations#columns) 。

表是否存在。

```php
if (Schema::hasTable('users')) {
    //
}
```

[修改字段](https://laravel-china.org/docs/5.3/migrations#modifying-columns) 需要下载依赖 `doctrine/dbal` 。

```
$ composer require doctrine/dbal
```

### 2.2 创建种子文件

```
$ php artisan make:seeder EmployeesTableSeeder
```

`EmployeesTableSeeder` 的内容：

```php
factory(App\Employee::class, 20)->create();
```

`DatabaseSeeder` 的内容：

```php
$this->call(EmployeesTableSeeder::class);
```

写 `database\factories\ModelFactory.php` （写法在 [这里](https://github.com/fzaninotto/Faker)）：

```php
$factory->define(App\Employee::class, function (Faker\Generator $faker) {

    return [
        'firstname' => $faker->firstName,
        'lastname' => $faker->lastName,
        'jobtitle' => $faker->jobTitle,
    ];
});
```

### 2.3 运行迁移和种子文件

```
# 1. 运行迁移
$ php artisan migrate

# 2. 种下种子
php artisan db:seed
```

### 尾牙

```
$ composer dump-autoload
```