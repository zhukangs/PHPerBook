# 问题与简答

## Redis 篇

### Redis 介绍

Redis 是一个高性能的 key-value 数据库。每秒可执行操作高达 10万+ QPS

### Redis 特点

- 支持数据持久化，可将内存中的数据保存在磁盘，重启时再次加载
- 支持 KV 类型数据，也支持其他丰富的数据结构存储
- 支持数据备份，即 master-slave 模式的数据备份

### Redis 支持哪些数据结构

- STRING：字符串、整数或浮点数

  ```
  set get incr incrby
  ```

- HASH：散列表，存储键值对之间的映射，无序排列。可以将redis中的hash类型看成是，存储多个键值对的容器

  ```
  hset hget hmset hmget hgetall 
  ```

- LIST：列表，可存储多个相同的字符串

  ```
  上进上出：栈，数据先进后出
  下进上出：队列，数据先进先出
  lpush(头部添加) lrange rpush(尾部添加) Itrim lpop(头部删除) 
  ```

- SET：集合，存储不同元素，无序排列

  ```
  sadd smembers sdiff(差集) sinter(交集) sunion(并集) scard 
  ```

- ZSET：有序集合，存储键值对，有序排列

  ```
  zadd zrange zrevrange(按序号降序获取)
  ```


### Redis 与 Memcache 区别

参考一

| 对比项    | Redis     | Memcache      |
| ------ | --------- | ------------- |
| 数据结构   | 丰富数据类型    | 只支持简单 KV 数据类型 |
| 数据一致性  | 事务        | cas           |
| 持久性    | 快照/AOF    | 不支持           |
| 网络IO   | 单线程 IO 复用 | 多线程、非阻塞 IO 复用 |
| 内存管理机制 | 现场申请内存    | 预分配内存         |

参考二

- 数据类型:memcache支持的数据类型就是字符串，redis支持的数据类型有字符串，哈希，链表，集合，有序集合。


- 持久化：memcache数据是存储到内存里面，一旦断电，或重启，则数据丢失。redis数据也是存储到内存里面的，但是可以持久化，周期性的把数据给保存到硬盘里面，导致重启，或断电不会丢失数据。


- 数据量：memcahce一个键存储的数据最大是1M,而redis的一个键值，存储的最大数据量是1G的数据量。

参考三

① 数据存储形式：
都是key/value形式。
② 数据类型：
​​​memcache：string
​​​redis：​  string、hash哈希、list链表、set集合、zset有序集合

​​​链表：把它理解为是一根管子。
​​​​我们可以在头部添加数据 lpush，可以在尾部添加数据。rpush
​​​​也可以在头部删除数据 lpop，也可以在尾部删除数据 rpop。
​​​​
​​​使用链表来模拟队列：先进先出
​​​​从尾部添加数据，从头部删除数据。

​​​使用链表来模拟栈：先进后出
​​​​从头部添加数据，从头部删除数据。​​
​​③ 持久化（本质，把数据从内存存储到硬盘）：
​​​memcache：不支持。
​​​redis：支持。
​​④ 单个value值大小：
​​​memcache：1M
​​​redis：1G

### Redis常用命令

- keys ，返回当前数据库里面的键，*表示所有
- exists，判断一个键是否存在
- del，删除指定的键
- expire，设置键的有效期
- ttl，返回一个键剩余的过期时间
- type，返回数据类型
- select，选择数据库，0-15，默认0
- dbsize，返回当前数据库里面键的个数
- flushdb，情况当前数据库所有的键
- flushall，清空所有数据库的所有键

### 发布订阅

发布订阅(pub/sub)是一种消息通信模式：发送者(pub)发送消息，订阅者(sub)接收消息

### 持久化策略

#### 快照持久化

将某一时刻的所有数据写入硬盘。使用`BGSAVE`命令，随着内存使用量的增加，执行 BGSAVE 可能会导致系统长时间地停顿。默认开启，文件名默认dump.rdb。

缺点：由于快照方式是在一定间隔做一次的，所以如果redis意外down掉的话，就会丢失最后一次快照后的所有修改。

#### AOF 持久化

只追加文件，在执行写命令时，将被执行的写命令复制到硬盘里面。使用 AOF 策略需要对硬盘进行大量写入，Redis 处理速度会受到硬盘性能的限制。配置文件redis.conf，appendonly yes即为开启，文件名如：appendonly.aof。

注意：如果两种持久话方式都开启，则以aof为准。

第1种持久化方式：快照持久化（默认）
​​​特点：把内存中的数据直接备份到文件中。
​​​触发：在一定时间内key被修改了指定次数。
第2种持久化方式：追加方式aof
​​​特点：把对数据的写操作命令直接备份到文件中。
​​​触发：每秒钟把写命令进行备份。
​​​
​​​aof文件重写：对同一个数据进行的多次同类型的写操作，对命令进行了合并。

### Redis 事务

```
redis> MULTI  #标记事务开始
OK
redis> INCR user_id  #多条命令按顺序入队
QUEUED
redis> INCR user_id
QUEUED
redis> INCR user_id
QUEUED
redis> PING
QUEUED
redis> EXEC  #执行
1) (integer) 1
2) (integer) 2
3) (integer) 3
4) PONG
```

> 在 Redis 事务中如果有某一条命令执行失败，其后的命令仍然会被继续执行

> 使用 DISCARD 可以取消事务，放弃执行事务块内的所有命令

### Redis 过期策略及内存淘汰机制

#### 过期策略

Redis 的过期策略就是指当 Redis 中缓存的 Key 过期了，Redis 如何处理

- 定时过期：每个设置过期时间的 Key 创建定时器，到过期时间立即清除。内存友好，CPU 不友好
- 惰性过期：访问 Key 时判断是否过期，过期则清除。CPU 友好，内存不友好
- 定期过期：隔一定时间，expires 字典中扫描一定数量的 Key，清除其中已过期的 Key。内存和 CPU 资源达到最优的平衡效果

#### 内存淘汰机制

```
[root]# redis-cli config get maxmemory-policy
1) "maxmemory-policy"
2) "noeviction"
```

- noeviction：新写入操作会报错
- allkeys-lru：移除最近最少使用的 key
- allkeys-random：随机移除某些 key
- volatile-lru：在设置了过期时间的键中，移除最近最少使用的 key
- volatile-random：在设置了过期时间的键中，随机移除某些 key
- volatile-ttl：在设置了过期时间的键中，有更早过期时间的 key 优先移除

### 为什么 Redis 是单线程的

Redis 是基于内存的操作，CPU 不是 Redis 的瓶颈，Redis 瓶颈最有可能是内存或网络。而且单线程容易实现，避免了不必要的上下文切换和竞争条件，不存在多线程切换消耗 CPU

### 如何利用 CPU 多核心

在单机单实例下，如果操作都是 O(N)、O(log(N)) 复杂度，对 CPU 消耗不会太高。为了最大利用 CPU，单机可以部署多个实例

