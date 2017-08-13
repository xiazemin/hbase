# 无法启动zk

$ tail -f /Users/didi/hbase/hbase/bin/../logs/hbase-didi-master-192.168.0.103.out

Java HotSpot\(TM\) 64-Bit Server VM warning: ignoring option PermSize=128m; support was removed in 8.0

Java HotSpot\(TM\) 64-Bit Server VM warning: ignoring option MaxPermSize=128m; support was removed in 8.0

Could not start ZK with 2 ZK servers in local mode deployment. Aborting as clients \(e.g. shell\) will not be able to find this ZK quorum.

$ vi conf/hbase-site.xml

  &lt;property&gt;

    &lt;name&gt;hbase.cluster.distributed&lt;/name&gt;

    &lt;value&gt;false&lt;/value&gt;

  &lt;/property&gt;

  &lt;property&gt;

    &lt;name&gt;hbase.zookeeper.quorum&lt;/name&gt;

    &lt;value&gt;master&lt;/value&gt;

  &lt;/property&gt;

$ ./bin/hbase shell

SLF4J: Class path contains multiple SLF4J bindings.

SLF4J: Found binding in \[jar:file:/Users/didi/hbase/hbase/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class\]

SLF4J: Found binding in \[jar:file:/Users/didi/hadoop/hadoop/share/hadoop/common/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class\]

SLF4J: See http://www.slf4j.org/codes.html\#multiple\_bindings for an explanation.

SLF4J: Actual binding is of type \[org.slf4j.impl.Log4jLoggerFactory\]

2017-08-13 11:26:43,965 WARN  \[main\] util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable

2017-08-13 11:27:16,568 ERROR \[main\] zookeeper.RecoverableZooKeeper: ZooKeeper exists failed after 4 attempts

2017-08-13 11:27:16,571 WARN  \[main\] zookeeper.ZKUtil: hconnection-0x533116810x0, quorum=master:2181, baseZNode=/hbase Unable to set watcher on znode \(/hbase/hbaseid\)

HBase Shell; enter 'help&lt;RETURN&gt;' for list of supported commands.

Type "exit&lt;RETURN&gt;" to leave the HBase Shell

Version 1.1.11, rbc73820af4c8e8e056f7e6e4f42af7ce3c6905c6, Sat Jun 10 18:18:50 PDT 2017



hbase\(main\):001:0&gt;





