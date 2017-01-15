## 流水操作

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
