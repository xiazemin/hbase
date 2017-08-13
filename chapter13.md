# HBase扫描



scan 命令用于查看HTable数据。使用 scan 命令可以得到表中的数据。它的语法如下：



scan ‘&lt;table name&gt;’ 

下面的示例演示了如何使用scan命令从表中读取数据。在这里读取的是emp表。



hbase\(main\):010:0&gt; scan 'emp'



ROW                           COLUMN+CELL



1 column=personal data:city, timestamp=1417521848375, value=hyderabad



1 column=personal data:name, timestamp=1417521785385, value=ramu



1 column=professional data:designation, timestamp=1417585277,value=manager



1 column=professional data:salary, timestamp=1417521903862, value=50000



1 row\(s\) in 0.0370 seconds

使用Java API扫描



使用Java API扫描整个表的数据的完整程序如下：



import java.io.IOException;



import org.apache.hadoop.conf.Configuration;



import org.apache.hadoop.hbase.HBaseConfiguration;

import org.apache.hadoop.hbase.util.Bytes;



import org.apache.hadoop.hbase.client.HTable;

import org.apache.hadoop.hbase.client.Result;

import org.apache.hadoop.hbase.client.ResultScanner;

import org.apache.hadoop.hbase.client.Scan;





public class ScanTable{



   public static void main\(String args\[\]\) throws IOException{



      // Instantiating Configuration class

      Configuration config = HBaseConfiguration.create\(\);



      // Instantiating HTable class

      HTable table = new HTable\(config, "emp"\);



      // Instantiating the Scan class

      Scan scan = new Scan\(\);



      // Scanning the required columns

      scan.addColumn\(Bytes.toBytes\("personal"\), Bytes.toBytes\("name"\)\);

      scan.addColumn\(Bytes.toBytes\("personal"\), Bytes.toBytes\("city"\)\);



      // Getting the scan result

      ResultScanner scanner = table.getScanner\(scan\);



      // Reading values from scan result

      for \(Result result = scanner.next\(\); result != null; result = Scanner.next\(\)\)



      System.out.println\("Found row : " + result\);

      //closing the scanner

      scanner.close\(\);

   }

}

