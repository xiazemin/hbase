# HBase禁用表



要删除表或改变其设置，首先需要使用 disable 命令关闭表。使用 enable 命令，可以重新启用它。



下面给出的语法是用来禁用一个表：



disable ‘emp’

下面给出的是一个例子，说明如何禁用表。



hbase\(main\):025:0&gt; disable 'emp'

0 row\(s\) in 1.2760 seconds

验证



禁用表之后，仍然可以通过 list 和exists命令查看到。无法扫描到它存在，它会给下面的错误。



hbase\(main\):028:0&gt; scan 'emp'



ROW         COLUMN+CELL



ERROR: emp is disabled.

is\_disabled



这个命令是用来查看表是否被禁用。它的语法如下。



hbase&gt; is\_disabled 'table name'

下面的例子验证表名为emp是否被禁用。如果禁用，它会返回true，如果没有，它会返回false。



hbase\(main\):031:0&gt; is\_disabled 'emp'



true



0 row\(s\) in 0.0440 seconds

disable\_all



此命令用于禁用所有匹配给定正则表达式的表。disable\_all命令的语法如下。



hbase&gt; disable\_all 'r.\*'

假设有5个表在HBase，即raja, rajani, rajendra, rajesh 和 raju。下面的代码将禁用所有以 raj 开始的表。



hbase\(main\):002:0&gt; disable\_all 'raj.\*'



raja

rajani

rajendra

rajesh

raju

Disable the above 5 tables \(y/n\)?



y



5 tables successfully disabled

禁用表使用Java API



要验证一个表是否被禁用，使用isTableDisabled\(\)方法和disableTable\(\)方法禁用一个表。这些方法属于HBaseAdmin类。按照下面给出禁用表中的步骤。



第1步



HBaseAdmin类的实例如下所示。



// Creating configuration object

Configuration conf = HBaseConfiguration.create\(\);



// Creating HBaseAdmin object

HBaseAdmin admin = new HBaseAdmin\(conf\);

第2步



使用isTableDisabled\(\)方法验证表是否被禁用，如下图所示。



Boolean b = admin.isTableDisabled\("emp"\);

第3步



如果表未禁用，禁用它，如下图所示。



if\(!b\){

   admin.disableTable\("emp"\);

   System.out.println\("Table disabled"\);

}

下面给出的是完整的程序，以验证表是否被禁用;如果没有，那么如何禁用它？



import java.io.IOException;



import org.apache.hadoop.conf.Configuration;



import org.apache.hadoop.hbase.HBaseConfiguration;

import org.apache.hadoop.hbase.MasterNotRunningException;

import org.apache.hadoop.hbase.client.HBaseAdmin;



public class DisableTable{



   public static void main\(String args\[\]\) throws MasterNotRunningException, IOException{



   // Instantiating configuration class

   Configuration conf = HBaseConfiguration.create\(\);

 

   // Instantiating HBaseAdmin class

   HBaseAdmin admin = new HBaseAdmin\(conf\);



   // Verifying weather the table is disabled

   Boolean bool = admin.isTableDisabled\("emp"\);

   System.out.println\(bool\);



   // Disabling the table using HBaseAdmin object

   if\(!bool\){

      admin.disableTable\("emp"\);

      System.out.println\("Table disabled"\);

   }



   }

}

