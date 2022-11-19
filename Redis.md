

# Redis



### :taco:Nosql

为什么要使用Nosql？

大数据时代（一般的数据库无法进行分析处理了！）

纵观历史：

> 1、单机MySQL时代！

90年代，一个基本的网址访问量一般不会很大，但数据库完全足够！

服务器没有太大压力；

网址的瓶颈：

1. 数据量太大，一台机器放不下
2. 数据的索引，mysql单条超过300万条就要建立索引，机器内存放不下
3. 访问量（读写混合 ），服务器无法承受

发生以上三种情况之一，必须要晋级；

> 2、Memcached（缓存）+ Mysql/Oracle + 垂直拆分

一台mysql服务器不够用，扩容、优化数据结构、算法

但是：网址80%都是在读，每次都要查询数据库十分麻烦；所以说希望减轻数据库压力，是有缓存保证效率；

缓存主要解决“读”的问题

发展过程：

1. 优化数据结构和索引
2. 文件缓存（IO）
3. Memcached 缓存

> 3、分库分表 + 水平拆分 + MySql 集群

主从;读写分离

本质：数据库（读、写）

读的问题：缓存

写的问题：

+ 锁表，十分影响效率，高并发下会出现严重问题
+ 转战lnnodb：行锁
+ 慢慢开始使用分库分表来解决写的压力！MySQL推出了表分区，但并没有使用很多！
+ MySQL集群，很好满足了那个年代的需求

> 4、如今年代

三体中提到：近的300年称为技术爆炸

MySQL等关系型数据库就不够用了！数据量很多，变化很快~！

MySQL使用它存储一些比较大的文件，博客、图片没数据库很大，效率低；如果有一种数据库来专门处理这种数据MySQL压力就变的非常小（如何处理这些问题！），大数据的UI压力上，表几乎没法更大！

> 为什么要用NoSQL

个人信息，日志等

NoSQL很少的处理以上问题！



**NoSQL**

NoSQL = Not Only SQL （不仅仅是SQL）

泛指非关系型数据库的：表格（行 和 列），NoSQL在当今大数据时代发展十分迅速，Redis是发展最快的，当下必须掌握的一门技术！

数据存储不需要一个固定的格式！不需要多余的操作就可以横向扩展！



> NoSQL特点

1. 方便扩展（数据之间没有关系，很好的发展）
2. 大数据量，高性能（redis 1s写8万次，读11万次，NoSQL的缓存记录级，是一种细粒度的缓存，性能比较高）
3. 数据库是多样型的！（不需要设计数据库！随去随用！）
4. 传统的RDBMS和NoSQL

```
传统的 RDBS
- 结构化组织
- SQL
- 数据和关系存在单独的表中
- 操作，数据定义语言
- 严格的一致性
- 基础的事务操作
- ...
```

```
NoSQL
- 不仅仅是数据
- 没有固定的查询像语言
- 键值对存储，列存储，文档存储，图形数据库（社交关系）
- 最终一致性
- CPA定理 和 BASE （异地多活）
- 高性能、高可用、高可扩
- ...
```



> 了解：大数据时代的 3V+3高

大数据时代的 3V：主要描述问题的

1. Volume海量
2. Variety(多样)
3. elocity(实时)

大数据时代的 3高：主要对程序的要求

1. 高并发
2. 高性能
3. 高可扩

真正在公司中的实践：NoSQL + RDBNS 一起使用才是最强的！



### :taco:NoSQL四大分类

**KV键值对：**

+ 新浪：redis
+ 美团：redis + Tair
+ 百度、阿里：Redis + memecache

**文档型数据库：（bson格式 和 json 一样）**

+ MongDB（一般必须掌握）
  + MonfDBshijiyigejiyu分布式文件存储的数据库，C++编写
  + 主要用于处理大量文档
  + MongoDB是介于关系型数据库和非关系型数据库中间产品！MongoDB是非关系型数据库中功能最丰富，最像关系型数据库的
+ ConthDB

**列存储数据库：**

