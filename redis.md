
## Redis初识

### Redis是什么？

**特点**

- 开源
- 多种数据结构
- 基于键值对的存储服务系统
- 多种数据结构
- 高性能、功能丰富

**哪些公司在使用Redis**

- GitHub
- Twitter
- stackoverflow
- alibaba
- baidu
- weibo
- bilibili
...

**特性**

- 速度快
- 持久化
- 多种数据结构
- 支持多种编辑语言
- 功能丰富
- 简单
- 主从复制
- 高可用、分布式

**Redis特性-速度快**

- 存储在内存中
![图 1](images/82029e1104a5297c8a7199ffaca1bf9c08a8f2c9ea026ec37d44764773368cf2.png)  
![图 2](images/366bc18ee3a6c163a08072be9606e1d66001f5413106693378ce836ff8d188a1.png)  
- 使用C语言开发的
- 线程模型：单线程

**Redis特性-持久化（断电不丢数据）**

- Redis所有数据保持在内存中，对数据的更新将异步地保存在磁盘上。

**Redis特性-多种数据结构**

主要5种数据结构：

- 字符串
- Hash
- 链表
- 集合
- 有序集合

还有数据结构

- BitMaps：位图
- HyperLogLog：超小内存唯一值计数
- GEO：地图信息定位

**Redis特性-支持多种客户端语言**

- java
- php
- python
- ruby
- go
- lua
- node
...

**Redis特性-功能丰富**

- 发布订阅
- Lua脚本
- 事务
- pipeline

**Redis特性-“简单”**

- 不依赖外部库（like libevent）
- 单线程模型

**Redis-主从复制**

![图 3](images/65ba32df5f76452bba2523c740a8fd04c40bb08ffa7296c105fb52beda5d7027.png)  

**Redis-高可用、分布式**

- 高可用（redis-sentinel v2.8版本）
- 分布式（redis-Cluster v3.0版本）

**Redis典型应用功能**

- 缓存系统
- 计数器
- 消息队列系统
- 排行榜
- 社交网络
- 实时系统

### Redis安装



**Redis可执行文件说明**

- redis-server -》Redis服务器
- redis-cli -》Redis命令行客户端
- redis-benchmark -》Redis性能测试工具
- redis-check-aof -》AOF文件修复工具
- redis-check-dump -》 ROB文件检测工具
- redis-sentinel -》 Sentinel 服务器（2.8以后）

**Redis启动**

三种启动方式

- 最简启动
  - redis-server
- 动态参数启动
  - redis-server --port 6380
- 配置文件启动
  - redis-server configPath

区别：

- 生产环境选择配置启动
- 单机多实例配置文件可以用端口区别分开


**Redis客户端连接**

```shell
redis-cli -h ipaddress -p 6379
```

**Redis客户端返回值**

- 状态回复
- 错误回复
- 整数回复
- 字符串回复
- 多行字符串回复

**Redis常用配置**

- `daemonize`：是否是守护进程（no｜yes）（推荐yes）
- `port`：Redis对外端口号
- `logfile`：Redis系统日志
- `dir`：Redis工作目录；日志文件、持久化文件旧存储在这个目录中

> redis的默认端口是：`6379`

## Redis API的使用和理解

### 通用命令

- keys
- dbsize
- exists key
- del key [key ...]
- expire key seconds
- type key

**keys**

- `keys *`：遍历所有key
- `keys [pattern]`：可以加通配符
  - keys ke*
  - keys he[h-l]
  - keys ph?

> keys 命令一般不在生产环境中使用o(n)
> 那keys*怎么用呢？
> - 热备从节点
> - scan

**dbsize**

- `dbsize` 算出key的总数o(1)
- redis将这个指令做了优化
- 可以经常使用

**exists**

- `exists key` 检查key是否存在
- 0 是不存在；1 是存在

**del**

- `del key` 删除指令key-value
- 可以删除多个

**expire、ttl、persist**

- `expire key seconds` 过期时间 - 设置key在seconds秒后过期
- `ttl key` 查看key剩余的过期时间
- `persist key` 去掉key的过期时间

**type**

- `type key` 返回key的类型，会有以下返回的类型
- string
- hash
- list
- set
- zset
- none

**时间复杂度**

| 命令 | 时间复杂度 |
| keys | O(n) |
| dbsize | O(1) |
| del | O(1) |
| exists | O(1) |
| expire | O(1) |
| type | O(1) |


### 字符串类型

### 哈希类型

### 列表类型

### 集合类型

### 有序集合类型

