# 安装hbase

axel  -n 20 [http://apache.fayea.com/hbase/1.1.11/hbase-1.1.11-bin.tar.gz](http://apache.fayea.com/hbase/1.1.11/hbase-1.1.11-bin.tar.gz)

$ ls

CHANGES.txt	LICENSE.txt	README.txt	conf		hbase-webapps

LEGAL		NOTICE.txt	bin		docs		lib

$ vi .bashrc

export HBASE\_HOME=/Users/didi/hbase/hbase

export PATH=$HBASE\_HOME/bin:$PATH