+ HBase
+ 分布式存储

**图关系型数据库：**

+ 不是存图像，是存关系；如社交网络，广告推荐！



### :taco:Redis入门

**概述**

> redis

Redis Remote Disctioonary Server ： 远程字典服务；

免费、开源、当下最热门的NoSQL之一，也被称为结构化数据库！



> redis能做什么

1. 内存存储、持久化：内存断电即失、所以说持久化很重要（rdb、aof）
2. 效率高，可以用于高速缓存
3. 发布订阅系统
4. 地图信息分析
5. 计时器、计数器（浏览量！）
6. ......

> 特性

1. 多样的数据类型
2. 持久化
3. 集群
4. 事务
5. ...

> 实验所需

官网：https://redis.com/

中文：http://redis.p2hp.com/

github：https://github.com/redis/redis

Redis 在 Linux上搭建使用！



### :taco:Linux安装Redis

redis默认端口：3679

下载地址：https://github.com/redis/redis/archive/7.0.5.tar.gz

```SH
# 减压
mv redis-7.0.5.tar.gz /opt/
cd /opt/
tar zxvf redis-7.0.5.tar.gz
# 减压后文件
[root@node01 opt]# cd redis-7.0.5
[root@node01 redis-7.0.5]# ls
00-RELEASENOTES     CONTRIBUTING.md  INSTALL    README.md   runtest-cluster    SECURITY.md    tests
BUGS                COPYING          Makefile   redis.conf  runtest-moduleapi  sentinel.conf  TLS.md
CODE_OF_CONDUCT.md  deps             MANIFESTO  runtest     runtest-sentinel   src            utils
```

配置文件：redis.conf

安装基本环境：安装 gcc-c++



```SH
make
...
make[1]: Leaving directory `/opt/redis-7.0.5/src'
make install
```

Redis 默认安装路径：/usr/local/bin

```SH
[root@node01 bin]# ls
redis-benchmark  redis-check-aof  redis-check-rdb  redis-cli  redis-sentinel  redis-server
[root@node01 bin]# pwd
/usr/local/bin
```

将redis配置复制到当前目录：（使用这个文件启动）

```go
mkdir config
cp /opt/redis-7.0.5/redis.conf config/
```

注意：redis 默认不是后台启动

```SH
vim config/redis.conf

daemonize yes
```

启动 Redis 服务: 通过指定配置文件

```sh
[root@node01 bin]# pwd
/usr/local/bin
[root@node01 bin]# redis-server config/redis.conf
[root@node01 bin]# redis-cli
127.0.0.1:6379>
[root@node01 bin]# redis-cli
127.0.0.1:6379> ping
PONG
127.0.0.1:6379> set name caixukun
OK
127.0.0.1:6379> get caixukun
(nil)
127.0.0.1:6379> keys *
1) "name"
```

进程：

```SH
[root@node01 ~]# ps -ef | grep redis
root      27202      1  0 05:40 ?        00:00:00 redis-server 127.0.0.1:6379
root      27217   8635  0 05:43 pts/0    00:00:00 redis-cli
root      27219   8753  0 05:43 pts/1    00:00:00 grep --color=auto redis
```

关闭 Redis : 进程消失

```SH
[root@node01 bin]# redis-cli
127.0.0.1:6379> SHUTDOWN
not connected> exit
```



### :taco:测试性能

```SH
[root@node01 bin]# ls
config  dump.rdb  redis-benchmark  redis-check-aof  redis-check-rdb  redis-cli  redis-sentinel  redis-serve
```

工具：redis-benchmark ； 一个压力测试功能，官方自带

简单测试：

```SH
[root@node01 bin]# redis-benchmark -h localhost -p 6379 -c 100 -n 10000

====== SET ======
  10000 requests completed in 0.10 seconds		# 10000 个请求0。10秒
  100 parallel clients							# 100 个并行
  3 bytes payload								# 每次写入3个 byte
  keep alive: 1									# 保持连接的数量 1
  host configuration "save": 3600 1 300 100 60 10000
  host configuration "appendonly": no
  multi-thread: no
