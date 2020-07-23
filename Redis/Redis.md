### Redis



#### 1.Redis命令

##### 	1.1 启动

```bash
# 启动redis服务端
$ redis-cli
```



##### 	1.2 报错

```bash
# (error) MISCONF Redis is configured to save RDB snapshots, but it is currently not able to persist on disk. Commands that may modify the data set are disabled, because this instance is configured to report errors during writes if RDB snapshotting fails (stop-writes-on-bgsave-error option). Please check the Redis logs for details about the RDB error.  

# 解决方法
# 命令行修改:
127.0.0.1:6379> config set stop-writes-on-bgsave-error no
```



##### 	1.3 切换数据库

```bash
# 切换数据库(默认16个数据库)
$ select [0-15]

# 查看db大小
$ dbsize
```



##### 	1.4 查看所有Key

```bash
127.0.0.1:6379[3]> keys *
```



##### 	1.5 清空数据库

```bash
# 清空当前数据库
flushdb

# 清空全部数据库
flushall
```



> ```bash
> Redis是单线程的
> ```



#### 2.Redis 键（key）

##### 	2.1keys命令

```bash
# 查看key是否存在
exists [key]

# 查看所有key
keys *

# 移动key到某个db
move [key] [db]

# 删除key
DEL key

# 设置过期时间
EXPIRE [key] [seconds]
setex
```



#### 3.Redis 字符串（String）

```bash
# 设置Key值
set key value

# 获取key值
get [key]

# 追加到key原来值末尾(key已存在,如果不存在就设置)
append [key] value

# 返回key字符串值得长度
strlen [key]

# key数字值增一
incr [key]

# key数字值减一
decr [key]

# 返回key字符串值得子字符
getrange [key] [start] [end]

# 不存在,则设置key值
setnx [key] [value]

# 同时设置一个或多个 key-value 对
mset key value

# 同时设置一个或多个 key-value 对，当且仅当所有给定 key 都不存在
msetnx key value
```



#### 4. Redis 哈希（Hash）

```bash
# 将哈希表中key字段field的值设为value
hset [key] field value

# 同时set 多个field-value
hmset key field1 value1 [field2 value2]

# 获取所有值
hvals key

# 获取在哈希表中指定 key 的所有字段和值
hgetall key

# 删除一个或多个字段
hdel key field1 [field2]

# 查看指定key的字段是否存在
hexists key field

# 获取字段数量
hlen key

# 获取所有哈希表中的字段
hkeys key

# 为哈希表 key 中的指定字段的整数值加上增量 increment 。
hincrby key field increment
```



#### 5. Zset(有序集合)

```bash
# 添加一个或多个值
zadd myset 1 one

# 通过字典区间返回有序集合的成员
ZRANGEBYLEX key min max

# 通过分数返回有序集合指定区间内的成员
ZRANGEBYSCORE key min max [WITHSCORES] [LIMIT]
```



#### 6. 三种特殊数据类型

##### 	6.1 Geospatial 地理位置

```bash
# 添加地理位置（纬度，经度，名称）
GEOADD key longitude latitude member [longitude latitude member ...]

# 返回由排序集表示的地理空间索引中两个成员之间的距离
GEODIST key member1 member2 [m|km|ft|mi]

# 返回有效的Geohash字符串，该字符串表示一个或多个元素在代表地理空间索引（其中使用GEOADD添加元素）的排序集合值中的位置。
127.0.0.1:6379> geohash china:city beijing
1) "we6z88pfk80"

# 返回由key的排序集表示的地理空间索引的所有指定成员的位置（经度，纬度）
GEOPOS key member [member ...]

# 使用GEOADD返回填充了地理空间信息的排序集中的成员，这些成员位于以中心位置和距中心的最大距离（半径）指定的区域的边界内
# 以113 23 这个经纬度为中心，寻找方圆500km以内的城市
GEORADIUS china:city 113 23 500 km withcoord withdist 

# 与GEORADIUS命令一样，但该查询已存在于由排序集表示的地理空间索引中的成员的名称
GEORADIUSBYMEMBER
```



##### 	6.2 Hyperloglog

```bash
# 将所有元素参数添加到以指定为第一个参数的变量名称存储的HyperLogLog数据结构中
pfadd mykey a b c d e f g

# 将多个HyperLogLog值合并为一个唯一值，该值将近似于观察到的源HyperLogLog结构的集合的并集的基数
# 合并两组mykey mykey2 => mykey3 并集
pfmerge mykey3 mykey mykey2

# 统计mykey 元素的基数数量
pfcount mykey
```



##### 	6.3 Bitmaps

> 位存储

统计用户信息



```bash
# 设置或清除key处存储的字符串值中offset处的位
SETBIT key offset value

# 返回key处存储的字符串值中offset处的位值
GETBIT key offset

# 统计
BITCOUNT key [start end]
```



#### 7. 事务

> Redis单条命令式保存原子性的，但是事务不保证原子性

Reids事务本质：一组命令的集合！一个事务的所有命令都会被序列化，在事务执行过程中，会按照顺序执行！

一次性、顺序性、排他性

```baSH
------- 队列 set set set 执行 -------
```



> Redis事务不存在隔离级别的概念

**Redis事务：**

* 开启事务(multi)
* 命令入队(……)
* 执行事务(exec)

> 正常执行事务

```bash
# 开启事务
127.0.0.1:6379> multi	
OK

# 命令入队
127.0.0.1:6379> set k1 v1
QUEUED
127.0.0.1:6379> set k2 v2
QUEUED
127.0.0.1:6379> get k2
QUEUED
127.0.0.1:6379> set k3 v3
QUEUED

# 执行事务
127.0.0.1:6379> exec
1) OK
2) OK
3) "v2"
4) OK
```

> 放弃事务

```bash
# 放弃事务
# 放弃后队列中的命令不会被执行
discard
```

> 编译型异常（代码有问题，命令有错），事务中所有命令都不会被执行



> 运行时异常（1/10），如果事务队列中存在语法性，那么执行命令的时候，其他命令是可以正常执行的，错误命令抛出异常

