MongoDB 是由C++语言编写的，是一个基于分布式文件存储的开源数据库系统。

在高负载的情况下，添加更多的节点，可以保证服务器性能。

MongoDB 旨在为WEB应用提供可扩展的高性能数据存储解决方案。

MongoDB 将数据存储为一个文档，数据结构由键值(key=>value)对组成。MongoDB 文档类似于 JSON 对象。字段值可以包含其他文档，数组及文档数组。

# 主要特点
- MongoDB的提供了一个面向文档存储，操作起来比较简单和容易。
- 你可以在MongoDB记录中设置任何属性的索引 (如：FirstName="Sameer",Address="8 Gandhi Road")来实现更快的排序。
- 你可以通过本地或者网络创建数据镜像，这使得MongoDB有更强的扩展性。
- 如果负载的增加（需要更多的存储空间和更强的处理能力） ，它可以分布在计算机网络中的其他节点上这就是所谓的分片。
- Mongo支持丰富的查询表达式。查询指令使用JSON形式的标记，可轻易查询文档中内嵌的对象及数组。
- MongoDb 使用update()命令可以实现替换完成的文档（数据）或者一些指定的数据字段 。
- Mongodb中的Map/reduce主要是用来对数据进行批量处理和聚合操作。
- Map和Reduce。Map函数调用emit(key,value)遍历集合中所有的记录，将key与value传给Reduce函数进行处理。
- Map函数和Reduce函数是使用Javascript编写的，并可以通过db.runCommand或mapreduce命令来执行MapReduce操作。
- GridFS是MongoDB中的一个内置功能，可以用于存放大量小文件。
- MongoDB允许在服务端执行脚本，可以用Javascript编写某个函数，直接在服务端执行，也可以把函数的定义存储在服务端，下次直接调用即可。
- MongoDB支持各种编程语言:RUBY，PYTHON，JAVA，C++，PHP，C#等多种语言。
- MongoDB安装简单。

# 启动

## 服务
    mongod -dbpath=/data/db 

## shell
    mongo

## web用户界面
    mongod -dbpath=/data/db --rest

如果你的MongoDB运行端口使用默认的27017，你可以在端口号为28017访问web用户界面，即地址为：http://localhost:28017。


# 基础概念

SQL术语/概念 |	MongoDB术语/概念 |	解释/说明
---|---|---
database |	database |	数据库，相同
table |	collection| 集合替代了表的概念
row 	|document 	|文档记录了每条数据记录
column 	|field 	|域替代了数据项,不同文档中的域类型不需要相同
index 	|index 	|支持索引
table joins　|嵌入文档 |MongoDB不支持表连接
primary key 	|primary key |	主键,MongoDB自动将_id字段设置为主键

# 数据库
## 数据库命名规则
数据库名可以是满足以下条件的任意UTF-8字符串。
- 不能是空字符串（"")。
- 不得含有' '（空格)、.、$、/、\和\0 (空宇符)。
- 应全部小写。
- 最多64字节。

## 内置数据库
### admin
从权限的角度来看，这是"root"数据库。要是将一个用户添加到这个数据库，这个用户自动继承所有数据库的权限。一些特定的服务器端命令也只能从这个数据库运行，比如列出所有的数据库或者关闭服务器。
### local
这个数据永远不会被复制，可以用来存储限于本地单台服务器的任意集合
### config
当Mongo用于分片设置时，config数据库在内部使用，用于保存分片的相关信息。

# 文档
- MongoDB 的文档不需要设置相同的字段，并且相同的字段不需要相同的数据类型，
- 文档中的键/值对是有序的。
- 文档中的值不仅可以是在双引号里面的字符串，还可以是其他几种数据类型（甚至可以是整个嵌入的文档)。
- MongoDB区分类型和大小写。
- MongoDB的文档不能有重复的键。
- 文档的键是字符串。除了少数例外情况，键可以使用任意UTF-8字符。

## 文档键命名规范
- 键不能含有\0 (空字符)。这个字符用来表示键的结尾。
- .和$有特别的意义，只有在特定环境下才能使用。
- 以下划线"_"开头的键是保留的(不是严格要求的)。

# 集合collection
- 集合名不能是空字符串""。
- 集合名不能含有\0字符（空字符)，这个字符表示集合名的结尾。
- 集合名不能以"system."开头，这是为系统集合保留的前缀。
- 用户创建的集合名字不能含有保留字符。有些驱动程序的确支持在集合名里面包含，这是因为某些系统生成的集合中包含该字符。除非你要访问这种系统创建的集合，否则千万不要在名字里出现$。　

