# section3

启动HBase

通过HBase根目录下的bin文件夹浏览并启动HBase。

$cd /usr/local/HBase

$./bin/start-hbase.sh

启动HBase主服务器

这在相同目录。启动它，如下图所示：

$./bin/local-master-backup.sh start 2 \(number signifies specific

server.\)

启动区域服务

启动区域服务器，如下所示。

$./bin/./local-regionservers.sh start 3

启动HBase Shell

可以使用以下命令启动HBase shell

$ ./bin/hbase shell

HBase的Web界面



要访问 HBase 的 Web界面，在浏览器中键入以下URL



http://localhost:60010

以下界面列出了当前正在运行的区域服务器，备份主服务以及HBase表。

vi  ~/.bashrc

为HBase库设置类路径（HBase的lib文件夹），如下图所示。



export CLASSPATH=$CLASSPATH://home/hadoop/hbase/lib/\*

这是为了防止“未找到类（class not found）”异常，同时使用Java API访问HBase。

