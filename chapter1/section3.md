# 参考文档：

## 

1、[http://www.alidata.org/archives/1509](http://www.alidata.org/archives/1509)（存储模型比较详细）

2、[http://www.searchtb.com/2011/01/understanding-hbase.html](http://www.searchtb.com/2011/01/understanding-hbase.html)（技术框架以及存储模型）

3、[http://wenku.baidu.com/view/b46eadd228ea81c758f578f4.html](http://wenku.baidu.com/view/b46eadd228ea81c758f578f4.html)（读和写的流程比较详细）

4,[http://www.yiibai.com/hbase/](http://www.yiibai.com/hbase/)

Hadoop的限制



Hadoop只能执行批量处理，并且只以顺序方式访问数据。这意味着必须搜索整个数据集，即使是最简单的搜索工作。



当处理结果在另一个庞大的数据集，也是按顺序处理一个巨大的数据集。在这一点上，一个新的解决方案，需要访问数据中的任何点（随机访问）单元。



Hadoop随机存取数据库



应用程序，如HBase, Cassandra, couchDB, Dynamo 和 MongoDB 都是一些存储大量数据和以随机方式访问数据的数据库。

