## 知识点

##### NoSQL简介
##### MongoDB简介
##### MongoDB 安装以及启动
##### MongoDB的相关概念
##### MongoDB数据类型
##### 课程总结

## NoSQL简介

##### NoSQL，泛指非关系型的数据库。随着互联网web2.0网站的兴起，传统的关系数据库在应付web2.0网站，特别是超大规模和高并发的SNS类型的web2.0纯动态网站已经显得力不从心，暴露了很多难以克服的问题，而非关系型的数据库则由于其本身的特点得到了非常迅速的发展。NoSQL数据库的产生就是为了解决大规模数据集合多重数据种类带来的挑战，尤其是大数据应用难题。
#### NoSQL数据库在以下的这几种情况下比较适用：
##### 1、数据模型比较简单；
##### 2、需要灵活性更强的IT系统；
##### 3、对数据库性能要求较高；
##### 4、不需要高度的数据一致性；
##### 5、对于给定key，比较容易映射复杂值的环境。

## MongoDB简介

##### MongoDB是一个基于分布式文件存储的数据库。由C++语言编写。旨在为WEB应用提供可扩展的高性能数据存储解决方案MongoDB是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。他支持的数据结构非常松散，是类似json的bson格式，因此可以存储比较复杂的数据类型。Mongo最大的特点是他支持的查询语言非常强大，其语法有点类似于面向对象的查询语言，几乎可以实现类似关系数据库单表查询的绝大部分功能，而且还支持对数据建立索引。

## 特点：

##### 它的特点是高性能、易部署、易使用，存储数据非常方便。主要功能特性有：

##### 面向集合存储，易存储对象类型的数据。
##### 模式自由。
##### 支持动态查询。
##### 支持完全索引，包含内部对象。
##### 支持复制和故障恢复。
##### 使用高效的二进制数据存储，包括大型对象（如视频等）。
##### 自动处理碎片，以支持云计算层次的扩展性。
##### 支持RUBY，PYTHON，JAVA，C++，PHP，C#等多种语言。
##### 文件存储格式为BSON（一种JSON的扩展）。
##### 可通过网络访问。

## MongoDB 安装以及启动

##### 官方网站下载：https://www.mongodb.com/download-center
##### 注意： 需要根据自身的系统来下载指定的版本

## ubuntu安装过程(以ubuntu16.04-64为例)

##### 在超级用户模式中操作

##### 将下载 mongodb-linux-x86_64-ubuntu1604-3.2.8.tgz 文件移动到 /usr/local
    mv mongodb-linux-x86_64-ubuntu1604-3.2.8.tgz /usr/local
##### 解压 mongodb-linux-x86_64-ubuntu1604-3.2.8.tgz
    tar xf mongodb-linux-x86_64-ubuntu1604-3.2.8.tgz
##### 将解压后的可执行文件路径添加到系统环境变量中
    修改文件/etc/bash.basrc文件，在最后添加如下内容：
    PATH=$PATH:/usr/local/mongodb-linux-x86_64-ubuntu1604-3.2.8/bin/
    export PATH
##### 重新启动环境变量
    source /etc/bash.bashrc
##### 创建默认数据库路径
    mkdir -p /data/db
##### 启动 mongod 服务
    １．直接运行　mongod 即可，使用默认数据库路径
##### mongod -dbpath/xxxx/yyyy 指定数据路径
##### 运行MongDB shell  连接其他主机的ｔｅｓｔ数据库
    mongo 连接本地默认数据库
    mongo 192.168.1.2./test  连接其他主机的test数据库
    mongo 192.168.1.1.2/test -u xxx -p yyyy  使用用户名和密码连接其他主机的数据库
   
## oDB的相关概念

##### 常见的概念有数据库, 表, 字段, 索引,主键等。在MongoDB中也有类似的概念，如下：

关系型概念 | MongoDB概念 | 含义
—- | —- | —- |
database | database | 数据库
table | collection | 数据库表/集合
row | document | 数据记录/文档
column | field | 数据字段/域
index | index | 索引
primary key | primary key | 主键,MongoDB自动将_id字段设置为主键
   
## 对比：

数据库表格式：
id | name | age
—- | —- | —- |
0001 | lisi | 10
jj0002 | zhangsan | 11

##### 结合格式：
    {
        "_id":ObjectId("56064886abe2f21f36b03134"),
        "name":"lisi"
        "age":10
    }
    {
         "_id":ObjectId("56064886abe2f21f36b03135),
        "name":"zhangsan"
        "age":11
    }
### 数据库
##### MongDB中数据库的命名规则

    数据库名可以是满足以下条件的任意UTF-8字符串。
    不能是空字符串（““)。
    不得含有空格、.、$、/、和。
    应全部小写。
    不要超过64字节。
    不要使用admin,local,config保留名字。

##### 在mongo shell中可以显示数据名称
    > show dbs
    local 0.000GB
    > db
    test
    >
