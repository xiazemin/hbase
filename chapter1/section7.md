# 安装hbase

axel  -n 20 [http://apache.fayea.com/hbase/1.1.11/hbase-1.1.11-bin.tar.gz](http://apache.fayea.com/hbase/1.1.11/hbase-1.1.11-bin.tar.gz)

$ ls

CHANGES.txt    LICENSE.txt    README.txt    conf        hbase-webapps

LEGAL        NOTICE.txt    bin        docs        lib

$ vi .bashrc

export HBASE\_HOME=/Users/didi/hbase/hbase

export PATH=$HBASE\_HOME/bin:$PATH

$ echo $JAVA\_HOME

/Library/Java/JavaVirtualMachines/jdk1.8.0\_144.jdk/Contents/Home/

$    vi conf/hbase-env.sh

export JAVA\_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0\_144.jdk/Contents/Home/

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

&lt;value&gt;master,slave&lt;/value&gt;
```

&lt;/property&gt;

&lt;property&gt;

```
&lt;name&gt;hbase.zookeeper.property.dataDir&lt;/name&gt;

&lt;value&gt;/Users/didi/zookeeper/server1/data&lt;/value&gt;
```

&lt;/property&gt;

&lt;/configuration&gt;

查看zookeeper配置

$vi /Users/didi/zookeeper/server1/zookeeper-3.4.6/conf/zoo.cfg

dataDir=/Users/didi/zookeeper/server1/data

$ ./bin/start-hbase.sh

starting master, logging to /Users/didi/hbase/hbase/bin/../logs/hbase-didi-master-192.168.0.103.out

Java HotSpot\(TM\) 64-Bit Server VM warning: ignoring option PermSize=128m; support was removed in 8.0

Java HotSpot\(TM\) 64-Bit Server VM warning: ignoring option MaxPermSize=128m; support was removed in 8.0

