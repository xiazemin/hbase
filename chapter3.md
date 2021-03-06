# HBASE 配置ZOOKEEPER

$ vi conf/hbase-site.xml

&lt;configuration&gt;

&lt;property&gt;

```
&lt;name&gt;hbase.rootdir&lt;/name&gt;

&lt;value&gt;hdfs://master:8020/hbase&lt;/value&gt;
```

&lt;/property&gt;

&lt;property&gt;

```
&lt;name&gt;hbase.cluster.distributed&lt;/name&gt;

&lt;value&gt;false&lt;/value&gt;
```

&lt;/property&gt;

&lt;property&gt;

```
&lt;name&gt;hbase.zookeeper.quorum&lt;/name&gt;

&lt;value&gt;localhost&lt;/value&gt;
```

&lt;/property&gt;

&lt;property&gt;

```
&lt;name&gt;hbase.zookeeper.property.clientPort&lt;/name&gt;

&lt;value&gt;2183&lt;/value&gt;

&lt;/property&gt;
```

&lt;property&gt;

```
&lt;name&gt;hbase.zookeeper.property.dataDir&lt;/name&gt;

&lt;value&gt;/Users/didi/zookeeper-3.4.6/data&lt;/value&gt;
```

&lt;/property&gt;

&lt;/configuration&gt;

$ ./bin/start-hbase.sh

starting master, logging to /Users/didi/hbase/hbase/bin/../logs/hbase-didi-master-192.168.0.103.out

Java HotSpot\(TM\) 64-Bit Server VM warning: ignoring option PermSize=128m; support was removed in 8.0

Java HotSpot\(TM\) 64-Bit Server VM warning: ignoring option MaxPermSize=128m; support was removed in 8.0

$ ./bin/hbase shell

SLF4J: Class path contains multiple SLF4J bindings

hbase\(main\):001:0&gt; list

TABLE

ERROR: The node /hbase is not in ZooKeeper. It should have been written by the master. Check the value configured in 'zookeeper.znode.parent'. There could be a mismatch with the one configured in the master.

Here is some help for this command:

List all tables in hbase. Optional regular expression parameter could

be used to filter the output. Examples:

hbase&gt; list

hbase&gt; list 'abc.\*'

hbase&gt; list 'ns:abc.\*'

hbase&gt; list 'ns:.\*'

$ vi conf/hbase-site.xml

将

&lt;property&gt;

```
&lt;name&gt;hbase.rootdir&lt;/name&gt;

&lt;value&gt;hdfs://localhost:8020/hbase&lt;/value&gt;
```

&lt;/property&gt;

替换为

&lt;property&gt;

```
&lt;name&gt;hbase.rootdir&lt;/name&gt;

&lt;value&gt;hdfs://master:8020/hbase&lt;/value&gt;
```

&lt;/property&gt;

2017-08-13 12:25:52,574 WARN  \[main\] zookeeper.ZKUtil: hconnection-0x533116810x0, quorum=localost:2183, baseZNode=/hbase Unable to set watcher on znode \(/hbase/hbaseid\)

Could not start ZK at requested port of 2183.  ZK was started at port: 2184.  Aborting as clients \(e.g. shell\) will not be able to find this ZK quorum.

$ ./bin/zkServer.sh  stop

2017-08-13 12:31:51,926 ERROR \[main\] zookeeper.RecoverableZooKeeper: ZooKeeper exists failed after 4 attempts

2017-08-13 12:31:51,927 WARN  \[main\] zookeeper.ZKUtil: hconnection-0x533116810x0, quorum=localost:2183, baseZNode=/hbase Unable to set watcher on znode \(/hbase/hbaseid\)

$ vi conf/hbase-site.xml  将localhost换成master

&lt;property&gt;

```
&lt;name&gt;hbase.zookeeper.quorum&lt;/name&gt;

&lt;value&gt;master&lt;/value&gt;
```

&lt;/property&gt;

2017-08-13 12:39:54,422 ERROR \[main\] zookeeper.RecoverableZooKeeper: ZooKeeper exists failed after 4 attempts

2017-08-13 12:39:54,423 WARN  \[main\] zookeeper.ZKUtil: hconnection-0x533116810x0, quorum=master:2183, baseZNode=/hbase Unable to set watcher on znode \(/hbase/hbaseid\)