### 集合
##### 集合就是 MongoDB文档组，类似于RDBMS (关系数据库管理系统：Relational Database Management System)中的表格。集合存在于数据库中，集合没有固定的结构，这意味这你在对集合可以插入不同格式和类型的数据，但通常抢矿下我们插入集合的数据都会有一定的关联性。当第一个文档插入是，集合就会被创建。
### 集合的命名规则
##### 集合名不能是空字符串“　”。
##### 集合名不能含有字符（空字符），这个字符表示集合名的结尾。
##### 集合名不能以"system."开头，这是为系统集合保留的前缀。
##### 用户创建的集合名字不能含有保留字符，不要包含$符号。

### 不同结构的文档可以插入同一个集合
    {"name":"lisi","age":10}
    {"name":"zhangsan","age":12,"gender":"male"}
    {"name":"wangwu","age":14,"gender":"female","address":"北京，海定区"}
### 文档
##### 文档是MongoDB的核心概念。文档由一系列键及其关联的值有序组成。比如：
    {"name":"lisi", "age": 10}
### 文档键的命名规则：
##### 文档的键是字符串。除了少数例外情况，键可以使用任意UTF-8字符。
#####      键不能含有 (空字符)。这个字符用来表示键的结尾。
#####      .和$有特别的意义，只有在特定环境下才能使用。
#####      以下划线 _ 开头的键是保留的。
### 注意   
##### 文档中的键/值对是有序的。
##### 文档中的值不仅可以是在双引号里面的字符串，还可以是其他几种数据类型（甚至可以是整个嵌入的文档)。
##### MongoDB区分类型和大小写。
##### MongoDB的文档不能有重复的键。

### MongoDB常用数据类型
##### 字符串。存储数据常用的数据类型。在 MongoDB 中，UTF-8 编码的字符串才是合法的。
##### 整型数值。用于存储数值。根据你所采用的服务器，可分为 32 位或 64 位。
##### 布尔值。用于存储布尔值（真/假）。
##### 双精度浮点值。用于存储浮点值。
##### Arrays 用于将数组或列表或多个值存储为一个键。
##### Timestamp 时间戳。记录文档修改或添加的具体时间。
##### Object 用于内嵌文档。
##### Null 用于创建空值。
##### Symbol 符号。该数据类型基本上等同于字符串类型，但不同的是，它一般用于采用特殊符号类型的语言。
##### Date 日期时间。用 UNIX 时间格式来存储当前日期或时间。创建 Date 对象，传入年月日信息。
##### Object ID 对象 ID。
##### 二进制数据
##### 代码类型
##### 正则表达式类型。


# MongoDB 数据库的创建及删除
### 数据库的创建
##### 使用 use dbname 命令创建新数据库，如果dbname已经存在，那么就切换到数据库。
    > use stu
    switched to db stu
    > db 
    stu
##### 当先数据库中鞋服一些数据后，通过show dbs就可以看到创建的数据库。
    > db.firstclass.insert({"name":"lisi","age":12})
    WriteResult({"nInserted":1})
    > show dbs
    local 0.000GB
    stu   0.000GB

### 数据库的删除
##### 使用　db.dropDatabase()来删除数据库
    > db
    stu
    > db.dropDatabase()
    {"drop":"stu","ok":1}
    > show dbs
    local 0.000GB
    test  0.000GB
## MongoDB集合的创建和删除
### 集合的创建
##### 使用db.collectionName.insert()创建。
    > db.one.insert({"name":"lisi","age":12})
    WriteResult({"nInserted":1})
### 集合的删除
##### 使用 db.collectionName.drop()删除集合。
    > db.one.drop()
    true
### MongoDB文档操作
#### 插入文档
##### 文档的数据结构和JSON基本一样,所有存储在集合中的数据都是BSON格式。
##### BSON是一种类json的一种二进制形式的存储格式,简称Binary JSON。 
##### 插入方法：
##### db.collectionName.insert(doc) 
##### db.collectionName.save(doc) 
    直接插入：
    > db.one.insert({"name":"lisi","age":12})
    WriteResult({"nInserted":1})
    > db.one.find()
    { "_id":ObjectId("578b4fc554ec6d203080b398"),"name":"lisi","age":12}
    >
    
    先保存于变量中：
    > doc {"name":"zhangsna","age":13};
    {"name":"zhangsan","age":13}
    > db.one.insert(doc);
    WriteResult({"nInserted":1})
    >
    
##### 如果不指定_id 字段 save() 方法类似于 insert() 方法。如果指定 _id 字段，则会更新该 _id的数据

