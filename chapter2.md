# hbase-site.xml配置



#### hbase.tmp.dir

* 本地文件系统tmp目录，一般配置成local模式的设置一下，但是最好还是需要设置一下，因为很多文件都会默认设置成它下面的
* 线上配置
  | `<property><name>hbase.tmp.dir</name><value>/mnt/dfs/11/hbase/hbase-tmp</value></property>` |
  | :--- |
* 默认值：
  | `${java.io.tmpdir}/hbase-${user.name}` |
  | :--- |


  写到系统的/tmp目录

#### hbase.rootdir

* HBase集群中所有RegionServer共享目录，用来持久化HBase的数据，一般设置的是hdfs的文件目录，如hdfs://namenode.
  [example.org:9000/hbase](http://example.org:9000/hbase)
* 线上配置
  | `<property><name>hbase.rootdir</name><value>hdfs://mycluster/hbase</value></property>` |
  | :--- |
* 默认值：
  | `${hbase.tmp.dir}/hbase` |
  | :--- |

#### hbase.cluster.distributed

* 集群的模式，分布式还是单机模式，如果设置成false的话，HBase进程和Zookeeper进程在同一个JVM进程。
* 线上配置为true
* 默认值：false

#### hbase.zookeeper.quorum

* zookeeper集群的URL配置，多个host中间用逗号（,）分割
* 线上配置
  | `<property><name>hbase.zookeeper.quorum</name><value>inspurXXX.xxx.xxx.org,inspurXXX.xxx.xxx.org,inspurXXX.xxx.xxx.org,inspurXXX.xxx.xxx.org,`[`inspurXXX.xxx.xxx.org`](http://inspurxxx.photo.163.org/)`</value></property>` |
  | :--- |
* 默认值：localhost

#### hbase.zookeeper.property.dataDir

* ZooKeeper的zoo.conf中的配置。 快照的存储位置
* 线上配置：/home/hadoop/zookeeperData
* 默认值：${hbase.tmp.dir}/zookeeper

#### zookeeper.session.timeout

* 客户端与zk连接超时时间
* 线上配置：1200000（20min）
* 默认值：180000（3min）

#### hbase.zookeeper.property.tickTime

* Client端与zk发送心跳的时间间隔
* 线上配置：6000（6s）
* 默认值：6000

#### hbase.security.authentication

* HBase集群安全认证机制，目前的版本只支持kerberos安全认证。
* 线上配置：kerberos
* 默认值：空

#### hbase.security.authorization

* HBase是否开启安全授权机制
* 线上配置： true
* 默认值： false

#### hbase.regionserver.kerberos.principal

* regionserver的kerberos认证的主体名称（由三部分组成：服务或用户名称、实例名称以及域名）
* 线上配置：hbase/\_HOST@HADOOP.
  [xxx.xxx.COM](http://hz.netease.com/)
* 默认：无

#### hbase.regionserver.keytab.file

* regionserver keytab文件路径
* 线上配置：/home/hadoop/etc/conf/hbase.keytab
* 默认值：无

#### hbase.master.kerberos.principal

* master的kerberos认证的主体名称（由三部分组成：服务或用户名称、实例名称以及域名）
* 线上配置：hbase/\_HOST@HADOOP.
  [xxx.xxx.COM](http://hz.netease.com/)
* 默认：无

#### hbase.master.keytab.file

* master keytab文件路径
* 线上配置：/home/hadoop/etc/conf/hbase.keytab
* 默认值：无

#### hbase.regionserver.handler.count

* regionserver处理IO请求的线程数
* 线上配置：50
* 默认配置：10

#### hbase.regionserver.global.memstore.upperLimit

* RegionServer进程block进行flush触发条件：该节点上所有region的memstore之和达到upperLimit\*heapsize
* 线上配置：0.45
* 默认配置：0.4

#### hbase.regionserver.global.memstore.lowerLimit

* RegionServer进程触发flush的一个条件：该节点上所有region的memstore之和达到lowerLimit\*heapsize
* 线上配置：0.4
* 默认配置：0.35

#### hbase.client.write.buffer

* 客户端写buffer，设置autoFlush为false时，当客户端写满buffer才flush
* 线上配置：8388608（8M）
* 默认配置：2097152（2M）

#### hbase.hregion.max.filesize

* 单个ColumnFamily的region大小，若按照ConstantSizeRegionSplitPolicy策略，超过设置的该值则自动split
* 线上配置：107374182400（100G）
* 默认配置：21474836480（20G）

#### hbase.hregion.memstore.block.multiplier

* 超过memstore大小的倍数达到该值则block所有写入请求，自我保护
* 线上配置：8（内存够大可以适当调大一些，出现这种情况需要客户端做调整）
* 默认配置：2

#### hbase.hregion.memstore.flush.size

* memstore大小，当达到该值则会flush到外存设备
* 线上配置：104857600（100M）
* 默认值： 134217728（128M）

#### hbase.hregion.memstore.mslab.enabled

* 是否开启mslab方案，减少因内存碎片导致的Full GC，提高整体性能
* 线上配置：true
* 默认配置： true

#### hbase.regionserver.maxlogs

* regionserver的hlog数量
* 线上配置：128
* 默认配置：32

#### hbase.regionserver.hlog.blocksize

* hlog大小上限，达到该值则block，进行roll掉
* 线上配置：536870912（512M）
* 默认配置：hdfs配置的block大小

#### hbase.hstore.compaction.min

* 进入minor compact队列的storefiles最小个数
* 线上配置：10
* 默认配置：3

#### hbase.hstore.compaction.max

* 单次minor compact最多的文件个数
* 线上配置：30
* 默认配置：10

#### hbase.hstore.blockingStoreFiles

* 当某一个region的storefile个数达到该值则block写入，等待compact
* 线上配置：100（生产环境可以设置得很大）
* 默认配置： 7

#### hbase.hstore.blockingWaitTime

* block的等待时间
* 线上配置：90000（90s）
* 默认配置：90000（90s）

#### hbase.hregion.majorcompaction

* 触发major compact的周期
* 线上配置：0（关掉major compact）
* 默认配置：86400000（1d）

#### hbase.regionserver.thread.compaction.large

* large compact线程池的线程个数
* 线上配置：5
* 默认配置：1

#### hbase.regionserver.thread.compaction.small

* small compact线程池的线程个数
* 线上配置：5
* 默认配置：1

#### hbase.regionserver.thread.compaction.throttle

* compact（major和minor）请求进入large和small compact线程池的临界点
* 线上配置：10737418240（10G）
* 默认配置：2 \* this.minFilesToCompact \* this.region.memstoreFlushSize

#### hbase.hstore.compaction.max.size

* minor compact队列中storefile文件最大size
* 线上配置：21474836480（20G）
* 默认配置：Long.MAX\_VALUE

#### hbase.rpc.timeout

* RPC请求timeout时间
* 线上配置：300000（5min）
* 默认配置：60000（10s）

#### hbase.regionserver.region.split.policy

* split操作默认的策略
* 线上配置： org.apache.hadoop.hbase.regionserver.ConstantSizeRegionSplitPolicy（采取老的策略，自己控制split）
* 默认配置： org.apache.hadoop.hbase.regionserver.IncreasingToUpperBoundRegionSplitPolicy（在region没有达到maxFileSize的前提下，如果fileSize达到regionCount \* regionCount \* flushSize则进行split操作）

#### hbase.regionserver.regionSplitLimit

* 单台RegionServer上region数上限
* 线上配置：150
* 默认配置：2147483647

## hbase-env.sh配置

#### 指定系统运行环境

| `exportJAVA_HOME=/usr/lib/jvm/java-6-sun/#JDK HOMEexportHBASE_HOME=/home/hadoop/cdh4/hbase-0.94.2-cdh4.2.1# HBase 安装目录exportHBASE_LOG_DIR=/mnt/dfs/11/hbase/hbase-logs#日志输出路径` |
| :--- |


#### JVM参数调优

| `exportHBASE_OPTS="-verbose:gc -XX:+PrintGCDetails -Xloggc:${HBASE_LOG_DIR}/hbase-gc.log -XX:+PrintGCTimeStamps -XX:+PrintGCApplicationConcurrentTime -XX:+PrintGCApplicationStoppedTime \-server -Xmx20480m -Xms20480m -Xmn10240m -Xss256k  -XX:SurvivorRatio=4 -XX:MaxPermSize=256m -XX:MaxTenuringThreshold=15 \-XX:ParallelGCThreads=16 -XX:+UseConcMarkSweepGC -XX:+UseParNewGC  -XX:CMSFullGCsBeforeCompaction=5 -XX:+UseCMSCompactAtFullCollection \-XX:+CMSClassUnloadingEnabled  -XX:CMSInitiatingOccupancyFraction=70 -XX:+UseCMSInitiatingOccupancyOnly -XX:CMSMaxAbortablePrecleanTime=5000     \"` |
| :--- |


  


