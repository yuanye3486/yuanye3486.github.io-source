---
title: Redis
date: 2018-3-7 11:08:05
tags: [Redis]
categories: [Redis]
---

## 1. Redis 有哪些数据结构？  
  + String(字符串)
    - append
    - set
    - get / mget
    - incr

  + Hash(字典)
    - hset
    - hget
    - hdel
    - hexist
    - hincrby

  + List(列表)
    - lpush / rpush
    - lpop  / rpop
    - blpop / brpop
    -

  + Set(集合)
    - sadd
    - smove ：将 member 元素从 source 集合移动到 destination 集合。[SMOVE source destination member]
    - spop  ：移除并返回集合中的一个随机元素。
    - srem  ：移除集合 key 中的一个或多个 member 元素，不存在的 member 元素会被忽略。[SREM key member [member ...]]
    - smembers：返回集合 key 中的所有成员。[SMEMBERS key]

  + SortedSet(有序集合)
    - zadd
    - zincrby
    - zrem / zremrangebyrank
    - zrange / zrangebyscore

  + HyperLogLog
    - 用于基数统计
    - HyperLogLog 键内存占用仅需 12K，可计算近 2^64 个不同元素的基数。
    - 算法给出的基数并不是精确的，是估算值。

  + Geo

  + Pub/Sub(发布订阅)
    - publish
    - subscribe
    - unsubscribe


## 2. 如何使用 Redis 实现分布式锁？
  + 先用 setnx 来争抢锁，抢到之后，再用 expire 给锁加一个过期时间防止锁忘记了释放。或者直接使用：
  ```
    SET key-with-expire-and-NX "lock" EX 10086 NX
  ```

## 3. 假如 Redis 里面有1亿个 key，其中有 10w 个 key 是以某个固定的已知的前缀开头的，如果将它们全部找出来？
  + 使用 keys 指令可以扫出指定模式的 key 列表。
    - 如果这个 redis 正在给线上的业务提供服务，那使用 keys 指令会有什么问题？
      redis的单线程的。keys指令会导致线程阻塞一段时间，线上服务会停顿，直到指令执行完毕，服务才能恢复。这个时候可以使用scan指令，scan指令可以无阻塞的提取出指定模式的key列表，但是会有一定的重复概率，在客户端做一次去重就可以了，但是整体所花费的时间会比直接用keys指令长。


## 4. 如何使用 Redis 实现异步队列？
  + 一般使用 list 结构作为队列，rpush 生产消息，lpop 消费消息。当 lpop 没有消息的时候，要适当 sleep 一会再重试。
    - 可不可以不用 sleep？
      list 还有个指令叫 blpop，在没有消息的时候，它会阻塞住直到消息到来。
    - 能不能生产一次消费多次呢？
      使用pub/sub主题订阅者模式，可以实现1:N的消息队列。
  + Redis 如何实现延时队列？
    - 使用 sortedset，拿时间戳作为 score，调用 zadd 来生产消息，消费者用 zrangebyscore 指令获取 N 秒之前的数据轮询进行处理。


## 5. 如果有大量的 key 需要设置同一时间过期，一般需要注意什么？
  如果大量的 key 过期时间设置的过于集中，到过期的那个时间点，redis 可能会出现短暂的卡顿现象。一般需要在时间上加一个随机值，使得过期时间分散一些。


## 6. [Redis 如何做持久化？](http://doc.redisfans.com/topic/persistence.html)
  + 使用 BGSAVE 命令做镜像全量持久化。
    - bgsave 的原理是什么？
      命令执行之后立即返回 OK ，然后 Redis fork 出一个新子进程，原来的 Redis 进程(父进程)继续处理客户端请求，而子进程则负责将数据保存到磁盘，然后退出。
  + RDB 持久化可以在指定的时间间隔内生成数据集的时间点快照
  + AOF 持久化记录服务器执行的所有写操作命令，并在服务器启动时，通过重新执行这些命令来还原数据集。
  + Redis 还可以同时使用 AOF 持久化和 RDB 持久化。 在这种情况下， 当 Redis 重启时， 它会优先使用 AOF 文件来还原数据集， 因为 AOF 文件保存的数据集通常比 RDB 文件所保存的数据集更完整。


## 7. Pipeline有什么好处，为什么要用pipeline？
  + 可以将多次 IO 往返的时间缩减为一次，前提是 pipeline 执行的指令之间没有因果相关性。


## 8. [Redis的同步机制了解么？](http://doc.redisfans.com/topic/replication.html#id1)  
  Redis可以使用主从同步，从从同步。第一次同步时，主节点做一次bgsave，并同时将后续修改操作记录到内存buffer，待完成后将rdb文件全量同步到复制节点，复制节点接受完成后将rdb镜像加载到内存。加载完成后，再通知主节点将期间修改的操作记录同步到复制节点进行重放就完成了同步过程。

## 9. Redis 集群原理？
  Redis Sentinal着眼于高可用，在master宕机时会自动将slave提升为master，继续提供服务。
  Redis Cluster着眼于扩展性，在单个redis内存不足时，使用Cluster进行分片存储。


## 10. Redis 常见应用场景
  + 全页面缓存
  + 排行榜
  + Session 存储
  + 队列
  + 发布/订阅
  + 分布式锁

  + 案例
    - [Redis在京东到家的订单中的使用](https://tech.imdada.cn/2017/06/30/daojia-redis/?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)


引用：
  [天下无难试之Redis面试刁难大全](https://mp.weixin.qq.com/s/507jyNbL4xCkxyW6Xk15Xg)
