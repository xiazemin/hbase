# HBase客户端API



## HBaseConfiguration类

添加 HBase 的配置到配置文件。这个类属于org.apache.hadoop.hbase包。

### 方法及说明

| S.No. | 方法及说明 |
| :--- | :--- |
| 1 | **static org.apache.hadoop.conf.Configuration create\(\)**此方法创建使用HBase的资源配置 |

## HTable类

HTable表示HBase表中HBase的内部类。它用于实现单个HBase表进行通信。这个类属于org.apache.hadoop.hbase.client类。

### 构造函数

| S.No. | 构造函数 |
| :--- | :--- |
| 1 | **HTable\(\)** |
| 2 | **HTable\(TableName tableName, ClusterConnection connection, ExecutorService pool\)**使用此构造方法，可以创建一个对象来访问HBase表。 |

### 方法及说明

| S.No. | 构造函数 |
| :--- | :--- |
| 1 | **void close\(\)**释放HTable的所有资源 |
| 2 | **void delete\(Delete delete\)**删除指定的单元格/行 |
| 3 | **boolean exists\(Get get\)**使用这个方法，可以测试列的存在，在表中，由Get指定获取。 |
| 4 | **Result get\(Get get\)**检索来自一个给定的行某些单元格。 |
| 5 | **org.apache.hadoop.conf.Configuration getConfiguration\(\)**返回此实例的配置对象。 |
| 6 | **TableName getName\(\)**返回此表的表名称实例。 |
| 7 | **HTableDescriptor getTableDescriptor\(\)**返回此表的表描述符。 |
| 8 | **byte\[\] getTableName\(\)**返回此表的名称。 |
| 9 | **void put\(Put put\)**使用此方法，可以将数据插入到表中。 |

## Put类

此类用于为单个行执行PUT操作。它属于org.apache.hadoop.hbase.client包。

### 构造函数

| S.No. | 构造函数和描述 |
| :--- | :--- |
| 1 | **Put\(byte\[\] row\)**使用此构造方法，可以创建一个将操作指定行。 |
| 2 | **Put\(byte\[\] rowArray, int rowOffset, int rowLength\)**使用此构造方法，可以使传入的行键的副本，以保持到本地。 |
| 3 | **Put\(byte\[\] rowArray, int rowOffset, int rowLength, long ts\)**使用此构造方法，可以使传入的行键的副本，以保持到本地。 |
| 4 | **Put\(byte\[\] row, long ts\)**使用此构造方法，我们可以创建一个Put操作指定行，用一个给定的时间戳。 |

### 方法

| S.No. | 方法及描述 |
| :--- | :--- |
| 1 | **Put add\(byte\[\] family, byte\[\] qualifier, byte\[\] value\)**添加指定的列和值到 Put 操作。 |
| 2 | **Put add\(byte\[\] family, byte\[\] qualifier, long ts, byte\[\] value\)**添加指定的列和值，使用指定的时间戳作为其版本到Put操作。 |
| 3 | **Put add\(byte\[\] family, ByteBuffer qualifier, long ts, ByteBuffer value\)**添加指定的列和值，使用指定的时间戳作为其版本到Put操作。 |
| 4 | **Put add\(byte\[\] family, ByteBuffer qualifier, long ts, ByteBuffer value\)**添加指定的列和值，使用指定的时间戳作为其版本到Put操作。 |

## Get类

此类用于对单行执行get操作。这个类属于org.apache.hadoop.hbase.client包。

### 构造函数

| S.No. | 构造函数和描述 |
| :--- | :--- |
| 1 | **Get\(byte\[\] row\)**使用此构造方法，可以为指定行创建一个Get操作。 |
| 2 | **Get\(Get get\)** |

### 方法

| S.No. | 构造函数和描述 |
| :--- | :--- |
| 1 | **Get addColumn\(byte\[\] family, byte\[\] qualifier\)**检索来自特定列家族使用指定限定符 |
| 2 | **Get addFamily\(byte\[\] family\)**检索从指定系列中的所有列。 |

## Delete类

这个类用于对单行执行删除操作。要删除整行，实例化一个Delete对象用于删除行。这个类属于org.apache.hadoop.hbase.client包。

### 构造函数

| S.No. | 构造方法和描述 |
| :--- | :--- |
| 1 | **Delete\(byte\[\] row\)**创建一个指定行的Delete操作。 |
| 2 | **Delete\(byte\[\] rowArray, int rowOffset, int rowLength\)**创建一个指定行和时间戳的Delete操作。 |
| 3 | **Delete\(byte\[\] rowArray, int rowOffset, int rowLength, long ts\)**创建一个指定行和时间戳的Delete操作。 |
| 4 | **Delete\(byte\[\] row, long timestamp\)**创建一个指定行和时间戳的Delete操作。 |

### 方法

| S.No. | 构造方法和描述 |
| :--- | :--- |
| 1 | **Delete addColumn\(byte\[\] family, byte\[\] qualifier\)**删除指定列的最新版本。 |
| 2 | **Delete addColumns\(byte\[\] family, byte\[\] qualifier, long timestamp\)**删除所有版本具有时间戳小于或等于指定的时间戳的指定列。 |
| 3 | **Delete addFamily\(byte\[\] family\)**删除指定的所有列族的所有版本。 |
| 4 | **Delete addFamily\(byte\[\] family, long timestamp\)**删除指定列具有时间戳小于或等于指定的时间戳的列族。 |

## Result类

这个类是用来获取Get或扫描查询的单行结果。

### 构造函数

| S.No. | 构造函数 |
| :--- | :--- |
| 1 | **Result\(\)**使用此构造方法，可以创建无Key Value的有效负载空的结果;如果调用Cells\(\)返回null。 |

### 方法

| S.No. | 方法及描述 |
| :--- | :--- |
| 1 | **byte\[\] getValue\(byte\[\] family, byte\[\] qualifier\)**此方法用于获取指定列的最新版本 |
| 2 | **byte\[\] getRow\(\)**此方法用于检索对应于从结果中创建行的行键。 |

  


  