## Capped Collection
capped collections

Capped collections 就是固定大小的collection。

它有**很高的性能以及队列过期的特性(过期按照插入的顺序)**. 有点和 "RRD" 概念类似。

Capped collections是高性能自动的维护对象的插入顺序。它非常适合类似记录日志的功能 和标准的collection不同，你必须要显式的创建一个capped collection， 指定一个collection的大小，单位是字节。collection的数据存储空间值提前分配的。

要注意的是指定的存储大小包含了数据库的头信息。

db.createCollection("mycoll", {capped:true, size:100000})

- 在capped collection中，你能添加新的对象。
- 能进行更新，然而，对象不会增加存储空间。如果增加，更新就会失败 。
- 数据库不允许进行删除。使用drop()方法删除collection所有的行。
- 注意: 删除之后，你必须显式的重新创建这个collection。
- 在32bit机器中，capped collection最大存储为1e9( 1X109)个字节。

# 元数据
元数据

数据库的信息是存储在集合中。它们使用了系统的命名空间：

    <dbname>.system.*

集合命名空间|描述
---|---
dbname.system.namespaces | 列出所有名字空间。
dbname.system.indexes | 列出所有索引。
dbname.system.profile | 包含数据库概要(profile)信息。
dbname.system.users | 列出所有可访问数据库的用户。
dbname.local.sources | 包含复制对端（slave）的服务器信息和状态。

对于修改系统集合中的对象有如下限制。

- 在{{system.indexes}}插入数据，可以创建索引。但除此之外该表信息是不可变的(特殊的**drop index**命令将自动更新相关信息)。
- {{system.users}}是可修改的。 
- {{system.profile}}是可删除的。

# 常用数据类型
数据|类型 | 描述
---|---|---
String|字符串。 | 存储数据常用的数据类型。在 MongoDB 中，UTF-8 编码的字符串才是合法的。
Integer | 整型数值。 | 用于存储数值。根据你所采用的服务器，可分为 32 位或 64 位。
Boolean | 布尔值。 | 用于存储布尔值（真/假）。
Double	 | 双精度浮点值。| 用于存储浮点值。
Min/Max keys | 相当于比较符号 | 将一个值与 BSON（二进制的 JSON）元素的最低值和最高值相对比。
Arrays	| 数组|用于将数组或列表或多个值存储为一个键。　
Timestamp	|时间戳。 | 记录文档修改或添加的具体时间。
Object	|-|用于**内嵌文档**。|
Null	|-|用于创建空值。|
Symbol	|符号。|该数据类型基本上等同于字符串类型，但不同的是，它一般用于采用特殊符号类型的语言。
Date	|日期时间。|用 UNIX 时间格式来存储当前日期或时间。你可以指定自己的日期时间：创建 Date 对象，传入年月日信息。
Object ID	|对象 ID。|用于创建文档的 ID。
Binary Data	|二进制数据。|用于存储二进制数据。
Code	|代码类型。|用于在文档中存储 JavaScript 代码。
Regular expression	|正则表达式类型。|用于存储正则表达式。

# 链接
## shell
    mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]

    mongodb://localhost
    mongodb://username:password@hostname/dbname
    mongodb://admin:123456@localhost/test #链接到指定数据库
    mongodb://localhost,localhost:27018,localhost:27019

连接本地数据库服务器，端口是默认的。
    
    mongodb://localhost

使用用户名fred，密码foobar登录localhost的admin数据库。
    
    mongodb://fred:foobar@localhost

使用用户名fred，密码foobar登录localhost的baz数据库。
    
    mongodb://fred:foobar@localhost/baz

连接 replica pair, 服务器1为example1.com服务器2为example2。
    
    mongodb://example1.com:27017,example2.com:27017

连接 replica set 三台服务器 (端口 27017, 27018, 和27019):
    
    mongodb://localhost,localhost:27018,localhost:27019

连接 replica set 三台服务器, 写入操作应用在主服务器 并且分布查询到从服务器。

    mongodb://host1,host2,host3/?slaveOk=true

直接连接第一个服务器，无论是replica set一部分或者主服务器或者从服务器。

    mongodb://host1,host2,host3/?connect=direct;slaveOk=true

当你的连接服务器有优先级，还需要列出所有服务器，你可以使用上述连接方式。

安全模式连接到localhost:

    mongodb://localhost/?safe=true

