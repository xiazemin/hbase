# 插入数据实践

hbase\(main\):015:0&gt;        put 'emp','1','personal data:name','raju'

0 row\(s\) in 0.1210 seconds

hbase\(main\):017:0&gt; scan 'emp'

ROW                   COLUMN+CELL

 1                    column=personal data:name, timestamp=1502610583470, value=

                      raju

1 row\(s\) in 0.0480 seconds







