# HBase架构及基本组件

![](/assets/importhbs.png)

Hbase基本组件说明：

Client

包含访问HBase的接口，并维护cache来加快对HBase的访问，比如region的位置信息

Master

为Region server分配region

负责Region server的负载均衡

发现失效的Region server并重新分配其上的region

管理用户对table的增删改查操作

Region Server

Regionserver维护region，处理对这些region的IO请求

Regionserver负责切分在运行过程中变得过大的region

Zookeeper作用

通过选举，保证任何时候，集群中只有一个master，Master与RegionServers 启动时会向ZooKeeper注册

存贮所有Region的寻址入口

实时监控Region server的上线和下线信息。并实时通知给Master

存储HBase的schema和table元数据

默认情况下，HBase 管理ZooKeeper 实例，比如， 启动或者停止ZooKeeper

Zookeeper的引入使得Master不再是单点故障

![](/assets/importhz.png)

![](/assets/importhl.png)