...
```



### :taco:基础知识

Redis默认有16个数据库

```SH
[root@node01 bin]# cat config/redis.conf | grep ^databases
databases 16
```

默认使用的第 0 个数据库

```SH
# 使用`SELECT`切换数据库：
127.0.0.1:6379> SELECT 3
OK
# dbsize 查看数据库大小，仅仅针对本数据库
127.0.0.1:6379[3]> DBSIZE
(integer) 0
127.0.0.1:6379[3]> set name caixukun
OK
127.0.0.1:6379[3]> DBSIZE
(integer) 1
# 查看有哪些数据
127.0.0.1:6379[3]> KEYS *
1) "name"
127.0.0.1:6379[3]> KEYS name
1) "name“
# 查看数据内容
127.0.0.1:6379[3]> GET name
"caixukun"
```

清空全部数据库：flushall

清空当前数据库：flushadb

```SH
127.0.0.1:6379[3]> FLUSHALL
OK
127.0.0.1:6379[3]> KEYS *
(empty array)
```



**思考：**为什么redis是6379！

6379在是手机按键上MERZ对应的号码，而MERZ取自意大利歌女 Alessia Merz 的名字。MERZ长期以来被 ntirez 及其朋友当作愚蠢的代名词。作者antirez同学在 twitter上说将在下一篇博文中向大家解释为什么他选择 6379 作为[默认默认端口号。而现在这篇博文出炉，在解释了Redis的LRU机制之后，向大家解释了采用 6379 作为默认端口的原因。

> Redis 是单线程的！

命名Redis是很快的，官方表示，Redis 是基于内存操作的，CPU不是Redis性能的瓶颈；Redis的瓶颈是根据网络带宽和内存，和Iran可以使用单线程来实现，就使用单线程！

Redis 是 C 语言写的，官方提供的数据为 100000 + 的 QPS ， 不比同样使用 key/value  Memecache

**Redis 为什么单线程这么快？**

1. 误区1：高性能的服务器一定是多线程？
2. 误区2：多线程（PU上下文切换！）一定比单线程块

CPU、内存、硬盘速度！

核心：Redis 将所有的内存放在内存中，所以说使用单线程操作效率就是最高的。多线程（CPU上下文切换：耗时的操作！！！），对于内存系统来说，如果没有上下文切换，效率就是最高的！多次读写都是在一个CPU上的，在内存情况下，这就是最佳的方案！



### :taco:五大数据类型

Redis是一个开源（BSD许可），内存存储的数据结构服务器，可用作数据库，高速缓存和消息队列代理。它支持[字符串](https://www.redis.net.cn/tutorial/3508.html)、[哈希表](https://www.redis.net.cn/tutorial/3509.html)、[列表](https://www.redis.net.cn/tutorial/3510.html)、[集合](https://www.redis.net.cn/tutorial/3511.html)、[有序集合](https://www.redis.net.cn/tutorial/3512.html)，[位图](https://www.redis.net.cn/tutorial/3508.html)，[hyperloglogs](https://www.redis.net.cn/tutorial/3513.html)等数据类型。内置复制、[Lua脚本](https://www.redis.net.cn/tutorial/3516.html)、LRU收回、[事务](https://www.redis.net.cn/tutorial/3515.html)以及不同级别磁盘持久化功能，同时通过Redis Sentinel提供高可用，通过Redis Cluster提供自动[分区](https://www.redis.net.cn/tutorial/3524.html)。



#### :tangerine: Redis-Key

```SH
127.0.0.1:6379> set name caixukun
OK
127.0.0.1:6379> set agent 1		# set key
OK
127.0.0.1:6379> EXISTS agent	# 判断是否存在
(integer) 1
127.0.0.1:6379> MOVE name 1		# 移除 key
(integer) 1
127.0.0.1:6379> keys *			# 查看所有的 key
1) "agent"
127.0.0.1:6379> SELECT 1
OK
127.0.0.1:6379[1]> keys *
1) "name"
127.0.0.1:6379[1]> EXISTS name	
(integer) 1

