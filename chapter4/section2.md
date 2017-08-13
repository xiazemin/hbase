# section2

错误：

Sun Aug 13 15:16:47 CST 2017, RpcRetryingCaller{globalStartTime=1502607482193, pause=100, retries=35}, org.apache.hadoop.hbase.MasterNotRunningException: org.apache.hadoop.hbase.MasterNotRunningException: Can't get connection to ZooKeeper: KeeperErrorCode = ConnectionLoss for /hbase

```
at org.apache.hadoop.hbase.client.RpcRetryingCaller.callWithRetries\(RpcRetryingCaller.java:157\)
```

添加



con.set\("hbase.zookeeper.quorum", "localhost"\);

con.set\("hbase.zookeeper.property.clientPort", "2183"\);

成功

Configuration: core-default.xml, core-site.xml, hbase-default.xml, hbase-site.xml

Configuration: core-default.xml, core-site.xml, mapred-default.xml, mapred-site.xml, yarn-default.xml, yarn-site.xml, hdfs-default.xml, hdfs-site.xml, hbase-default.xml, hbase-site.xml

org.apache.hadoop.hbase.client.HBaseAdmin@6a192cfe

Table created

