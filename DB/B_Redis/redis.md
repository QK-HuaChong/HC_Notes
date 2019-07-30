# Redis

- Redis是一个开源，高级的键值存储和一个适用的解决方案，用于构建高性能，可扩展的Web应用程序。
  
## Redis命令

- 启动Rsdis
  >- redis-cli

- 在远程服务器上运行命令
  >- redis-cli -h host -p port -a password
  
### Redis 键命令

|命令|描述|
|--|--|
`DEL key`|删除指定键
DUMP key|返回存储在指定键的值的序列化版本
EXISTS key|检查键是否存在
EXPIRE key seconds|设置键在指定时间秒数后过期
EXPIREAT key timestamp|指定时间戳后过期
PERSIST key|删除指定键的过期时间
RENAME key newkey|更改键的名字
PTTL key|获取键到期的剩余时间
TYPE key|返回键的类型

## Redis 字符串

|命令|描述|
|--|--|
`SET key value`|指定键的值
`GET key`|获取指定键的值
GETRANGE key start end|获取指定键的值的切片
GETSET key value|设置指定键的值并返回旧值
SETNX key value|设置键的值，仅当键存在时
STRLEN key|获取指定键的值的长度
MGET key1 [key2...]|获取所有指定键的值
MSET key1 value [key2 value...]|为多个键设置他们的值

## Redis 散列

- Redis Hashes是字符串字段和字符串值之间的映射(类似于PHP中的数组类型)。 因此，它们是表示对象的完美数据类型。

|命令|描述|
|--|--|
`HDEL key field [field2]`|删除一个或多个哈希字段
HEXISTS key field|判断是否存在指定的散列字段
HGET key field|获取指定键的哈希值
HGETALL key|获取指定键的哈希中的所有字段和值
HKEYS key|获取哈希中所有的字段
`HSET key field value`|设置散列字段的字符串值
HVALS key|获取哈希中所有的值

## Redis 列表

- Redis列表只是字符串列表，按插入顺序排序。可以在列表的头部或尾部添加Redis列表中的元素。

|命令|描述|
|--|--|
`LPUSH（RPUSH） key value1 [value2]`|将一个或多个值存入列表
`LPOP key`|删除并获取列表中的第一个值
LINDEX key index value|通过索引在列表中设置元素的值
LRANGE key start stop|获取一定长度的元素
`RPOP key`|删除并获取列表中的最后一个值

## Redis 集合

### 无序集合

|命令|描述|
|--|--|
`SADD key member1 [member2..]`|将一个或多个成员添加到集合
`SREM key member1 [member2..]`|从集合中删除一个或多个元素
SCARD key|获取集合中的成员数
SDIFF key1 [key2]|减去多个集合
SINTER key1 [key2]|相交多个集合
SUNION key1 [key2]|添加多个集合
SMERMBERS key|获取指定集合中的所有元素
SISMEMBER key value|检查集合中是否包含该元素

### 有序集合

|命令|描述|
|--|--|
ZADD key score1 member1 [score2 member2]|向有序集合添加一个或多个成员，或者更新已存在成员的分数
ZCARD key|获取有序集合的成员数
ZCOUNT key min max|计算在有序集合中指定区间分数的成员数
ZINCRBY key increment member|有序集合中对指定成员的分数加上增量 increment
ZINTERSTORE destination numkeys key [key ...]|计算给定的一个或多个有序集的交集并将结果集存储在新的有序集合 key 中
ZLEXCOUNT key min max|在有序集合中计算指定字典区间内成员数量
ZRANGE key start stop [WITHSCORES]|通过索引区间返回有序集合成指定区间内的成员
ZRANGEBYLEX key min max [LIMIT offset count]|通过字典区间返回有序集合的成员
ZRANGEBYSCORE key min max [WITHSCORES] [LIMIT]|通过分数返回有序集合指定区间内的成员
ZRANK key member|返回有序集合中指定成员的索引
ZREM key member [member ...]|移除有序集合中的一个或多个成员

## Redis HyperLogLog

- HyperLogLog是一种使用随机化的算法，以少量内存提供集合中唯一元素数量的近似值。
  
|命令|描述|
|--|--|
PFADD key element [element..]|将指定的元素添加到HyperLogLog中
PFCOUNT key [key..]|返回给定的HyperLogLog的基数估算值
PFMERGE destkey sourcekey [sourcekey..]|将多个HyperLogLog合并为一个新的HyperLogLog

## Redis 事务

- Redis事务由命令`MULTI`命令启动，然后需要传递一个应该在事务中执行的命令列表，然后整个事务由`EXEC`命令执行。

- 示例：
  
```redis
redis 127.0.0.1:6379> MULTI
OK
redis 127.0.0.1:6379> SET mykey "redis"
QUEUED
redis 127.0.0.1:6379> GET mykey
QUEUED
redis 127.0.0.1:6379> INCR visitors
QUEUED
redis 127.0.0.1:6379> EXEC  
1) OK
2) "redis"
3) (integer) 1
```

|命令|描述|
|--|--|
DISCARD|丢失在MULTI之后发送的所有命令
EXEC|执行在MUULTI之后发出的所有命令
MULTI|编辑事务块的开始
UNWHATCH|取消WHATCH民航临海对所有key的监视
WHATCH key [key ...]|监视给定的间以确定MULTI/EXEC块的执行

## Redis 连接

|命令|描述|
|--|--|
AUTH password|使用给定的密码验证服务器
ECHO message|打印给定的字符串信息
PING|检查服务器是否在运行
QUIT|关闭当前连接
SELECT index|更改当前连接的所选数据库

## Redis 内存淘汰机制

- 在redis.config中有一行配置：
  
>maxmemory-policy volatile-lru

- noeviction：当内存不足以容纳新写入数据时，新写入操作会报错。应该没人用吧。

- `allkeys-lru`：当内存不足以容纳新写入数据时，在键空间中，移除最近最少使用的key。**推荐使用**，目前项目在用这种。

- allkeys-random：当内存不足以容纳新写入数据时，在键空间中，随机移除某个key。应该也没人用吧，你不删最少使用Key,去随机删。

- volatile-lru：当内存不足以容纳新写入数据时，在设置了过期时间的键空间中，移除最近最少使用的key。这种情况一般是把redis既当缓存，又做持久化存储的时候才用。不推荐

- volatile-random：当内存不足以容纳新写入数据时，在设置了过期时间的键空间中，随机移除某个key。依然不推荐

- volatile-ttl：当内存不足以容纳新写入数据时，在设置了过期时间的键空间中，有更早过期时间的key优先移除。不推荐

## 单独

## 相关链接

[Redis入门教程](https://blog.csdn.net/weixin_40753536/article/details/80109251)