```

设置过期时间

```SH
127.0.0.1:6379> SET name zhangsan
OK
127.0.0.1:6379> KEYS *
1) "agent"
2) "name"
127.0.0.1:6379> get name
"zhangsan"
127.0.0.1:6379> EXPIRE name 10
(integer) 1
127.0.0.1:6379> TTL name
(integer) 5
127.0.0.1:6379> TTL name
(integer) 2
127.0.0.1:6379> TTL name
(integer) -2
127.0.0.1:6379> get name
(nil)
```

查看数据类型

```sh
OK
127.0.0.1:6379> KEYS *
1) "agent"
2) "name"
127.0.0.1:6379> type name
string
127.0.0.1:6379> type agent
string
```



#### :tangerine: String

**字符串**

```SH
127.0.0.1:6379> set key1 v1				# 设置值 
OK
127.0.0.1:6379> get key1				# 获得值
"v1"
127.0.0.1:6379> KEYS *					# 获得所有的值
1) "key1"
127.0.0.1:6379> EXISTS key1
(integer) 1
127.0.0.1:6379> APPEND key1 "hello"		# 追加字符串，动态修改
(integer) 7								# 返回字符数
127.0.0.1:6379> get key1
"v1hello"
127.0.0.1:6379> STRLEN key1				# 获取字符串长度
(integer) 7
127.0.0.1:6379> APPEND key1 ",redis"
(integer) 13
127.0.0.1:6379> STRLEN key1
(integer) 13
127.0.0.1:6379> get key1
"v1hello,redis"
```

**自增：incr 和 decr**

```SH
127.0.0.1:6379> set views 0
OK
127.0.0.1:6379> get views
"0"
127.0.0.1:6379> incr views
(integer) 1
127.0.0.1:6379> incr views
(integer) 2
127.0.0.1:6379> get views
"2"
127.0.0.1:6379> decr views
(integer) 1
127.0.0.1:6379> decr views
(integer) 0
127.0.0.1:6379> get views
"0"
```

**步长：incrby 、decrby**

```SH
127.0.0.1:6379> incrby views 10
(integer) 10
127.0.0.1:6379> incrby views 10
(integer) 20
127.0.0.1:6379> decrby views 5
(integer) 15
127.0.0.1:6379> decrby views 5
```

**字符串范围 range**

```sh
127.0.0.1:6379> KEYS *
(empty array)
127.0.0.1:6379> set url www.baidu.com	# 设置url的值
OK
127.0.0.1:6379> get url
"www.baidu.com"
127.0.0.1:6379> getrange url 4 8		# 截取字符串
"baidu"
127.0.0.1:6379> getrange url 0 -1
"www.baidu.com"
127.0.0.1:6379> SETRANGE url 4 xxxxx	# 替换
(integer) 13
127.0.0.1:6379> get url
"www.xxxxx.com"
```

setex（值存在）： 设置过期时间

setnx（值不存在）： 不存在在设置；在分布式锁中常会使用

```SH
127.0.0.1:6379> set key1 60
OK
127.0.0.1:6379> setex key1 10 "hello"	# 设置10s过期
OK
127.0.0.1:6379> get key1
"hello"
127.0.0.1:6379> setnx key1 "redis"		# 如果 key1 不存在，创建
(integer) 1
127.0.0.1:6379> get key1
"redis"
```

+ mset：批量设置值
+ mget批量获取值

```SH
127.0.0.1:6379> mset k1 v1 k2 v2 k3 v3
OK
127.0.0.1:6379> KEYS *
1) "k2"
2) "k3"
3) "k1"
127.0.0.1:6379> mget k1 k2 k3
1) "v1"
2) "v2"
3) "v3"
# 如果不存在批量设置 msetnx
```

对象

```SH
set user:1 {name:zhnagsan,age:3} # 设置一个user:1 对象，使用json字符来保持一个对象