### 更新文档
##### 更新方法：
##### db.collectionName.update()
##### db.collectionName.save()
    db.collectionName.update(
    {query},
    {update},
    {
    upsert: <boolean>
    multi: <boolean>
    writeConcern: <document>
    }
    )
    参数说明：
    query : update的查询条件。
    update : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内 set 后面的
    upset : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false, 不插入。
    multi : 可选，mongodb 默认是　false, 只更新找到的第一条记录，付过这个参数为truem酒吧按条件查出来多条记录全部更新。
    writeConcern : 可选，抛出异常的级别
    
    修改　name == zhangsan 的　age 为 20
    > db.one.update({"name":"zhangsan"},{$set:{"age":20}})
    WriteResult({"nMatched":1, "nUpserted" : 0, "nModified" : 1 })
    > db.one.find()
    { "_id" : ObjectId("578b4fc554ec6d203080b398"), "name" : "lisi", "age" : 12 }
    { "_id" : ObjectId("578b4fc554ec6d203080b399"), "name" : "zhangsan", "age" : 20 }
    >
    给_id为ObjectId("578b4fc554ec6d203080b399")的文档添加一个"gender"
    > db.one.save({ "_id" : ObjectId("578b4fc554ec6d203080b399"), "name" : "zhangsan", "age" : 20, "gender" : "male" })
    WriteResult({"nMatched":1, "nUpserted" : 0, "nModified" : 1 })
    > db.one.find()
    { "_id" : ObjectId("578b4fc554ec6d203080b398"), "name" : "lisi", "age" : 12 }
    { "_id" : ObjectId("578b4fc554ec6d203080b399"), "name" : "zhangsan", "age" : 20 }
    
##### 其他更新操作：
    //更新第一个符合条件
    db.one.update({"name":"zhangsan"},{$set:{"age":30}})
    
    //更新所有符合条件
    db.one.update({"name":"zhangsan"},{$set:{"age":30}},false,true)
    
    //没有符合条件，添加一条文档进去
    db.one.update({"name":"zhangsan"},{$set:{"age":30}},true,true)
    
    //将所有name=zhangsan的文档的age增加５
    db.one.update({"name":"zhangsan"},{$inc:{"age":5}},false,true)
    
    //将所有name=zhangsan 的文档的age和course字段删除
    db.one.update({"name":"zhangsan"},{$unset:{"age":1, "course":1}}, false,true)
    
    //在一个数组域中添加一个数据并且讲size域的值加１
    db.one.update({"age":10},{$push:{"course":"html"}, $inc:{"size":1}}, false,false)
    
    //在一个数组域中添加多个数据
    db.one.update({"age":10},{$pushAll:{"course":["html","python"]}}, false,false)
    
    //删除数组域中的一个数据
    db.one.update({"age":20},{$pop:{"course":-1}}, false,false)  //删除course第一个
    db.one.update({"age":20},{$pop:{"course":1}}, false,false)　　//删除course最后一个
    
    //删除数组域中的某个特定数据
    db.one.update({"age":20},{$pull:{"course":"python"}}, false,false)
    
    //删除数组域中的过个数据
    db.one.update({"age":20},{$pullALL:{"course":["python","C"]}}, false,false)
    
    //修改某个域的名字
    db.one.update({"age":20},{$rename:{"course":"class"}}, false,false)
    
    //在某个数组域中添加数据（数据不存在时，才会添加）
    db.one.update({"age":20},{$addToSet:{"course":"python"}}, false,true)
    
### 删除文档
###### 删除方法：　db.collectionName.remove()

    db.collectionName.remove(
        {query},
        {
           justOne: boolean,
           writeConcern: document
        }
    )
    参数说明：
    query: 删除制定条件的文档
    justOne: 设置为true或１是，仅仅删除第一个符合条件的文档，默认删除所有符合条件的
    writeConcern: 抛出异常
    
    > db.one.find()
    { "_id" : ObjectId("578b4fc554ec6d203080b398"), "name" : "lisi", "age" : 10 }
    { "_id" : ObjectId("578b4fc554ec6d203080b398"), "name" : "lisi1", "age" : 10 }
    { "_id" : ObjectId("578b4fc554ec6d203080b398"), "name" : "lisi2", "age" : 10 }
    > db.one.remove({"age":10},1)
    WriteResult({"nRmoved": 1 })
    > db.one.find()
    { "_id" : ObjectId("578b4fc554ec6d203080b398"), "name" : "lisi1", "age" : 10 }
    { "_id" : ObjectId("578b4fc554ec6d203080b398"), "name" : "lisi2", "age" : 10 }
    >
    
    >db.one.remove({})  //删除了第一个符合条件的文档
    WriteResult({"nRmoved": ２ })
    
### 查找文档
##### 查找方法
##### db.collectionName.find() 
##### db.collectionName.findOne()

##### 查找所有文档：
    db.collectionName.find()
##### 按照条件操作符查找：
    db.collectionName.find({"age": {$lt: 10}})   //   查询年龄小于　　１０　的文档
    db.collectionName.find({"age": {$lt3: 10}})  //　　查询年龄小于等于　　１０　的文档
    db.collectionName.find({"age": {$gte: 10}})  //　　查询年龄大于等于　　１０　的文档
    db.collectionName.find({"age": {$gt: 10}})   //　　查询年龄大于　　１０　的文档
    db.collectionName.find({"age": {$ne: 10}})   //    查询年龄不等于　　１０　的文档
    db.collectionName.find({"age": {$mod: [10,0]}})   //　　查询年龄能被１０整除的文档
    db.collectionName.find({"age": {$not: {$mod: [10,0]}}})  //　　查询年龄不能被１０整除的文档
    db.collectionName.find({"course": {$all: ["english","math"]}})   //　　查询course包含english和math的文档
    db.collectionName.find({"course": {$size: 3}})  //　　查找　course数组元素个数等于３的文档
    
    
    
    
    
    
    
    
    
    
    
