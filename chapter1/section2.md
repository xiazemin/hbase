# HBase容错性

Master容错：Zookeeper重新选择一个新的Master

无Master过程中，数据读取仍照常进行；

无master过程中，region切分、负载均衡等无法进行；

RegionServer容错：定时向Zookeeper汇报心跳，如果一旦时间内未出现心跳，Master将该RegionServer上的Region重新分配到其他RegionServer上，失效服务器上“预写”日志由主服务器进行分割并派送给新的RegionServer

Zookeeper容错：Zookeeper是一个可靠地服务，一般配置3或5个Zookeeper实例

Region定位流程：

![](/assets/importhso.png)

寻找RegionServer

ZooKeeper--&gt; -ROOT-\(单Region\)--&gt; .META.--&gt; 用户表

-ROOT-

表包含.META.表所在的region列表，该表只会有一个Region；

Zookeeper中记录了-ROOT-表的location。

.META.

表包含所有的用户空间region列表，以及RegionServer的服务器地址。

Hbase使用场景

storing large amounts  of data\(100s of TBs\)

need high write throughput

need efficient random access\(key lookups\) within large data sets

need to scale gracefully with data

for structured and semi-structured data

don't need fullRDMS capabilities\(cross row/cross table transaction, joins,etc.\)

大数据量存储，大数据量高并发操作

需要对数据随机读写操作

读写访问均是非常简单的操作

Hbase与HDFS对比

两者都具有良好的容错性和扩展性，都可以扩展到成百上千个节点；

HDFS适合批处理场景

不支持数据随机查找

不适合增量数据处理

不支持数据更新

![](/assets/importhdd.png)

