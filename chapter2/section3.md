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



