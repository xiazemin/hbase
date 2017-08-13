# HBase Admin API

HBaseAdmin类

HBaseAdmin是一个类表示管理。这个类属于org.apache.hadoop.hbase.client包。使用这个类，可以执行管理员任务。使用Connection.getAdmin\(\)方法来获取管理员的实例

| S.No. | 方法及说明 |
| :--- | :--- |
| 1 | **void createTable\(HTableDescriptor desc\)**创建一个新的表 |
| 2 | **void createTable\(HTableDescriptor desc, byte\[\]\[\] splitKeys\)**创建一个新表使用一组初始指定的分割键限定空区域 |
| 3 | **void deleteColumn\(byte\[\] tableName, String columnName\)**从表中删除列 |
| 4 | **void deleteColumn\(String tableName, String columnName\)**删除表中的列 |
| 5 | **void deleteTable\(String tableName\)**删除表 |

## 



