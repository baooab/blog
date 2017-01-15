## 流水操作

## 2017/01/15

1. [PHP Data Objects]()，from php.net
2. [PHP MySQL Querying data using simple SELECT statement](http://www.mysqltutorial.org/php-querying-data-from-mysql-table/)，from mysqltutorial.org 

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
