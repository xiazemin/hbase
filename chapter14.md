# HBase计数和截断



count



可以使用count命令计算表的行数量。它的语法如下：



count ‘&lt;table name&gt;’ 

删除第一行后，表emp就只有两行。验证它，如下图所示。



hbase\(main\):023:0&gt; count 'emp'

2 row\(s\) in 0.090 seconds

=&gt; 2 

truncate



此命令将禁止删除并重新创建一个表。truncate 的语法如下：



hbase&gt; truncate 'table name'

下面给出是 truncate 命令的例子。在这里，我们已经截断了emp表。



hbase\(main\):011:0&gt; truncate 'emp'

Truncating 'one' table \(it may take a while\):

   - Disabling table...

   - Truncating table...

  0 row\(s\) in 1.5950 seconds

截断表之后，使用scan 命令来验证。会得到表的行数为零。





 

hbase\(main\):017:0&gt; scan ‘emp’

ROW                  COLUMN+CELL

0 row\(s\) in 0.3110 seconds



