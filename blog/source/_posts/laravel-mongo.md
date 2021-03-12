---
title: laravel & mongo
date: 2019-06-21 11:21:53
tags:
---

# 在 Laravel 中使用 MongoDB


**安装**

* 推荐组件
```
composer require jenssegers/mongodb
```

* 修改数据库配置文件 config/database.php 中
```
添加 MongoDB 的数据库的信息:
'mongodb' => [    
        'driver'   => 'mongodb',    
        'host'     => 'localhost',    
        'port'     => 27017,    
        'database' => env('DB_CONNECTION', 'mongodb'),    
        'username' => '',    
        'password' => '',
],


```

**使用**

* 新增迁移

```
use Jenssegers\Mongodb\Schema\Blueprint;
public function up()
{
    Schema::connection('mongo')->create('product', function (Blueprint $collection) {
        $collection->string('name');
        $collection->string('mfn')->unique();
    });
}

```

* model 

```
Jenssegers\Mongodb\Eloquent\Model

class MongoModel extends Model
{
    protected $connection = 'mongo';

    protected $collection = 'product';

    public $timestamps = false;

}

```