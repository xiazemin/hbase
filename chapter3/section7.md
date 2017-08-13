# 使用Java API创建一个表

可以使用HBaseAdmin类的createTable\(\)方法创建表在HBase中。这个类属于org.apache.hadoop.hbase.client 包。下面给出的步骤是来使用Java API创建表在HBase中。



第1步：实例化HBaseAdmin



这个类需要配置对象作为参数，因此初始实例配置类传递此实例给HBaseAdmin。



Configuration conf = HBaseConfiguration.create\(\);

HBaseAdmin admin = new HBaseAdmin\(conf\);

第2步：创建TableDescriptor



HTableDescriptor类是属于org.apache.hadoop.hbase。这个类就像表名和列族的容器一样。



//creating table descriptor

HTableDescriptor table = new HTableDescriptor\(toBytes\("Table name"\)\);

//creating column family descriptor

HColumnDescriptor family = new HColumnDescriptor\(toBytes\("column family"\)\);

//adding coloumn family to HTable

table.addFamily\(family\);

第3步：通过执行管理



使用HBaseAdmin类的createTable\(\)方法，可以在管理模式执行创建的表。



admin.createTable\(table\);



