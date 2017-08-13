# HBase表描述和修改



描述



该命令返回表的说明。它的语法如下：



hbase&gt; describe 'table name'

下面给出的是对emp表的 describe 命令的输出。



hbase\(main\):006:0&gt; describe 'emp'

   DESCRIPTION

      ENABLED

      

'emp', {NAME =&gt; 'READONLY', DATA\_BLOCK\_ENCODING =&gt; 'NONE', BLOOMFILTER

=&gt; 'ROW', REPLICATION\_SCOPE =&gt; '0', COMPRESSION =&gt; 'NONE', VERSIONS =&gt;

'1', TTL true





=&gt; 'FOREVER', MIN\_VERSIONS =&gt; '0', KEEP\_DELETED\_CELLS =&gt; 'false',

BLOCKSIZE =&gt; '65536', IN\_MEMORY =&gt; 'false', BLOCKCACHE =&gt; 'true'}, {NAME

=&gt; 'personal





data', DATA\_BLOCK\_ENCODING =&gt; 'NONE', BLOOMFILTER =&gt; 'ROW',

REPLICATION\_SCOPE =&gt; '0', VERSIONS =&gt; '5', COMPRESSION =&gt; 'NONE',

MIN\_VERSIONS =&gt; '0', TTL





=&gt; 'FOREVER', KEEP\_DELETED\_CELLS =&gt; 'false', BLOCKSIZE =&gt; '65536',

IN\_MEMORY =&gt; 'false', BLOCKCACHE =&gt; 'true'}, {NAME =&gt; 'professional

data', DATA\_BLO





CK\_ENCODING =&gt; 'NONE', BLOOMFILTER =&gt; 'ROW', REPLICATION\_SCOPE =&gt; '0',

VERSIONS =&gt; '1', COMPRESSION =&gt; 'NONE', MIN\_VERSIONS =&gt; '0', TTL =&gt;

'FOREVER', K





EEP\_DELETED\_CELLS =&gt; 'false', BLOCKSIZE =&gt; '65536', IN\_MEMORY =&gt;

'false', BLOCKCACHE =&gt; 'true'}, {NAME =&gt; 'table\_att\_unset',

DATA\_BLOCK\_ENCODING =&gt; 'NO 



NE', BLOOMFILTER =&gt; 'ROW', REPLICATION\_SCOPE =&gt; '0', COMPRESSION =&gt;

'NONE', VERSIONS =&gt; '1', TTL =&gt; 'FOREVER', MIN\_VERSIONS =&gt; '0',

KEEP\_DELETED\_CELLS





=&gt; 'false', BLOCKSIZE =&gt; '6

修改



alter用于更改现有表的命令。使用此命令可以更改列族的单元，设定最大数量和删除表范围运算符，并从表中删除列家族。



更改列族单元格的最大数目



下面给出的语法来改变列家族单元的最大数目。



hbase&gt; alter 't1', NAME =&gt; 'f1', VERSIONS =&gt; 5

在下面的例子中，单元的最大数目设置为5。



hbase\(main\):003:0&gt; alter 'emp', NAME =&gt; 'personal data', VERSIONS =&gt; 5

Updating all regions with the new schema...

0/1 regions updated.

1/1 regions updated.

Done.

0 row\(s\) in 2.3050 seconds

表范围运算符



使用alter，可以设置和删除表范围，运算符，如MAX\_FILESIZE，READONLY，MEMSTORE\_FLUSHSIZE，DEFERRED\_LOG\_FLUSH等。



设置只读



下面给出的是语法，是用以设置表为只读。



hbase&gt;alter 't1', READONLY\(option\)

在下面的例子中，我们已经设置表emp为只读。



hbase\(main\):006:0&gt; alter 'emp', READONLY

Updating all regions with the new schema...

0/1 regions updated.

1/1 regions updated.

Done.

0 row\(s\) in 2.2140 seconds

删除表范围运算符



也可以删除表范围运算。下面给出的是语法，从emp表中删除“MAX\_FILESIZE”。



hbase&gt; alter 't1', METHOD =&gt; 'table\_att\_unset', NAME =&gt; 'MAX\_FILESIZE'

删除列族



使用alter，也可以删除列族。下面给出的是使用alter删除列族的语法。



hbase&gt; alter ‘ table name ’, ‘delete’ =&gt; ‘ column family ’ 

下面给出的是一个例子，从“emp”表中删除列族。



假设在HBase中有一个employee表。它包含以下数据：



hbase\(main\):006:0&gt; scan 'employee'



         ROW                   COLUMN+CELL



row1 column=personal:city, timestamp=1418193767, value=hyderabad



row1 column=personal:name, timestamp=1418193806767, value=raju



row1 column=professional:designation, timestamp=1418193767, value=manager



row1 column=professional:salary, timestamp=1418193806767, value=50000



1 row\(s\) in 0.0160 seconds 

现在使用alter命令删除指定的 professional 列族。



hbase\(main\):007:0&gt; alter 'employee','delete'=&gt;'professional'

Updating all regions with the new schema...

0/1 regions updated.

1/1 regions updated.

Done.

0 row\(s\) in 2.2380 seconds 

现在验证该表中变更后的数据。观察列族“professional”也没有了，因为前面已经被删除了。



hbase\(main\):003:0&gt; scan 'employee'

 ROW             COLUMN+CELL

row1 column=personal:city, timestamp=14181936767, value=hyderabad



row1 column=personal:name, timestamp=1418193806767, value=raju



1 row\(s\) in 0.0830 seconds

使用Java API添加一列族



可以使用HBAseAdmin类的addColumn方法添加一列家族的表。按照下面给出的步骤将一个列族添加到表中。



第1步



实例化HBaseAdmin类。



// Instantiating configuration object

Configuration conf = HBaseConfiguration.create\(\);



// Instantiating HBaseAdmin class

HBaseAdmin admin = new HBaseAdmin\(conf\); 

第2步



addColumn\(\)方法需要一个表名和一个HColumnDescriptorclass对象。因此需要实例化HColumnDescriptor类。 HColumnDescriptor依次构造函数需要一个列族名称用于添加。在这里加入了一个名为“contactDetails”到“employee”表的列族。





 

// Instantiating columnDescriptor object



HColumnDescriptor columnDescriptor = new

HColumnDescriptor\("contactDetails"\);

第3步



使用addColumn方法添加列族。通过表名和HColumnDescriptor类对象作为这个方法的参数。



// Adding column family

admin.addColumn\("employee", new HColumnDescriptor\("columnDescriptor"\)\);

下面给出的是一个完整的程序，用于添加一列族到现有的表。



import java.io.IOException;



import org.apache.hadoop.conf.Configuration;



import org.apache.hadoop.hbase.HBaseConfiguration;

import org.apache.hadoop.hbase.HColumnDescriptor;

import org.apache.hadoop.hbase.MasterNotRunningException;

import org.apache.hadoop.hbase.client.HBaseAdmin;



public class AddColoumn{



   public static void main\(String args\[\]\) throws MasterNotRunningException, IOException{



      // Instantiating configuration class.

      Configuration conf = HBaseConfiguration.create\(\);



      // Instantiating HBaseAdmin class.

      HBaseAdmin admin = new HBaseAdmin\(conf\);



      // Instantiating columnDescriptor class

      HColumnDescriptor columnDescriptor = new HColumnDescriptor\("contactDetails"\);

      

      // Adding column family

      admin.addColumn\("employee", columnDescriptor\);

      System.out.println\("coloumn added"\);

   }

}

编译和执行上述程序，如下所示



$javac AddColumn.java

$java AddColumn

上述编译只有已经设置“.bashrc”中的类路径。如果还没有，请按照下面编译给出.java文件的程序。



//if "/home/home/hadoop/hbase " is your Hbase home folder then.





$javac -cp /home/hadoop/hbase/lib/\*: Demo.java

如果一切顺利，它会生成以下的输出：



 column added

使用Java API删除列族



可以使用HBAseAdmin类的deleteColumn\(\)方法删除列族。按照下面给出的步骤添加一个列族到表中。



第1步



实例化HBaseAdmin类。



// Instantiating configuration object

Configuration conf = HBaseConfiguration.create\(\);



// Instantiating HBaseAdmin class

HBaseAdmin admin = new HBaseAdmin\(conf\); 

第2步



使用deleteColumn\(\)方法添加列族。传递表名和列族名作为这个方法的参数。



// Deleting column family

admin.deleteColumn\("employee", "contactDetails"\); 

下面给出的是从现有表中删除列族的完整的程序。



import java.io.IOException;



import org.apache.hadoop.conf.Configuration;



import org.apache.hadoop.hbase.HBaseConfiguration;

import org.apache.hadoop.hbase.MasterNotRunningException;

import org.apache.hadoop.hbase.client.HBaseAdmin;



public class DeleteColoumn{



   public static void main\(String args\[\]\) throws MasterNotRunningException, IOException{



      // Instantiating configuration class.

      Configuration conf = HBaseConfiguration.create\(\);



      // Instantiating HBaseAdmin class.

      HBaseAdmin admin = new HBaseAdmin\(conf\);



      // Deleting a column family

      admin.deleteColumn\("employee","contactDetails"\);

      System.out.println\("coloumn deleted"\); 

   }

}



