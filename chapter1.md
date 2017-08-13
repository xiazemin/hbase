# Hbase数据模型

![](/assets/importhd.png)hbase基本概念



RowKey：是Byte array，是表中每条记录的“主键”，方便快速查找，Rowkey的设计非常重要。

Column Family：列族，拥有一个名称\(string\)，包含一个或者多个相关列

Column：属于某一个columnfamily，familyName:columnName，每条记录可动态添加

Version Number：类型为Long，默认值是系统时间戳，可由用户自定义

Value\(Cell\)：Byte array

Hbase物理模型

每个column family存储在HDFS上的一个单独文件中，空值不会被保存。

Key 和 Version number在每个 column family中均有一份；

HBase 为每个值维护了多级索引，即：&lt;key, column family, column name, timestamp&gt;