以安全模式连接到replica set，并且等待至少两个复制服务器成功写入，超时时间设置为2秒。
    
    mongodb://host1,host2,host3/?safe=true;w=2;wtimeoutMS=2000

## options
- replicaSet=name 	
    - 验证replica set的名称。
    - Impliesconnect=replicaSet.
- slaveOk=true|false 	
    - true:
        - 在connect=direct模式下，驱动会连接第一台机器，即使这台服务器不是主。
        - 在connect=replicaSet模式下，驱动会发送所有的写请求到主并且把读取操作分布在其他从服务器。
    - false:
        - 在 connect=direct模式下，驱动会自动找寻主服务器. 
        - 在connect=replicaSet 模式下，驱动仅仅连接主服务器，并且所有的读写命令都连接到主服务器。

- safe=true|false 	
    - true: 在执行更新操作之后，驱动都会发送getLastError命令来确保更新成功。(还要参考 wtimeoutMS).
    - false: 在每次更新之后，驱动不会发送getLastError来确保更新成功。
- w=n 
    - 驱动添加 { w : n } 到getLastError命令. 应用于safe=true。
- wtimeoutMS=ms 
    - 驱动添加 { wtimeout : ms } 到 getlasterror 命令. 应用于 safe=true.
- fsync=true|false 	
    - true: 驱动添加 { fsync : true } 到 getlasterror 命令.应用于 safe=true.
    - false: 驱动不会添加到getLastError命令中。

- journal=true|false 
    - 如果设置为 true, 同步到 journal (在提交到数据库前写入到实体中). 应用于 safe=true
- connectTimeoutMS=ms
    - 可以打开连接的时间。
- socketTimeoutMS=ms 	
    - 发送和接受sockets的时间。

# 比较语法
操作 |	格式 |	范例| 	
---|---|---
等于 |	{<key>:<value>}| 	db.col.find({"by":"菜鸟教程"}).pretty() 	
小于 |	{<key>:{$lt:<value>}} |	db.col.find({"likes":{$lt:50}}).pretty() 
小于或等于 |	{<key>:{$lte:<value>}}| 	db.col.find({"likes":{$lte:50}}).pretty() 
大于 |	{<key>:{$gt:<value>}} |	db.col.find({"likes":{$gt:50}}).pretty() 
大于或等于| 	{<key>:{$gte:<value>}} |	db.col.find({"likes":{$gte:50}}).pretty()
不等于 |	{<key>:{$ne:<value>}} |	db.col.find({"likes":{$ne:50}}).pretty() 

# 逻辑符号
## AND
db.col.find({key1:value1, key2:value2}).pretty()
## OR
>db.col.find(
   {
      $or: [
	     {key1: value1}, {key2:value2}
      ]
   }
).pretty()

# $type
如果想获取 "col" 集合中 title 为 String 的数据，你可以使用以下命令：

>db.col.find({"title" : {$type : 2}})

# 索引
>db.COLLECTION_NAME.ensureIndex({KEY:1})

Parameter|	Type|	Description
---|---|---
background|	Boolean|	建索引过程会阻塞其它数据库操作，background可指定以后台方式创建索引，即增加 "background" 可选参数。 "background" 默认值为false。
unique	|Boolean|	建立的索引是否唯一。指定为true创建唯一索引。默认值为false.
name	|string|	索引的名称。如果未指定，MongoDB的通过连接索引的字段名和排序顺序生成一个索引名称。
dropDups	|Boolean|	在建立唯一索引时是否删除重复记录,指定 true 创建唯一索引。默认值为 false.
sparse	|Boolean|	对文档中不存在的字段数据不启用索引；这个参数需要特别注意，如果设置为true的话，在索引字段中不会查询出不包含对应字段的文档.。默认值为 false.
expireAfterSeconds	|integer|	指定一个以秒为单位的数值，完成 TTL设定，设定集合的生存时间。
v	|index version|	索引的版本号。默认的索引版本取决于mongod创建索引时运行的版本。
weights	document	|索引权重值，|数值在 1 到 99,999 之间，表示该索引相对于其他索引字段的得分权重。
default_language	|string|	对于文本索引，该参数决定了停用词及词干和词器的规则的列表。 默认为英语
language_override	|string|	对于文本索引，该参数指定了包含在文档中的字段名，语言覆盖默认的language，默认值为 language.

>db.values.ensureIndex({open: 1, close: 1}, {background: true})

