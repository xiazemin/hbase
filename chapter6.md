# HBase删除表



用drop命令可以删除表。在删除一个表之前必须先将其禁用。



hbase\(main\):018:0&gt; disable 'emp'

0 row\(s\) in 1.4580 seconds





hbase\(main\):019:0&gt; drop 'emp'

0 row\(s\) in 0.3060 seconds

使用exists 命令验证表是否被删除。



hbase\(main\):020:0&gt; exists 'emp'

Table emp does not exist



0 row\(s\) in 0.0730 seconds

drop\_all



这个命令是用来在给出删除匹配“regex”表。它的语法如下：



hbase&gt; drop\_all ‘t.\*’ 

注意：要删除表，则必须先将其禁用。



示例



假设有一些表的名称为raja, rajani, rajendra, rajesh, 和 raju。



hbase\(main\):017:0&gt; list

TABLE

raja

rajani

rajendra 

rajesh

raju

9 row\(s\) in 0.0270 seconds

所有这些表以字母raj开始。首先使用disable\_all命令禁用所有这些表如下所示。



hbase\(main\):002:0&gt; disable\_all 'raj.\*'

raja

rajani

rajendra

rajesh

raju

Disable the above 5 tables \(y/n\)?

y

5 tables successfully disabled

现在，可以使用 drop\_all 命令删除它们，如下所示。



hbase\(main\):018:0&gt; drop\_all 'raj.\*'

raja

rajani

rajendra

rajesh

raju



Drop the above 5 tables \(y/n\)?



y

5 tables successfully dropped

使用Java API删除表



可以使用 HBaseAdmin 类的deleteTable\(\)方法删除表。按照下面给出是使用Java API来删除表中的步骤。



第1步



实例化HBaseAdmin类。



// creating a configuration object

Configuration conf = HBaseConfiguration.create\(\);



// Creating HBaseAdmin object

HBaseAdmin admin = new HBaseAdmin\(conf\); 

第2步



使用HBaseAdmin类的disableTable\(\)方法禁止表。



admin.disableTable\("emp1"\);

第3步



现在使用HBaseAdmin类的deleteTable\(\)方法删除表。



admin.deleteTable\("emp12"\);

下面给出的是完整的Java程序用于删除HBase表。





 

import java.io.IOException;



import org.apache.hadoop.hbase.HBaseConfiguration;

import org.apache.hadoop.conf.Configuration;

import org.apache.hadoop.hbase.client.HBaseAdmin;



public class DeleteTable {



   public static void main\(String\[\] args\) throws IOException {



      // Instantiating configuration class

      Configuration conf = HBaseConfiguration.create\(\);



      // Instantiating HBaseAdmin class

      HBaseAdmin admin = new HBaseAdmin\(conf\);



      // disabling table named emp

      admin.disableTable\("emp12"\);



      // Deleting emp

      admin.deleteTable\("emp12"\);

      System.out.println\("Table deleted"\);

   }

}



