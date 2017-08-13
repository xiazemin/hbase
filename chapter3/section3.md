# HBASE WEBUI

1.0.1版本的hbase的master web 默认是不运行的，所以需要自己配置默认端口。

在hbase-site.xml中加入一下内容即可

&lt;!-- 新增的配置 --&gt;

&lt;property&gt;

&lt;name&gt;hbase.master.info.port&lt;/name&gt;

&lt;value&gt;60010&lt;/value&gt;

&lt;/property&gt;

&lt;!-- 新增的配置 --&gt;

$ ./bin/stop-hbase.sh

stopping hbase..................

192:hbase didi$ ./bin/start-hbase.sh

starting master, logging to /Users/didi/hbase/hbase/bin/../logs/hbase-didi-master-192.168.0.103.out

Java HotSpot\(TM\) 64-Bit Server VM warning: ignoring option PermSize=128m; support was removed in 8.0

Java HotSpot\(TM\) 64-Bit Server VM warning: ignoring option MaxPermSize=128m; support was removed in 8.0

![](/assets/importui.png)

