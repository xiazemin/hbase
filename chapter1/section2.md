# HBase容错性



Master容错：Zookeeper重新选择一个新的Master

无Master过程中，数据读取仍照常进行；

无master过程中，region切分、负载均衡等无法进行；

RegionServer容错：定时向Zookeeper汇报心跳，如果一旦时间内未出现心跳，Master将该RegionServer上的Region重新分配到其他RegionServer上，失效服务器上“预写”日志由主服务器进行分割并派送给新的RegionServer

Zookeeper容错：Zookeeper是一个可靠地服务，一般配置3或5个Zookeeper实例

Region定位流程：

