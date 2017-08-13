# HBase安全



我们可以授予和撤销HBase用户的权限。也有出于安全目的，三个命令：grant, revoke 和 user\_permission.。



grant



grant命令授予特定的权限，如读，写，执行和管理表给定一个特定的用户。 grant命令的语法如下：



hbase&gt; grant &lt;user&gt; &lt;permissions&gt; \[&lt;table&gt; \[&lt;column family&gt; \[&lt;column; qualifier&gt;\]\]

我们可以从RWXCA组，其中给予零个或多个特权给用户



R - 代表读取权限

W - 代表写权限

X - 代表执行权限

C - 代表创建权限

A - 代表管理权限

下面给出是为用户“Tutorialspoint'授予所有权限的例子。



hbase\(main\):018:0&gt; grant 'Tutorialspoint', 'RWXCA'

revoke



revoke命令用于撤销用户访问表的权限。它的语法如下：



hbase&gt; revoke &lt;user&gt;

下面的代码撤消名为“Tutorialspoint”用户的所有权限。



hbase\(main\):006:0&gt; revoke 'Tutorialspoint'

user\_permission



此命令用于列出特定表的所有权限。 user\_permission的语法如下：





 

hbase&gt;user\_permission ‘tablename’

下面的代码列出了“emp”表的所有用户权限。



hbase\(main\):013:0&gt; user\_permission 'emp'