# key是一个巧妙的设计：user:{id}:{filed},如此设计在Redis中完全是Ok
127.0.0.1:6379> mset user:1:name zhangsan user:1:age 2
OK
127.0.0.1:6379> mget user:1:name user:1:age
1) "zhangsan"
2) "2"
```

getset：先get再set 

+ 如果不存在值，则返回 nil
+ 如果存在值：获取原来的值，并设置值

数据结构是相同的。

String类似的使用常见：value除了是我们的字符串，还可以是数字！

+ 计数器
+ 统计多单位的数量 uid:0:follow 0
+ 对象缓存存储

```:taco:
127.0.0.1:6379> getset db redis
(nil)
127.0.0.1:6379> get db
"redis"
127.0.0.1:6379> getset db mongodb
"redis"
127.0.0.1:6379> get db
"mongodb"
```



#### :tangerine:List

---

基本数据类型，列表

在 Redis 可以将 list 用作：栈、队列、阻塞队列

所有的 list 命令都是可以用 “l” 来开头的

```SH
##########################################################
127.0.0.1:6379> LPUSH list one 		# 将一个值或者多个值，插入到列表头部（左）
(integer) 1
127.0.0.1:6379> LPUSH list two
(integer) 2
127.0.0.1:6379> LPUSH list there
(integer) 3
127.0.0.1:6379> LRANGE list 0 -1	# 获取 list 的值
1) "there"
2) "two"
3) "one"
127.0.0.1:6379> LRANGE list 0 1		# 通过区间获取具体的值
1) "there"
2) "two"
##########################################################
127.0.0.1:6379> RPUSH list right	# 将一个值或者多个值，插入到列表头部（右）
(integer) 4
127.0.0.1:6379> LRANGE list 0 -1
1) "there"
2) "two"
3) "one"
4) "right"
##########################################################
LPOP
RPOP
127.0.0.1:6379> LRANGE list 0 -1
1) "there"
2) "two"
3) "one"
4) "right"
127.0.0.1:6379> LPOP list	# 移除第一个元素
"there"
127.0.0.1:6379> RPOP list	# 移除第二个元素
"right"
127.0.0.1:6379> LRANGE list 0 -1
1) "two"
2) "one"
##########################################################
Lindex
127.0.0.1:6379> lindex list 0	# 通过下标获取list的值
"two"
127.0.0.1:6379> lindex list 1
"one"
##########################################################
llist
127.0.0.1:6379> LLEN list	# 获取list的长度
(integer) 2
##########################################################

!
127.0.0.1:6379> lrem list 1 one		# 移除一个值，从上到下
(integer) 1
##########################################################
trim 修剪,list
127.0.0.1:6379> RPUSH mylist "hello"
(integer) 1
127.0.0.1:6379> RPUSH mylist "hello1"
(integer) 2
127.0.0.1:6379> RPUSH mylist "hello2"
(integer) 3
127.0.0.1:6379> ltrim mylist 1 2
OK
127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello1"
2) "hello2"
##########################################################
rpop lpush # 移除列表最后一个元素，添加到其他列表
127.0.0.1:6379> RPUSH mylist "hello"
(integer) 1
127.0.0.1:6379> RPUSH mylist "hello1"
(integer) 2
127.0.0.1:6379> RPUSH mylist "hello2"
(integer) 3
127.0.0.1:6379> RPOPLPUSH mylist myotherlist
"hello2"
127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello"
2) "hello1"
127.0.0.1:6379> LRANGE myotherlist 0 -1
1) "hello2"
##########################################################
判断列表是否存在
127.0.0.1:6379> EXISTS list
(integer) 0
##########################################################
lset 将列表中指定下标的值替换成新的值，
127.0.0.1:6379> EXISTS list
(integer) 0
127.0.0.1:6379> lset list 0 item
(error) ERR no such key
127.0.0.1:6379> LPUSH list value1
(integer) 1
127.0.0.1:6379> LRANGE list 0 0
1) "value1"
127.0.0.1:6379> LSET list 0 item
OK
127.0.0.1:6379> LRANGE list 0 0
1) "item"
##########################################################
linsert # 插入
127.0.0.1:6379> RPUSH mylist hello
(integer) 1
127.0.0.1:6379> RPUSH mylist world
(integer) 2
127.0.0.1:6379> LINSERT mylist before "world" "other"
(integer) 3
127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello"
2) "other"
3) "world"
```

> 小结

实际上是一个链表，left、right都可以创建

如果key不存在：创建新的链表

如果存在，新增内容；

如移除了所有的值，空链表，也代表不存在！

两边插入或改动值，效率最高！中间元素，相对来说效率会低一点



#### :tangerine:Set

---

Set 中的值是不能重读的！
无序的！

```SH
127.0.0.1:6379> SADD myset "hello"	# 添加一个值
(integer) 1
127.0.0.1:6379> SADD myset "world"
(integer) 1
127.0.0.1:6379> SADD myset "!!!"
(integer) 1
127.0.0.1:6379> smembers myset	# 查看
1) "hello"
2) "!!!"
3) "world"
127.0.0.1:6379> sismember myset hello	# 判断 hello 值是否存在 myset 中
(integer) 1
127.0.0.1:6379> scard myset	# set集合元素个数
(integer) 3
127.0.0.1:6379> srem myset !!!	# 移除元素
(integer) 1
127.0.0.1:6379> scard myset
(integer) 2

