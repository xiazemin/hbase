# 安装zookeeper

![](/assets/importzkp.png)

$ vi conf/zoo.cfg

dataDir=/Users/didi/zookeeper-3.4.6/data

clientPort=2183

$ ./bin/zkServer.sh start

JMX enabled by default

Using config: /Users/didi/zookeeper-3.4.6/zookeeper/bin/../conf/zoo.cfg

Starting zookeeper ... STARTED

$ ./bin/zkCli.sh -server localhost:2183

Connecting to localhost:2183

2017-08-13 12:07:18,883 \[myid:\] - INFO  \[main:Environment@100\] - Client environment:zookeeper.version=3.4.6-1569965, built on 02/20/2014 09:09 GMT

2017-08-13 12:07:18,889 \[myid:\] - INFO  \[main:Environment@100\] - Client environment:host.name=192.168.0.103

2017-08-13 12:07:18,889 \[myid:\] - INFO  \[main:Environment@100\] - Client environment:java.version=1.8.0\_144

Session establishment complete on server localhost/127.0.0.1:2183, sessionid = 0x15dd9c5a2440000, negotiated timeout = 30000

WATCHER::

WatchedEvent state:SyncConnected type:None path:null

\[zk: localhost:2183\(CONNECTED\) 0\]

2、配置conf/hbase-env.sh

就加了一句，不让HBase管理zookeeper

\[java\] view plain copy

export HBASE\_MANAGES\_ZK=false  

默认应该是true，如果你想让HBase来管理zookeeper，那可以设为true。

