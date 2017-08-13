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

