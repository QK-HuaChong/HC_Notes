# Redis

- Redis是一个开源，高级的键值存储和一个适用的解决方案，用于构建高性能，可扩展的Web应用程序。
  
## Redis命令

- 启动Rsdis
  >- redsi-cli

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

## Redis 哈希

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
`LPUSH key value1 [value2]`|将一个或多个值存入列表
`LPOP key`|删除并获取列表中的第一个值
LSET key index value|通过索引在列表中设置元素的值
LRANGE key start stop|获取一定长度的元素
`RPOP key`|删除并获取列表中的最后一个值

## Redis 集合

|命令|描述|
|--|--|
`SADD key member1 [member2..]`|将一个或多个成员添加到集合
`SREM key member1 [member2..]`|从集合中删除一个或多个元素
SCARD key|获取集合中的成员数
SDIFF key1 [key2]|减去多个集合
SINTER key1 [key2]|相交多个集合
SUNION key1 [key2]|添加多个集合

## Redis HyperLogLog

- HyperLogLog是一种使用随机化的算法，以少量内存提供集合中唯一元素数量的近似值。
  
|命令|描述|
|--|--|
PFADD key element [element..]|将指定的元素添加到HyperLogLog中
PFCOUNT key [key..]|返回给定的HyperLogLog的基数估算值
PFMERGE destkey sourcekey [sourcekey..]|将多个HyperLogLog合并为一个新的HyperLogLog