# 聚合
the group aggregate field 'ele' must be defined as an expression inside an object
- 集合内的查询只能针对一个单一对象(比如一个组的mean)

表达式|	描述
---|---
$sum	|计算总和。
-|db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : "$likes"}}}])
$avg	|计算平均值
-|db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$avg : "$likes"}}}])
$min	|获取集合中所有文档对应值得最小值。
-|db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$min : "$likes"}}}])
$max	|获取集合中所有文档对应值得最大值。
-|db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$max : "$likes"}}}])
$push	|在结果文档中插入值到一个数组中。
-|db.mycol.aggregate([{$group : {_id : "$by_user", url : {$push: "$url"}}}])
$addToSet|	在结果文档中插入值到一个数组中，但不创建副本。	
-|db.mycol.aggregate([{$group : {_id : "$by_user", url : {$addToSet : "$url"}}}])
$first|	根据资源文档的排序获取第一个文档数据。
-|db.mycol.aggregate([{$group : {_id : "$by_user", first_url : {$first : "$url"}}}])
$last|	根据资源文档的排序获取最后一个文档数据	
-|db.mycol.aggregate([{$group : {_id : "$by_user", last_url : {$last : "$url"}}}])

# 管道
表达式：处理输入文档并输出。表达式是无状态的，只能用于计算当前聚合管道的文档，不能处理其它的文档。

这里我们介绍一下聚合框架中常用的几个操作：

- $project：修改输入文档的结构。可以用来重命名、增加或删除域，也可以用于创建计算结果以及嵌套文档。
- $match：用于过滤数据，只输出符合条件的文档。$match使用MongoDB的标准查询操作。
- $limit：用来限制MongoDB聚合管道返回的文档数。
- $skip：在聚合管道中跳过指定数量的文档，并返回余下的文档。
- $unwind：将文档中的某一个数组类型字段拆分成多条，每条包含数组中的一个值。
- $group：将集合中的文档分组，可用于统计结果。
- $sort：将输入文档排序后输出。
- $geoNear：输出接近某一地理位置的有序文档。


    db.articles.aggregate( [
        { $match : { score : { $gt : 70, $lte : 90 } } },
        { $group: { _id: null, count: { $sum: 1 } } }
    ] );

# 复制
mongodb的复制至少需要两个节点。其中一个是主节点，负责处理客户端请求，其余的都是从节点，负责复制主节点上的数据。

mongodb各个节点常见的搭配方式为：一主一从、一主多从。

主节点记录在其上的所有操作oplog，**从节点定期轮询主节点获取这些操作**，然后对自己的数据副本执行这些操作，从而保证从节点的数据与主节点一致。 

