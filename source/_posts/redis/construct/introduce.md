---
title: Redis介绍，安装，连接。
date: 2017-12-03 23:02:54
tags:
	- redis
	- noSql
categories: redis基础
cover_picture: http://s1.wailian.download/2017/11/30/redis.jpg
---
## 一.什么是redis
### 1.redis介绍
Redis是一个高性能的kv对缓存和内存数据库(存的不像mysql那样的表)
Redis的存储结构就是key-value，形式如下：
![map](http://s1.wailian.download/2017/12/03/redismap.png)
注：redis中的value内部可以支持各种数据结构类型，比如可以存入一个普通的string，还可以存list，set，hashmap，sortedSet（有序的set）

### 2.redis应用场景

> * A、用来做缓存(ehcache/memcached)——redis的所有数据是放在内存中的（内存数据库）
> * B、可以在某些特定应用场景下替代传统数据库——比如社交类的应用
> * C、在一些大型系统中，巧妙地实现一些特定的功能：session共享、购物车只要你有丰富的想象力，redis可以用在各种官网说明上没有提到的场景。。。。。

### 3.redis的特性

> * A、redis数据访问速度快（数据在内存中）
> * B、redis的数据有持久化（持久化机制有两种：1、定期将内存数据dump到磁盘；2、aof持久化机制——用记日志的方式记录每一条数据更新操作，一旦出现灾难事件，可以通过日志重放来恢复整个数据库）
> * C、redis还支持集群模式（容量可以线性扩展）
> * D、redis相比其他缓存工具（ehcach/memcached），有一个鲜明的优势：支持丰富的数据结构

## 二.安装redis

### 1、先去官网（http://redis.io/download ）下载一个源码工程（redis官网版本只支持linux/微软开源事业部维护了一个windows版本）
### 2、把安装包上传到服务器，解压缩
### 3、切换到解压出来的源码工程目录中cd redis-2.6.16 
### 4、用make命令来对redis的c语言源码工程进行编译
### 5、编译完成之后，用make  install命令进行安装
```
make  PREFIX=/usr/local/redis  install
```
安装成功的显示：
![map](http://s1.wailian.download/2017/12/03/redis1.jpg)
进入redis的bin目录：
![map](http://s1.wailian.download/2017/12/03/redis2.jpg)
然后再指定配置文件，启动redis服务：
![map](http://s1.wailian.download/2017/12/03/redis3.jpg)
启动成功的显示：
![map](http://s1.wailian.download/2017/12/03/redis4.jpg)
上述启动方法，会让redis服务进程运行在console前台，最好应该放到后台运行，可将启动命令改为如下方式：

> * 方式一

```
nohup bin/redis-server ./redis.conf 1>/dev/null 2>&1 &
```

> * 方式二

修改配置文件
vi  redis.conf
修改其中一个配置
![map](http://s1.wailian.download/2017/12/03/redis5.png)
保存文件后再用普通命令启动，也可以启动为后台模式

```
bin/redis-server  ./redis.conf
```

## 三.客户端连接

### 1、用redis自带的命令行客户端

```
bin/redis-cli  -h  notrue-centos  -p  6379

redis notrue-centos:6379> ping

PONG

redis notrue-centos:6379>
```

### 2、或者用redis的api客户端连接

新建一个maven工程，导入jedis的maven依赖坐标

```
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.7.2</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
```

然后写一个类用来测试服务器跟客户端的连通性：

```java
public class RedisClientConnectionTest {

public static void main(String[] args) {

        // 构造一个redis的客户端对象

        Jedis jedis = new Jedis("pinshutang.zicp.net", 6379);

         String ping = jedis.ping();

         System.out.println(ping);

        }

}
```