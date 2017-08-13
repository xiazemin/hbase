# HBase删除数据



从表删除特定单元格



使用 delete 命令，可以在一个表中删除特定单元格。 delete 命令的语法如下：



delete ‘&lt;table name&gt;’, ‘&lt;row&gt;’, ‘&lt;column name &gt;’, ‘&lt;time stamp&gt;’

下面是一个删除特定单元格和例子。在这里，我们删除salary



hbase\(main\):006:0&gt; delete 'emp', '1', 'personal data:city',

1417521848375

0 row\(s\) in 0.0060 seconds

删除表的所有单元格



使用“deleteall”命令，可以删除一行中所有单元格。下面给出是 deleteall 命令的语法。



deleteall ‘&lt;table name&gt;’, ‘&lt;row&gt;’,

这里是使用“deleteall”命令删去 emp 表 row1 的所有单元的一个例子。



hbase\(main\):007:0&gt; deleteall 'emp','1'

0 row\(s\) in 0.0240 seconds

使用scan命令验证表。表被删除后的快照如下。



hbase\(main\):022:0&gt; scan 'emp'



ROW                  COLUMN+CELL



2 column=personal data:city, timestamp=1417524574905, value=chennai 



2 column=personal data:name, timestamp=1417524556125, value=ravi



2 column=professional data:designation, timestamp=1417524204, value=sr:engg



2 column=professional data:salary, timestamp=1417524604221, value=30000



3 column=personal data:city, timestamp=1417524681780, value=delhi



3 column=personal data:name, timestamp=1417524672067, value=rajesh



3 column=professional data:designation, timestamp=1417523187, value=jr:engg



3 column=professional data:salary, timestamp=1417524702514, value=25000

使用Java API删除数据



可以从使用HTable类的delete\(\)方法删除HBase表数据。按照下面给出从表中删除数据的步骤。



第1步：实例化Configuration类



Configuration类增加了HBase配置文件到它的对象。可以创建使用HbaseConfiguration类的create\(\)方法，如下图所示的Configuration 对象。



Configuration conf = HbaseConfiguration.create\(\);

第2步：实例化HTable类



有一个类叫HTable，实现在HBase中的Table类。此类用于单个HBase的表进行通信。在这个类实例，它接受配置对象和表名作为参数。实例化HTable类，如下图所示。



HTable hTable = new HTable\(conf, tableName\); 

第3步：实例化Delete 类



通过传递将要删除的行的行ID，在字节数组格式实例化Delete类。也可以通过构造时间戳和Rowlock。



Delete delete = new Delete\(toBytes\("row1"\)\);

第4步：选择删除数据



可以使用Delete类的delete方法删除数据。这个类有各种删除方法。选择使用这些方法来删除列或列族。这里显示Delete类方法的用法在下面的例子。



delete.deleteColumn\(Bytes.toBytes\("personal"\), Bytes.toBytes\("name"\)\);

delete.deleteFamily\(Bytes.toBytes\("professional"\)\);

第5步：删除数据



通过HTable类实例的delete\(\)方法，如下所示删除所选数据。



table.delete\(delete\); 

第6步：关闭HTable实例



删除数据后，关闭HTable实例。



table.close\(\);

下面给出的是从HBase表中删除的数据的完整程序。





 

import java.io.IOException;



import org.apache.hadoop.conf.Configuration;



import org.apache.hadoop.hbase.HBaseConfiguration;

import org.apache.hadoop.hbase.client.Delete;

import org.apache.hadoop.hbase.client.HTable;

import org.apache.hadoop.hbase.util.Bytes;



public class DeleteData {



   public static void main\(String\[\] args\) throws IOException {



      // Instantiating Configuration class

      Configuration conf = HBaseConfiguration.create\(\);



      // Instantiating HTable class

      HTable table = new HTable\(conf, "employee"\);



      // Instantiating Delete class

      Delete delete = new Delete\(Bytes.toBytes\("row1"\)\);

      delete.deleteColumn\(Bytes.toBytes\("personal"\), Bytes.toBytes\("name"\)\);

      delete.deleteFamily\(Bytes.toBytes\("professional"\)\);



      // deleting the data

      table.delete\(delete\);



      // closing the HTable object

      table.close\(\);

      System.out.println\("data deleted....."\);

   }

}