```

set 无需不重复集合，随机抽取

```SH
127.0.0.1:6379> SMEMBERS myset
1) "Python"
2) "JAVA"
3) "GO"
4) "PHP"
5) "SHELL"
127.0.0.1:6379> srandmember myset		# 随机抽取一个
"JAVA"
127.0.0.1:6379> srandmember myset
"PHP"
127.0.0.1:6379> srandmember myset 2		# 随机抽取两个
1) "Python"
2) "SHELL"
127.0.0.1:6379> srandmember myset 2
1) "PHP"
2) "JAVA"
```

删除：随机删除key

```SH
127.0.0.1:6379> smembers myset
1) "Python"
2) "PHP"
3) "GO"
4) "JAVA"
5) "SHELL"
127.0.0.1:6379> spop myset			# 随机删除1个元素
"JAVA"
127.0.0.1:6379> smembers myset
1) "Python"
2) "PHP"
3) "GO"
4) "SHELL"
127.0.0.1:6379> spop myset 2		# 随机删除多个元素
1) "GO"
2) "Python"
127.0.0.1:6379> smembers  myset
1) "PHP"
2) "SHELL"

```

将一个指定的值，移动到另外一个set集合！

```sh
127.0.0.1:6379> sadd myset1 "GO"
(integer) 1
127.0.0.1:6379> sadd myset1 "Linux"
(integer) 1
127.0.0.1:6379> sadd myset2 "Python"
(integer) 1
127.0.0.1:6379> sadd myset2 "kubernetes"
(integer) 1
127.0.0.1:6379> smembers myset1
1) "GO"
2) "Linux"
127.0.0.1:6379> smembers myset2
1) "Python"
2) "kubernetes"
127.0.0.1:6379> smove myset1 myset2 "Linux"	 # 移动指定的元素到另一个集合
(integer) 1
127.0.0.1:6379> smove myset2 myset1 "Python"
(integer) 1
127.0.0.1:6379> smembers myset1
1) "Python"
2) "GO"
127.0.0.1:6379> smembers myset2
1) "kubernetes"
2) "Linux"
```

数字集合类

+ 并集、交集、差集

```SH
127.0.0.1:6379> sadd myset1 "tom"
(integer) 1
127.0.0.1:6379> sadd myset1 "alias"
(integer) 1
127.0.0.1:6379> sadd myset2 "jack"
(integer) 1
127.0.0.1:6379> sadd myset2 "tom"
(integer) 1
127.0.0.1:6379> smembers myset1
1) "alias"
2) "tom"
127.0.0.1:6379> smembers myset2
1) "tom"
2) "jack"

