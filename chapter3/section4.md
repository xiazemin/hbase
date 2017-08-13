# HBase常用命令

HBase常用命令status, version, table\_help和whoami。本章将介绍了这些命令。



status



命令返回包括在系统上运行的服务器的细节和系统的状态。它的语法如下：



hbase\(main\):009:0&gt; status

如果执行这个命令，它会返回下面的输出



hbase\(main\):009:0&gt; status

3 servers, 0 dead, 1.3333 average load

version



该命令返回HBase系统使用的版本。它的语法如下：



hbase\(main\):010:0&gt; version

如果执行这个命令，它会返回下面的输出。



hbase\(main\):009:0&gt; version

0.98.8-hadoop2, r6cfc8d064754251365e070a10a82eb169956d5fe, Fri Nov 14

18:26:29 PST 2014

table\_help



此命令将引导如何使用表引用的命令。



