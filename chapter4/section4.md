# 使用Java API列出表





在类HBaseAdmin中有一个方法叫 listTables\(\)，列出HBase中所有的表的列表。这个方法返回HTableDescriptor对象的数组。



//creating a configuration object

Configuration conf = HBaseConfiguration.create\(\);





//Creating HBaseAdmin object

HBaseAdmin admin = new HBaseAdmin\(conf\);





//Getting all the list of tables using HBaseAdmin object

HTableDescriptor\[\] tableDescriptor =admin.listTables\(\);





就可以得到使用HTableDescriptor类长度可变的HTableDescriptor\[\]数组的长度。从该对象使用getNameAsString\(\)方法获得表的名称。运行'for'循环而获得HBase表的列表。