![image](http://www.runoob.com/wp-content/uploads/2013/12/replication.png)

## 副本集设置
    mongod --port "PORT" --dbpath "YOUR_DB_DATA_PATH" --replSet "REPLICA_SET_INSTANCE\_NAME"
### 实例

    mongod --port 27017 --dbpath "D:\set up\mongodb\data" --replSet rs0

以上实例会启动一个名为rs0的MongoDB实例，其端口号为27017。


在Mongo客户端使用命令rs.initiate()来启动一个新的副本集。

我们可以使用rs.conf()来查看副本集的配置

查看副本集状态使用 rs.status() 命令

我们需要使用多条服务器来启动mongo服务。进入Mongo客户端，并使用rs.add()方法来添加副本集的成员。

rs.add() 命令基本语法格式如下：

>rs.add(HOST_NAME: PORT)

- MongoDB中你只能通过主节点将Mongo服务添加到副本集中， 判断当前运行的Mongo服务是否为主节点可以使用命令db.isMaster() 。

- MongoDB的副本集与我们常见的主从有所不同，主从在主机宕机后所有服务将停止，而副本集在主机宕机后，副本会接管主节点成为主节点，不会出现宕机的情况。

# 分片
![image](http://www.runoob.com/wp-content/uploads/2013/12/sharding.png)
- Shard:
    - 用于存储实际的数据块，实际生产环境中一个shard server角色可由几台机器组个一个relica set承担，防止主机单点故障
- Config Server:
    - mongod实例，存储了整个 ClusterMetadata，其中包括 chunk信息。
- Query Routers:
    - 前端路由，客户端由此接入，且让整个集群看上去像单一数据库，前端应用可以透明使用。

# MongoDB 备份(mongodump)与恢复(mongorestore)
mongodump -h dbhost -d dbname -o dbdirectory

mongorestore -h dbhost -d dbname --directoryperdb dbdirectory

# 监控
## mongostat 命令
mongostat是mongodb自带的状态检测工具，在命令行下使用。它会间隔固定时间获取mongodb的当前运行状态，并输出。如果你发现数据库突然变慢或者有其他问题的话，你第一手的操作就考虑采用mongostat来查看mongo的状态。 

## mongotop命令
mongotop提供了一个方法，用来跟踪一个MongoDB的实例，查看哪些大量的时间花费在读取和写入数据。 mongotop提供每个集合的水平的统计数据。默认情况下，mongotop返回值的每一秒。 

# 命令
- "show dbs" 命令可以显示所有数据的列表。
- "db" 命令可以显示当前数据库对象或集合。
- "use"命令，可以创建并连接到一个指定的数据库。
- db.dropDatabase() 删除当前数据库，
- db.collection.drop()
- db.COLLECTION_NAME.insert(document)
    - 也可以将数据定义为一个变量,执行db.col.insert(document)
    
            db.col.insert({title: 'MongoDB 教程', 
            description: 'MongoDB 是一个 Nosql 数据库',
            by: '菜鸟教程',
            url: 'http://www.runoob.com',
            tags: ['mongodb', 'database', 'NoSQL'],
            likes: 100})

-  db.col.save(document)
    - 如果不指定 _id 字段 save() 方法类似于 insert() 方法。如果指定 _id字段，则会更新该 _id 的数据。

            db.collection.save(
               <document>,
               {
                 writeConcern: <document>
               }
            )

  
- db.COLLECTION_NAME.find()
    - db.col.find().pretty()
        - 以格式化的方式显示文档
- db.col.update()

        db.collection.update(
           <query>,
           <update>,
           {
             upsert: <boolean>,
             multi: <boolean>,
             writeConcern: <document>
           }
        )
    
    - query : update的查询条件，类似sql update查询内where后面的。
    - update :  update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
    - upsert : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
    - multi : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
    - writeConcern :可选，抛出异常的级别。
    
            db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}})
            
            db.col.update( { "count" : { $gt : 3 } } , { $set : { "test2" : "OK"} },false,true ); 
    
- remove()
    - query :（可选）删除的文档的条件。
    - justOne : （可选）如果设为 true 或 1，则只删除一个文档。

    db.collection.remove(
       <query>,
       {
         justOne: <boolean>,
         writeConcern: <document>
       }
    )  
- MongoDB Limit() 方法
    如果你需要在MongoDB中读取指定数量的数据记录，可以使用MongoDB的Limit方法，limit()方法接受一个数字参数，该参数指定从MongoDB中读取的记录条数。
    语法

    limit()方法基本语法如下所示：
    
    >db.COLLECTION_NAME.find().limit(NUMBER)
- MongoDB Skip() 方法
    使用skip()方法来跳过指定数量的数据，skip方法同样接受一个数字参数作为跳过的记录条数。
    
    skip() 方法脚本语法格式如下：
    
    >db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER)
    
    实例
    
    以上实例只会显示第二条文档数据
    
    >db.col.find({},{"title":1,_id:0}).limit(1).skip(1)
    { "title" : "Java 教程" }
- sort
    - 其中 1 为升序排列，而-1是用于降序排列。
    >db.COLLECTION_NAME.find().sort({KEY:1})
- ensureIndex() 方法
    - 用于创建索引
    >db.COLLECTION_NAME.ensureIndex({KEY:1,KEY2:-1})
- aggregate() 方法
    - MongoDB中聚合的方法使用aggregate()。
    - >db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)
    
    - >db.col.aggregate([{$group:{_id:"$likes",num:{$sum:"$likes"}}}])
- mongod --port "PORT" --dbpath "YOUR_DB_DATA_PATH" --replSet "REPLICA_SET_INSTANCE_NAME"
    - 启动一个REPLICA_SET_INSTANCE_NAME名为的MongoDB实例，其端口号为PORT
- rs.initiate()来启动一个新的副本集。
- rs.conf()来查看副本集的配置
- 查看副本集状态使用 rs.status() 命令
- rs.add()方法来添加副本集的成员。
>rs.add(HOST_NAME: PORT)
- 判断当前运行的Mongo服务是否为主节点可以使用命令db.isMaster() 。
- mongorestore -h dbhost -d dbname --directoryperdb dbdirectory
- mongodump -h dbhost -d dbname -o dbdirectory