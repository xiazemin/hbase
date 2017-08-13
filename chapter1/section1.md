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

该机制用于数据的容错和恢复：



每个HRegionServer中都有一个HLog对象，HLog是一个实现Write Ahead Log的类，在每次用户操作写入MemStore的同时，也会写一份数据到HLog文件中（HLog文件格式见后续），HLog文件定期会滚动出新的，并删除旧的文件（已持久化到StoreFile中的数据）。当HRegionServer意外终止后，HMaster会通过Zookeeper感知到，HMaster首先会处理遗留的 HLog文件，将其中不同Region的Log数据进行拆分，分别放到相应region的目录下，然后再将失效的region重新分配，领取 到这些region的HRegionServer在Load Region的过程中，会发现有历史HLog需要处理，因此会Replay HLog中的数据到MemStore中，然后flush到StoreFiles，完成数据恢复

