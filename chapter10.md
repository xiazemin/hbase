# HBase更新数据



可以使用put命令更新现有的单元格值。按照下面的语法，并注明新值，如下图所示。



put ‘table name’,’row ’,'Column family:column name',’new value’

新给定值替换现有的值，并更新该行。



示例



假设HBase中有一个表emp拥有下列数据



hbase\(main\):003:0&gt; scan 'emp'

 ROW              COLUMN+CELL

row1 column=personal:name, timestamp=1418051555, value=raju

row1 column=personal:city, timestamp=1418275907, value=Hyderabad

row1 column=professional:designation, timestamp=14180555,value=manager

row1 column=professional:salary, timestamp=1418035791555,value=50000

1 row\(s\) in 0.0100 seconds

以下命令将更新名为“Raju'员工的城市值为'Delhi'。



hbase\(main\):002:0&gt; put 'emp','row1','personal:city','Delhi'

0 row\(s\) in 0.0400 seconds

更新后的表如下所示，观察这个城市Raju的值已更改为“Delhi”。



hbase\(main\):003:0&gt; scan 'emp'

  ROW          COLUMN+CELL

row1 column=personal:name, timestamp=1418035791555, value=raju

row1 column=personal:city, timestamp=1418274645907, value=Delhi

row1 column=professional:designation, timestamp=141857555,value=manager

row1 column=professional:salary, timestamp=1418039555, value=50000

1 row\(s\) in 0.0100 seconds

使用Java API更新数据



使用put\(\)方法将特定单元格更新数据。按照下面给出更新表的现有单元格值的步骤。



第1步：实例化Configuration类



Configuration类增加了HBase的配置文件到它的对象。使用HbaseConfiguration类的create\(\)方法，如下图所示的配置对象。



Configuration conf = HbaseConfiguration.create\(\);

第2步：实例化HTable类



有一类叫HTable，实现在HBase中的Table类。此类用于单个HBase的表进行通信。在这个类实例，它接受配置对象和表名作为参数。实例化HTable类，如下图所示。



HTable hTable = new HTable\(conf, tableName\);

第3步：实例化Put类



要将数据插入到HBase表中，使用add\(\)方法和它的变体。这种方法属于Put类，因此实例化Put类。这个类必须以字符串格式的列名插入数据。可以实例化Put类，如下图所示。



Put p = new Put\(Bytes.toBytes\("row1"\)\);

第4步：更新现有的单元格



Put 类的add\(\)方法用于插入数据。它需要表示列族，列限定符（列名称）3字节阵列，并要插入的值。将数据插入HBase表使用add\(\)方法，如下图所示。



p.add\(Bytes.toBytes\("coloumn family "\), Bytes.toBytes\("column

name"\),Bytes.toBytes\("value"\)\);

p.add\(Bytes.toBytes\("personal"\),

Bytes.toBytes\("city"\),Bytes.toBytes\("Delih"\)\);

第5步：保存表数据



插入所需的行后，HTable类实例的put\(\)方法添加如下所示保存更改。



hTable.put\(p\); 

第6步：关闭HTable实例



创建在HBase的表数据之后，使用close\(\)方法，如下所示关闭HTable实例。



hTable.close\(\);

下面给出的是完整的程序，在一个特定的表更新数据。





 

import java.io.IOException;



import org.apache.hadoop.conf.Configuration;



import org.apache.hadoop.hbase.HBaseConfiguration;

import org.apache.hadoop.hbase.client.HTable;

import org.apache.hadoop.hbase.client.Put;

import org.apache.hadoop.hbase.util.Bytes;



public class UpdateData{



public static void main\(String\[\] args\) throws IOException {



      // Instantiating Configuration class

      Configuration config = HBaseConfiguration.create\(\);



      // Instantiating HTable class

      HTable hTable = new HTable\(config, "emp"\);



      // Instantiating Put class

      //accepts a row name

      Put p = new Put\(Bytes.toBytes\("row1"\)\);



      // Updating a cell value

      p.add\(Bytes.toBytes\("personal"\),

      Bytes.toBytes\("city"\),Bytes.toBytes\("Delih"\)\);



      // Saving the put Instance to the HTable.

      hTable.put\(p\);

      System.out.println\("data Updated"\);



      // closing HTable

      hTable.close\(\);

   }

}



