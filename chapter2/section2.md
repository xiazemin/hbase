# hbase 单机、伪分布、完全分布部署

# **hbase1.1.2安装文档（配套hadoop2.6.1）**

hbase 下载地址：

[http://hbase.apache.org/](http://hbase.apache.org/)

下载后解压到自己所需的目录：我的目录是/home/lin/hadoop/hbase-1.1.2

---

## **1、单机模式：**

\(1\)、修改conf/[Hbase](http://lib.csdn.net/base/hbase)-env.sh

添加java环境变量：

export JAVA\_HOME=/usr/soft/jdk1.7.0\_79

\(2\)、编辑[hbase](http://lib.csdn.net/base/hbase)-site.xml

若是不配置默认是temp 每次启动会被清空

&lt;configuration&gt;

```
&lt;property&gt;

    &lt;name&gt;hbase.rootdir&lt;/name&gt;

    &lt;value&gt;file:///home/lin/hadoop/hbase-1.1.2/data&lt;/value&gt;

&lt;/property&gt;
```

&lt;/configuration&gt;

\(3\)、启动hbase

$ bin/start-hbase.sh

jps 查看后 出现Hmaster就是启动成功 然后就可以进入shell进行对hbase的操作。

$ bin/hbase shell

单机模式配置成功！

---

## **2、伪分布模式：**

伪分布模式需要用到hadoop文件系统 ，所以配置会比单机模式麻烦很多 并且需要版本匹配；我用的

hadoop是2.6.1 hbase是1.1.2

\(1\)、修改conf/hbase-env.sh

添加java环境变量和hbase\_classpath\(

指向hadoop的配置文件目录

\)环境变量：

export JAVA\_HOME=/usr/soft/jdk1.7.0\_79

export HBASE\_CLASSPATH=/home/lin/hadoop/hadoop-2.6.1/etc/hadoop

\(2\)、编辑hbase-site.xml

hbase.rootdir 要配置为hdfs上的路径；打开分布

&lt;configuration&gt;

```
&lt;property&gt;

    &lt;name&gt;hbase.rootdir&lt;/name&gt;

    &lt;value&gt;file:///home/lin/hadoop/hbase-1.1.2/data&lt;/value&gt;

&lt;/property&gt;

&lt;property&gt;

    &lt;name&gt;hbase.cluster.distributed&lt;/name&gt;

    &lt;value&gt;true&lt;/value&gt;

&lt;/property&gt;
```

&lt;/configuration&gt;

\(3\)、启动hbase

$ bin/start-hbase.sh

jps 查看后出现下面的进程证明启动成功，可以看到比单机模式多了两个进程；

![](http://img.blog.csdn.net/20151028104552306?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

然后就可以进入shell进行对hbase的操作。

![](file:///D:/Documents/我的文档/My Knowledge/temp/f65d8d0e-53b6-4946-83ce-067ca7dc8f4e_128_files/4207a1bb-5574-4c66-bf9b-36325bcdac6a.png)

访问web 根据自己的IP访问

[http://192.168.0.166:16010/master-status](http://192.168.0.166:16010/master-status)

（之前的端口是60010  根据版本自行选择端口访问）

---

## **3、完全分布模式：**

伪分布模式需要用到hadoop文件系统 ，所以配置会比单机模式麻烦很多 并且需要版本匹配；我用的

hadoop是2.6.1 hbase是1.1.2；

使用三个节点，分别是   ip:hostname    192.168.0.162    lin162   ,

192.168.0.163    lin163 ,

192.168.0.164    lin164  ；主节点是162

hosts

和 hostname 自己配置 这里不多说；

下面在162上配置：

\(1\)、修改conf/hbase-env.sh

添加java环境变量和hbase\_classpath\(

指向hadoop的配置文件目录

\)环境变量：

```

```

\(2\)、编辑hbase-site.xml

hbase.rootdir 要配置为hdfs上的路径；打开分布

```
<
configuration
>
```

\(3\)、配置regionservers 添加slave

```

```

\(4\)、把hbase scp到lin163 和 lin164

```
$ scp -r /home/lin/hadoop/hbase-1.1.2
lin@192.168.0.163:
/home/lin/hadoop/hbase-1.1.2
$ scp -r /home/lin/hadoop/hbase-1.1.2
lin@192.168.0.164:
/home/lin/hadoop/hbase-1.1.2
```

\(5\)、在主节点lin162启动hbase

```
$  
bin/start-hbase.sh
```

\(6\)、验证是否成功

在主节点lin162 jps 出现  Hmaster 和 HquorumPeer

![](http://img.blog.csdn.net/20151028104051400?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

![](file:///D:/Documents/我的文档/My Knowledge/temp/18259326-abfc-4825-b9ca-b3e8868dedc3.png)

在slave lin163 和 164 jps 出现  HregionServer 和 HquorumPeer

![](http://img.blog.csdn.net/20151028104100964?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

![](file:///D:/Documents/我的文档/My Knowledge/temp/17136c0a-f115-4ecf-b2a7-611b47fb179d.png)

然后就可以hbase shell  进入shell进行对hbase的操作。

