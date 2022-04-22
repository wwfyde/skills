# Redis数据库

> 官方简介: 一款开源的、基于内存的数据结构(data structure)存储(store)系统, 可以用作数据库(database)、缓存(cache)和消息中间件(message broker).
>
> Redis支持的数据结构: **字符串**(strings)、**哈希**(hashes, 散列)、**列表**(lists)、**集合**(sets)、支持范围查询的**有序集合**(sorted sets with range queries,  zsets), bitmaps, hyperloglogs, 地理空间索引(geospatia indexes), **流**(streams).
>
> Redis内置了 **复制**(replication), **LUA脚本**, **LRU驱动事件**, **事务**(transactions)和 不同级别的**磁盘持久化**(on-disk persistence), 并通过 Redis哨兵(sentry) 和**自动分区**(automatic partitioning)提供高可用性(high availability). 
>
> 
>
> [安装和配置参见](软件使用技巧.md)



## 常见问题

redis删除机制

缓存穿透: 数据不存在时, 去DB中查询, 这个时候 设置默认值

缓存雪崩: 大量缓存失效, 需要到Database中去查询增加了数据库的压力, 解决方案使用队列

redis常用命令



## 最佳实践

- 使用 `scan` 命令实现[大量数据的遍历](https://mp.weixin.qq.com/s?__biz=MzU2Njg3OTU1Mg==&mid=2247484141&idx=1&sn=f391cdd1c4f6a6f5f47c3dd95dfb84e6&utm_source=tuicool&utm_medium=referral)
- 持久化 分布式事务



## Redis特性

- 读写性能优异
- 持久化: 数据保存在磁盘中，重启的时候可以再次加载进行使用。
- 数据类型丰富:key-value类型的数据, 同时还提供list，set，zset，hash等数据结构的存储。
- 单线程/ 多线程
- 数据备份: Redis支持数据的备份，即master-slave模式的数据备份
- 数据自动过期
- 发布订阅
- 分布式
- 不支持事务, Key-Value形式
- 性能极高 – Redis能读的速度是110000次/s,写的速度是81000次/s 。
- 原子 – Redis的所有操作都是原子性的。
- 丰富的特性 – Redis还支持 publish/subscribe, 通知, key 过期等等特性。

## 底层原理

### 主从模式

### 哨兵机制

### 高可用集群

## 说明简介

### 概念定义

Redis 是一个开源、支持网络、基于内存、可选持久性的键值对(key-value)存储数据库

一种内存中的数据结构存储系统，它可以用作数据库、缓存和消息中间件。 

它支持多种类型的数据结构，如 [字符串（strings）](http://www.redis.cn/topics/data-types-intro.html#strings)， [散列（hashes）](http://www.redis.cn/topics/data-types-intro.html#hashes)， [列表（lists）](http://www.redis.cn/topics/data-types-intro.html#lists)， [集合（sets）](http://www.redis.cn/topics/data-types-intro.html#sets)， [有序集合（sorted sets）](http://www.redis.cn/topics/data-types-intro.html#sorted-sets) 与范围查询， [bitmaps](http://www.redis.cn/topics/data-types-intro.html#bitmaps)， [hyperloglogs](http://www.redis.cn/topics/data-types-intro.html#hyperloglogs) 和 [地理空间（geospatial）](http://www.redis.cn/commands/geoadd.html) 索引半径查询。

 Redis 内置了 [复制（replication）](http://www.redis.cn/topics/replication.html)，[LUA脚本（Lua scripting）](http://www.redis.cn/commands/eval.html)， [LRU驱动事件（LRU eviction）](http://www.redis.cn/topics/lru-cache.html)，[事务（transactions）](http://www.redis.cn/topics/transactions.html) 和不同级别的 [磁盘持久化（persistence）](http://www.redis.cn/topics/persistence.html)， 并通过 [Redis哨兵（Sentinel）](http://www.redis.cn/topics/sentinel.html)和自动 [分区（Cluster）](http://www.redis.cn/topics/cluster-tutorial.html)提供高可用性（high availability）。



---

### 特点

高性能的key-value数据库

**Redis支持主从同步**；数据可以从主服务器向任意数量的从服务器上同步，从服务器可以是关联其他从服务器的主服务器。这使得Redis可执行单层树复制。从盘可以有意无意的对数据进行写操作。

当数据依赖不再需要，Redis这种基于内存的性质，与在执行一个事务时将每个变化都写入硬盘的数据库系统相比就显得执行效率非常高。写与读操作速度没有明显差别。

特别适合高并发项目的开发和使用



---

## 数据模型

| 结构类型 | 结构存储的值                                                 | 结构的读写能力                                               |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| String   | 可以是字符串, 整数或者浮点数                                 | 对整个字符串或者字符串的其中一部分执行操作;对整数和浮点数执行自增(increment)或者自减(decrement)  操作 |
| List     | 双向链表, 链表上的每个节点都包含了一个字符串                 | 从链表的两端推入或者弹出元素; 根据偏移量对链表进行修剪(trim);读取单个或者多个元素; 从集合里面随机获取元素 |
| Set      | 包含字符串的无序收集器(unordered collection),并且被包含的每个字符串都是独一无二, 各不相同的 | 添加、获取、移出单个元素；检查一个元素是否存在于集合中；计算交集、并集、差集；从集合里面随机获取元素 |
| Hash     | 包含键值对的无序散列表                                       | 添加、获取、移出单个元素；获取所有键值对                     |
| Zset     | 字符串成员(member)与浮点数分值(score)之间的有序映射,元素的排列顺序由分值的大小决定 | 添加、获取、删除单个元素；根据分值范围（range）或者成员来获取元素 |

## python操作数据库

```python
# 快速使用
import redis

# decode_responses 解决现实打印字符串方式问题
r = redis.Redis(host='localhost', port=6379, db=0, decode_responses=True)


```



```python
# redis


```

# 重要主题

## pub/sub-发布订阅

> 软件架构, 软件设计模式

# 应用场景



## 应用场景


https://segmentfault.com/a/1190000016188385



### 缓存

- 降低数据库压力
- 键过期功能
- 缓存现在几乎是所有中大型网站都在用的必杀技，合理的利用缓存不仅能够提升网站访问速度，还能大大降低数据库的压力。Redis提供了键过期功能，也提供了灵活的键淘汰策略，所以，现在Redis用在缓存的场合非常多。

### 排行榜

- 很多网站都有排行榜应用的，如京东的月度销量榜单、商品按时间的上新排行榜等。Redis提供的有序集合数据类构能实现各种复杂的排行榜应用。

### 计数器

- incr命令
- 什么是计数器，如电商网站商品的浏览量、视频网站视频的播放数等。为了保证数据实时效，每次浏览都得给+1，并发量高时如果每次都请求数据库操作无疑是种挑战和压力。Redis提供的incr命令来实现计数器功能，内存操作，性能非常好，非常适用于这些计数场景。

### 分布式会话

- 集群模式下，在应用不多的情况下一般使用容器自带的session复制功能就能满足，当应用增多相对复杂的系统中，一般都会搭建以Redis等内存数据库为中心的session服务，session不再由容器管理，而是由session服务及内存数据库管理。

### 分布式锁

- 在很多互联网公司中都使用了分布式技术，分布式技术带来的技术挑战是对同一个资源的并发访问，如全局ID、减库存、秒杀等场景，并发量不大的场景可以使用数据库的悲观锁、乐观锁来实现，但在并发量高的场合中，利用数据库锁来控制资源的并发访问是不太理想的，大大影响了数据库的性能。可以利用Redis的setnx功能来编写分布式的锁，如果设置返回1说明获取锁成功，否则获取锁失败，实际应用中要考虑的细节要更多。

### 社交网络

- 点赞、踩、关注/被关注、共同好友等是社交网站的基本功能，社交网站的访问量通常来说比较大，而且传统的关系数据库类型不适合存储这种类型的数据，Redis提供的哈希、集合等数据结构能很方便的的实现这些功能。

### 最新列表

- Redis列表结构，LPUSH可以在列表头部插入一个内容ID作为关键字，LTRIM可用来限制列表的数量，这样列表永远为N个ID，无需查询最新的列表，直接根据ID去到对应的内容页即可。

### 消息系统

- 消息队列是大型网站必用中间件，如ActiveMQ、RabbitMQ、Kafka等流行的消息队列中间件，主要用于业务解耦、流量削峰及异步处理实时性低的业务。Redis提供了发布/订阅及阻塞队列功能，能实现一个简单的消息队列系统。另外，这个不能和专业的消息中间件相比。

## 用作数据库





## 用作消息队列





## 用作缓存



### 缓存更新策略

> [参考文档](https://coolshell.cn/articles/17416.html)
>
> 核心思路是以最新的数据为准, 一旦有新的数据就让缓存失效