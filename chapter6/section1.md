# HBase关闭



exit



可以通过键入exit命令退出shell。



hbase\(main\):021:0&gt; exit

停止HBase



要停止HBase，浏览进入到HBase主文件夹，然后键入以下命令。



./bin/stop-hbase.sh

使用Java API停止HBase



可以使用HBaseAdmin类的shutdown\(\)方法关闭HBase。按照下面给出关闭HBase的步骤：



第1步



实例化HbaseAdmin类。



// Instantiating configuration object

Configuration conf = HBaseConfiguration.create\(\);



// Instantiating HBaseAdmin object

HBaseAdmin admin = new HBaseAdmin\(conf\);

第2步



使用HBaseAdmin类的shutdown\(\)方法关闭HBase。



admin.shutdown\(\);

下面给出的是停止HBase的程序。



import java.io.IOException;



import org.apache.hadoop.hbase.HBaseConfiguration;

import org.apache.hadoop.conf.Configuration;

import org.apache.hadoop.hbase.client.HBaseAdmin;



public class ShutDownHbase{



   public static void main\(String args\[\]\)throws IOException {



      // Instantiating configuration class

      Configuration conf = HBaseConfiguration.create\(\);



      // Instantiating HBaseAdmin class

      HBaseAdmin admin = new HBaseAdmin\(conf\);



      // Shutting down HBase

      System.out.println\("Shutting down hbase"\);

      admin.shutdown\(\);

   }

}

