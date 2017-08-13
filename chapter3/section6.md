# HBase创建表

可以使用命令创建一个表，在这里必须指定表名和列族名。在HBase shell中创建表的语法如下所示。

create ‘&lt;table name&gt;’,’&lt;column family&gt;’

### 示例

下面给出的是一个表名为emp的样本模式。它有两个列族：“personal data”和“professional data”。

| Row key | personal data | professional data |
| :--- | :--- | :--- |
|  |  |  |
|  |  |  |

在HBase shell创建该表如下所示。

hbase\(main\):001:0&gt;  create 'emp', 'personal data', 'professional data';

hbase\(main\):002:0\*

hbase\(main\):003:0\* list

0 row\(s\) in 2.5600 seconds



TABLE

emp

1 row\(s\) in 0.0200 seconds



=&gt; \["emp"\]

