# mysql-索引优化



自测工具

关键字

 key 、primary key 、unique key 与index区别



SET OPTIMIZER_TRACE_MAX_MEM_SIZE=268435456; 

SET optimizer_trace="enabled=on";



## 概念明晰

## 聚簇索引

> 索引指针直接指向数据页，按索引键值对数据物理页进行物理组织排序，它保存着每行数据。

聚簇索引的选择

1. 有主键时，根据主键创建聚簇索引
2. 没有主键时，会用一个唯一且不为空的索引列做为主键，成为此表的聚簇索引
3. 如果以上两个都不满足那innodb自己创建一个虚拟的聚集索引（大小为6Byte）



特征

 索引叶节点直接关联数据页。



对于聚簇索引的存储引擎，数据的物理存放顺序与索引顺序是一致的，即：只要索引是相邻的，那么对应的数据一定也是相邻地存放在磁盘上的，如果主键不是自增id，不断地调整数据的物理地址、分页，当然也有其他一些措施来减少这些操作，但却无法彻底避免。但，如果是自增的，那就简单了，它只需要一页一页地写，索引结构相对紧凑，磁盘碎片少，效率也高。

## 二级索引 

> 也叫辅助索引，索引叶节点存储的是聚簇索引key，查询时，先通过二级索引定位到聚簇索引，再通过聚簇索引查询到具体行数据



## 覆盖索引

> 指一个查询语句的执行只需要从辅助索引中就可以得到查询记录，而不需要查询聚集索引(行数据)中的记录。也可以称之为实现了索引覆盖



## 联合索引

>

最左前缀原则







[高性能MySQL》读后感——聚簇索引](https://www.jianshu.com/p/54c6d5db4fe6)









