# hbase  shell



$ ./bin/hbase shell

SLF4J: Class path contains multiple SLF4J bindings.

SLF4J: Found binding in \[jar:file:/Users/didi/hbase/hbase/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class\]

SLF4J: Found binding in \[jar:file:/Users/didi/hadoop/hadoop/share/hadoop/common/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class\]

SLF4J: See http://www.slf4j.org/codes.html\#multiple\_bindings for an explanation.

SLF4J: Actual binding is of type \[org.slf4j.impl.Log4jLoggerFactory\]

2017-08-13 13:40:42,458 WARN  \[main\] util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable

HBase Shell; enter 'help&lt;RETURN&gt;' for list of supported commands.

Type "exit&lt;RETURN&gt;" to leave the HBase Shell

Version 1.1.11, rbc73820af4c8e8e056f7e6e4f42af7ce3c6905c6, Sat Jun 10 18:18:50 PDT 2017



hbase\(main\):001:0&gt;

hbase\(main\):002:0\* list

TABLE

0 row\(s\) in 0.2160 seconds



=&gt; \[\]

hbase\(main\):003:0&gt;      status

1 servers, 0 dead, 2.0000 average load



hbase\(main\):004:0&gt; version

1.1.11, rbc73820af4c8e8e056f7e6e4f42af7ce3c6905c6, Sat Jun 10 18:18:50 PDT 2017



hbase\(main\):005:0&gt; whoami

didi \(auth:SIMPLE\)

    groups: staff, com.apple.sharepoint.group.1, everyone, localaccounts, \_appserverusr, admin, \_appserveradm, \_lpadmin, \_appstore, \_lpoperator, \_developer, com.apple.access\_ftp, com.apple.access\_screensharing, com.apple.access\_ssh



hbase\(main\):006:0&gt; table\_help

Help for table-reference commands.



You can either create a table via 'create' and then manipulate the table via commands like 'put', 'get', etc.

See the standard help information for how to use each of these commands.



However, as of 0.96, you can also get a reference to a table, on which you can invoke commands.

For instance, you can get create a table and keep around a reference to it via:



   hbase&gt; t = create 't', 'cf'



Or, if you have already created the table, you can get a reference to it:



   hbase&gt; t = get\_table 't'



You can do things like call 'put' on the table:



  hbase&gt; t.put 'r', 'cf:q', 'v'



which puts a row 'r' with column family 'cf', qualifier 'q' and value 'v' into table t.



To read the data out, you can scan the table:



  hbase&gt; t.scan



which will read all the rows in table 't'.



Essentially, any command that takes a table name can also be done via table reference.

Other commands include things like: get, delete, deleteall,

get\_all\_columns, get\_counter, count, incr. These functions, along with

the standard JRuby object methods are also available via tab completion.



For more information on how to use each of these commands, you can also just type:



   hbase&gt; t.help 'scan'



which will output more information on how to use that command.



You can also do general admin actions directly on a table; things like enable, disable,

flush and drop just by typing:



   hbase&gt; t.enable

   hbase&gt; t.flush

   hbase&gt; t.disable

   hbase&gt; t.drop



Note that after dropping a table, your reference to it becomes useless and further usage

is undefined \(and not recommended\).



hbase\(main\):007:0&gt;

