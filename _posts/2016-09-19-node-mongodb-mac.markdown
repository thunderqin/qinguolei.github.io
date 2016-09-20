---
layout:     post
title:      "node环境下 安装使用mongodb"
subtitle:   "mongodb环境配置"
date:       2016-09-19 12:00:00
author:     "Guolei"
header-img: ""
header-mask: 0.3
catalog:    true
tags:
    - mongodb
    - node
    - mac
---

> mongoDB 作为非关系型数据库，配合node使用，效果更棒

## 安装

```js
brew install mongodb
```

#开启服务

需要权限,因为mongodb 安装在/data/db下，需要权限才能创建访问

```js
sudo mongod
```

##操作数据库


1 ***首先，新建一个命令行 ctrl+n***

进入mongo环境

```js
mongod
```

2 ***创建一个数据库,名字是'guolei'***

```js
use guolei
```

可以通过

```js
show dbs
```

 查看数据库列表（如果看不到自己创建的数据库，需要插入数据）

3 ***新增数据***

数据表的名字叫'demo'

```js
db.demo.insert({name:'guolei'})
```

4  ***查看数据表****

```js
db.demo.find().pretty()
```
pretty是组织化的方式返回，更容易阅读，不加也行。

5 ***修改数据***

假如要把我的名字改成guanxi,执行

```js
db.demo.update({name:'guolei'},{$set:{'title':'guanxi'}})
```

6  ***删除***
增删改查。。。。

```js
db.demo.remove({'title':'guanxi'})
```

实际操作如下

![](/img/in-post/mongo/mongo-cli.jpeg)

备注： 可以使用Robomongodb这款可视化工具 操作数据库

## node环境使用MongoDB


新建一个目录，初始化

```js
git init
```

安装Mongodb模块

```js
npm  install mongodb
```

新建一个index.js

```js
var  mongodb = require('mongodb');
var  server  = new mongodb.Server('localhost', 27017, {});
var  db = new mongodb.Db('mydb', server, {});

//连接db
db.open(function(err, db){
    if(!err){
        console.log('connect db');
        db.createCollection('mycoll', {}, function(err, collection){
            if(err){
                console.log(err);
            }else{

                var tmp1 = {title:'hello'};
                   var tmp2 = {title:'world'};
                   collection.insert([tmp1,tmp2],{safe:true},function(err,result){
                   console.log(result);
                   });
                   collection.find().toArray(function(err,docs){
                   console.log('find');
                   console.log(docs);
                   });
                   collection.findOne(function(err,doc){
                    console.log('findOne');
                      console.log(doc);
                   });
            }

        });

    }else{
        console.log(err);
    }
});

```

最后执行

```js
node index.js
```

注意

1. 保证mongod 运行着
2. node版本>4

执行结果

![](/img/in-post/mongo/node-mongo.jpeg)

写这篇文章的时候，本人已经喝了四瓶啤酒，不详细的地方，大家海涵。。。。


### 著作权声明

本文demo借鉴了[whoamme](http://www.cnblogs.com/whoamme/p/3467374.html)的博客
