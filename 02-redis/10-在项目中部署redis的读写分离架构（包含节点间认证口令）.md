# 知道了这些东西，关键是怎么搭建呢？？？

一主一从，往主节点去写，在从节点去读，可以读到，主从架构就搭建成功了



# 搭建一个新的Slave机器

在slave node上配置：`slaveof 192.168.1.1 6379`，即可

在redis-cli中直接使用`slaveof`命令

# 强制读写分离

基于主从复制架构，实现读写分离

redis slave node只读，默认开启，slave-read-only

开启了只读的redis slave node，会拒绝所有的写操作，这样可以强制搭建成读写分离的架构

# 集群安全认证

master上启用安全认证，`requirepass`设置连接的口令

slave连接口令，`masterauth`



# 读写分离架构的测试

先启动主节点
再启动从节点

主写从读

# 坑

bind

bind 127.0.0.1 -> 本地的开发调试的模式，就只能127.0.0.1本地才能访问到6379的端口

每个redis.conf中的bind 127.0.0.1 -> bind自己的ip地址

开放端口：在每个节点上都: iptables -A INPUT -ptcp --dport  6379 -j ACCEPT

`redis-cli -h ipaddr`
`info replication`