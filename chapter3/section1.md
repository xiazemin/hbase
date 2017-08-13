# 配置



ERROR: The node /hbase is not in ZooKeeper. It should have been written by the master. Check the value configured in 'zookeeper.znode.parent'. There could be a mismatch with the one configured in the master.  

解决方法：

在hbase-site.xml文件中添加如下配置：

&lt;property&gt;  

    &lt;name&gt;zookeeper.znode.parent&lt;/name&gt;  

    &lt;value&gt;/hbase&lt;/value&gt;  

&lt;/property&gt;  

$ ./bin/start-hbase.sh

starting master, logging to /Users/didi/hbase/hbase/bin/../logs/hbase-didi-master-192.168.0.103.out

$ ./bin/hbase shell

SLF4J: Class path contains multiple SLF4J bindings.

SLF4J: Found binding in \[jar:file:/Users/didi/hbase/hbase/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class\]

SLF4J: Found binding in \[jar:file:/Users/didi/hadoop/hadoop/share/hadoop/common/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class\]

SLF4J: See http://www.slf4j.org/codes.html\#multiple\_bindings for an explanation.

SLF4J: Actual binding is of type \[org.slf4j.impl.Log4jLoggerFactory\]

2017-08-13 13:40:42,458 WARN  \[main\] util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable

HBase Shell; enter 'help&lt;RETURN&gt;' for list of supported commands.

Type "exit&lt;RETURN&gt;" to leave the HBase Shell

Version 1.1.11, rbc73820af4c8e8e056f7e6e4f42af7ce3c6905c6, Sat Jun 10 18:18:50 PDT 2017



hbase\(main\):001:0&gt;

hbase\(main\):002:0\* list

TABLE

0 row\(s\) in 0.2160 seconds



=&gt; \[\]