# 差集
127.0.0.1:6379> sdiff myset1 myset2
1) "alias"

# 交集
127.0.0.1:6379> sinter myset1 myset2
1) "tom"

# 并集
127.0.0.1:6379> sunion myset1 myset2
1) "tom"
2) "alias"
3) "jack"


```



#### :tangerine:Hash集合

---

Map集合，key-map! 时候这个值是一个map集合，本质和String类型没有太大的区别，还是一个简单的key - value

```SH
127.0.0.1:6379> hset myhash field1 redis	# 存值
(integer) 1	
127.0.0.1:6379> hget myhash field1			# 取值
"redis"

127.0.0.1:6379> hmset myhash field1 "hello" field2 "world"	# 存多个值
OK
127.0.0.1:6379> hget myhash field1
"hello"
127.0.0.1:6379> hget myhash field2
"world"
127.0.0.1:6379> hmget myhash field1 field2	# 获取多个值
1) "hello"
2) "world"
127.0.0.1:6379> hgetall myhash		# 获取所有的数据
1) "field1"
2) "hello"
5) "field2"
6) "world"
```

删除一个值

```sh
127.0.0.1:6379> hdel myhash field1	# 删除 hash 指定的 key
(integer) 1
127.0.0.1:6379> hgetall myhash
1) "field2"
2) "world"
```

长度：获取键值对数量

```SH
127.0.0.1:6379> hlen myhash
(integer) 1
```

判断hash指定key是否存在

```sh
127.0.0.1:6379> hexists myhash key2
(integer) 1
```

只获取key或value

```SH
127.0.0.1:6379> hkeys myhash
1) "field2"
2) "key1"
3) "key2"
4) "key3"
127.0.0.1:6379> hvals myhash
1) "world"
2) "1"
3) "2"
4) "3"
```

自增、自减

```SH
# 自增
127.0.0.1:6379> hvals myhash
1) "world"
2) "1"
3) "2"
4) "3"
127.0.0.1:6379> hincrby myhash key3 1
(integer) 4
127.0.0.1:6379> hincrby myhash key3 1
(integer) 5
127.0.0.1:6379> hvals myhash
1) "world"
2) "1"
3) "2"
4) "5"
# 自减
127.0.0.1:6379> hincrby myhash key3 -1
(integer) 4
```

使用：hash变更的数据（user、name、age）；用户信息的保存之类，或者经常变动的信息；

+ hash：更适合对象的存储
+ string：合适字符串



#### :tangerine:Zset(有序集合)

---

在 set 的基础上，增加了一个值，set k1 v1； zset k1 score v1

排序的作用

```sh
127.0.0.1:6379> zadd myset 1 one
(integer) 1
127.0.0.1:6379> zadd myset 2 two 3 three
(integer) 2
127.0.0.1:6379> zrange myset 0 -1
1) "one"
2) "two"
3) "three"
```

排序：

```sh
127.0.0.1:6379> zadd salary 2500 tom
(integer) 1
127.0.0.1:6379> zadd salary 200 alias
(integer) 1
127.0.0.1:6379> zadd salary 3000 jerry
(integer) 1
127.0.0.1:6379> zrange salary  0 -1
1) "alias"
2) "tom"
3) "jerry"
127.0.0.1:6379> zrangebyscore salary -inf +inf
1) "alias"
2) "tom"
3) "jerry"
127.0.0.1:6379> zrangebyscore salary -inf +inf withscores
1) "alias"
2) "200"
3) "tom"
4) "2500"
5) "jerry"
6) "3000"

```

移除：

```sh
1) "alias"
2) "tom"
3) "jerry"
127.0.0.1:6379> zrem salary alias	# 移除指定元素
(integer) 1
127.0.0.1:6379> zrange salary 0 -1
1) "tom"
2) "jerry"
```

集合中的个数

```
127.0.0.1:6379> zcard salary
(integer) 2
```

获取指定区间的数量：zcount

用途：排行































