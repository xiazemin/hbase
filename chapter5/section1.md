# HBase启用表



启用表的语法：



enable ‘emp’

给出下面是一个例子，使一个表启用。



hbase\(main\):005:0&gt; enable 'emp'

0 row\(s\) in 0.4580 seconds

验证



启用表之后，扫描。如果能看到的模式，那么证明表已成功启用。



hbase\(main\):006:0&gt; scan 'emp'



      ROW                        COLUMN+CELL



1 column=personal data:city, timestamp=1417516501, value=hyderabad



1 column=personal data:name, timestamp=1417525058, value=ramu



1 column=professional data:designation, timestamp=1417532601, value=manager



1 column=professional data:salary, timestamp=1417524244109, value=50000



2 column=personal data:city, timestamp=1417524574905, value=chennai



2 column=personal data:name, timestamp=1417524556125, value=ravi



2 column=professional data:designation, timestamp=14175292204, value=sr:engg



2 column=professional data:salary, timestamp=1417524604221, value=30000 



3 column=personal data:city, timestamp=1417524681780, value=delhi



3 column=personal data:name, timestamp=1417524672067, value=rajesh



3 column=professional data:designation, timestamp=14175246987, value=jr:engg



3 column=professional data:salary, timestamp=1417524702514, value=25000



3 row\(s\) in 0.0400 seconds

is\_enabled



此命令用于查找表是否被启用。它的语法如下：



hbase&gt; is\_enabled 'table name'

下面的代码验证表emp是否启用。如果启用，它将返回true，如果没有，它会返回false。



hbase\(main\):031:0&gt; is\_enabled 'emp'

true



0 row\(s\) in 0.0440 seconds

使用Java API启用表



要验证一个表是否被启用，使用isTableEnabled\(\)方法;并且使用enableTable\(\)方法使一个表启用。这些方法属于HBaseAdmin类。按照下面给出启用表的步骤。



第1步



HBaseAdmin类的实例如下所示。



// Creating configuration object

Configuration conf = HBaseConfiguration.create\(\);



// Creating HBaseAdmin object

HBaseAdmin admin = new HBaseAdmin\(conf\);

第2步



使用isTableEnabled\(\)方法验证表是否被启用，如下所示。



Boolean bool=admin.isTableEnabled\("emp"\);

第3步



如果表未禁用，那么禁用它，如下图所示





 

if\(!bool\){

   admin.enableTable\("emp"\);

   System.out.println\("Table enabled"\);

}

下面给出的是完整的程序，以验证表是否已启用，如果它不是，那么启用它。



import java.io.IOException;



import org.apache.hadoop.conf.Configuration;



import org.apache.hadoop.hbase.HBaseConfiguration;

import org.apache.hadoop.hbase.MasterNotRunningException;

import org.apache.hadoop.hbase.client.HBaseAdmin;



public class EnableTable{



   public static void main\(String args\[\]\) throws MasterNotRunningException, IOException{



   // Instantiating configuration class

   Configuration conf = HBaseConfiguration.create\(\);



   // Instantiating HBaseAdmin class

   HBaseAdmin admin = new HBaseAdmin\(conf\);



   // Verifying weather the table is disabled

   Boolean bool = admin.isTableEnabled\("emp"\);

   System.out.println\(bool\);



   // Disabling the table using HBaseAdmin object

   if\(!bool\){

      admin.enableTable\("emp"\);

      System.out.println\("Table Enabled"\);

   }

   

   }

}

