# HBase读取数据



get命令和HTable类的get\(\)方法用于从HBase表中读取数据。使用 get 命令，可以同时获取一行数据。它的语法如下：



get ’&lt;table name&gt;’,’row1’

下面的例子说明如何使用get命令。扫描emp表的第一行。



hbase\(main\):012:0&gt; get 'emp', '1'



   COLUMN                     CELL

   

personal : city timestamp=1417521848375, value=hyderabad



personal : name timestamp=1417521785385, value=ramu



professional: designation timestamp=1417521885277, value=manager



professional: salary timestamp=1417521903862, value=50000



4 row\(s\) in 0.0270 seconds

读取指定列



下面给出的是语法，使用get方法读取指定列。



hbase&gt;get 'table name', ‘rowid’, {COLUMN =&gt; ‘column family:column name ’}

下面给出的示例，是用于读取HBase表中的特定列。



hbase\(main\):015:0&gt; get 'emp', 'row1', {COLUMN=&gt;'personal:name'}



  COLUMN                CELL

  

personal:name timestamp=1418035791555, value=raju



1 row\(s\) in 0.0080 seconds

使用Java API读取数据



从一个HBase表中读取数据，要使用HTable类的get\(\)方法。这种方法需要Get类的一个实例。按照下面从HBase表中检索数据给出的步骤。



第1步：实例化Configuration类



Configuration类增加了HBase的配置文件到它的对象。使用HbaseConfiguration类的create\(\)方法，如下图所示的配置对象。



Configuration conf = HbaseConfiguration.create\(\);

第2步：实例化HTable类



有一类叫HTable，实现在HBase中的Table类。此类用于单个HBase的表进行通信。在这个类实例，它接受配置对象和表名作为参数。实例化HTable类，如下图所示。



HTable hTable = new HTable\(conf, tableName\);

第3步：实例化获得类



可以从HBase表使用HTable类的get\(\)方法检索数据。此方法提取从一个给定的行的单元格。它需要一个 Get 类对象作为参数。创建如下图所示。



Get get = new Get\(toBytes\("row1"\)\);

第4步：读取数据



当检索数据，可以通过ID得到一个单列，或得到一组行一组行ID，或者扫描整个表或行的子集。



可以使用Get类的add方法变种检索HBase表中的数据。



从特定的列族获取指定的列，使用下面的方法。



get.addFamily\(personal\) 

要得到一个特定的列族的所有列，使用下面的方法。



get.addColumn\(personal, name\) 

第5步：获取结果



获取结果通过Get类实例的HTable类的get方法。此方法返回Result类对象，其中保存所请求的结果。下面给出的是get\(\)方法的使用。



Result result = table.get\(g\);  

第6步：从Result实例读值



Result 类提供getValue\(\)方法从它的实例读出值。如下图所示，使用它从Result 实例读出值。



byte \[\] value =

result.getValue\(Bytes.toBytes\("personal"\),Bytes.toBytes\("name"\)\);

byte \[\] value1 =

result.getValue\(Bytes.toBytes\("personal"\),Bytes.toBytes\("city"\)\);

下面给出的是从一个HBase表中读取值的完整程序



import java.io.IOException;



import org.apache.hadoop.conf.Configuration;



import org.apache.hadoop.hbase.HBaseConfiguration;

import org.apache.hadoop.hbase.client.Get;

import org.apache.hadoop.hbase.client.HTable;

import org.apache.hadoop.hbase.client.Result;

import org.apache.hadoop.hbase.util.Bytes;



public class RetriveData{



   public static void main\(String\[\] args\) throws IOException, Exception{

   

      // Instantiating Configuration class

      Configuration config = HBaseConfiguration.create\(\);



      // Instantiating HTable class

      HTable table = new HTable\(config, "emp"\);



      // Instantiating Get class

      Get g = new Get\(Bytes.toBytes\("row1"\)\);



      // Reading the data

      Result result = table.get\(g\);



      // Reading values from Result class object

      byte \[\] value = result.getValue\(Bytes.toBytes\("personal"\),Bytes.toBytes\("name"\)\);



      byte \[\] value1 = result.getValue\(Bytes.toBytes\("personal"\),Bytes.toBytes\("city"\)\);



      // Printing the values

      String name = Bytes.toString\(value\);

      String city = Bytes.toString\(value1\);

      

      System.out.println\("name: " + name + " city: " + city\);

   }

}



