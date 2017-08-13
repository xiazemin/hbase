# 几张图看懂列式存储



## 1 为什么要按列存储

列式存储\(Columnar or column-based\)是相对于传统关系型数据库的行式存储\(Row-basedstorage\)来说的。简单来说两者的区别就是如何组织表\(翻译不好，直接抄原文了\)：

Ø  Row-based storage stores atable in a sequence of rows.

Ø  Column-based storage storesa table in a sequence of columns.



下面来看一个例子：

![](http://img.blog.csdn.net/20141115094556515?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)



从上图可以很清楚地看到，行式存储下一张表的数据都是放在一起的，但列式存储下都被分开保存了。所以它们就有了如下这些优缺点：

|  | **行式存储** | **列式存储** |
| :--- | :--- | :--- |
| **优点** | Ø  数据被保存在一起Ø  INSERT/UPDATE容易 | Ø  查询时只有涉及到的列会被读取Ø  投影\(projection\)很高效Ø  任何列都能作为索引 |
| **缺点** | Ø  选择\(Selection\)时即使只涉及某几列，所有数据也都会被读取 | Ø  选择完成时，被选择的列要重新组装Ø  INSERT/UPDATE比较麻烦 |

_注：关系型数据库理论回顾 - 选择\(Selection\)和投影\(Projection\)_

![](http://img.blog.csdn.net/20141115094806194?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)_  
_

_  
_

## 2补充：数据压缩

刚才其实跳过了资料里提到的另一种技术：通过字典表压缩数据。为了方面后面的讲解，这部分也顺带提一下了。

下面中才是那张表本来的样子。经过字典表进行数据压缩后，表中的字符串才都变成数字了。正因为每个字符串在字典表里只出现一次了，所以达到了压缩的目的\(有点像规范化和非规范化Normalize和Denomalize\)

![](http://img.blog.csdn.net/20141115094911562?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  


  


## 3查询执行性能

下面就是最牛的图了，通过一条查询的执行过程说明列式存储\(以及数据压缩\)的优点：

![](http://img.blog.csdn.net/20141115094934319?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  


  


关键步骤如下：

1.     去字典表里找到字符串对应数字\(只进行一次字符串比较\)。

2.     用数字去列表里匹配，匹配上的位置设为1。

3.     把不同列的匹配结果进行位运算得到符合所有条件的记录下标。

4.     使用这个下标组装出最终的结果集。

  




从Dremel和Impala的学习引申出了SQL查询的并行执行问题，于是借此机会深入学习一下关系数据库以及关系代数的并行计算。

## Speedup和Scaleup

Speedup指用两倍的硬件换来一半的执行时间。Scaleup指两倍的硬件换来同等时间内执行两倍的任务。但往往事情不是那么简单，两倍的硬件也会带来其他问题：更多CPU带来的长启动时间和通信开销，以及并行计算带来的数据倾斜问题。

![](http://img.blog.csdn.net/20141213140448636?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  


## 多处理器架构

**共享内存**：任意CPU都能访问任意的内存\(全局共享\)和磁盘。优点是简单，缺点是扩展性差，可用性低。

![](http://img.blog.csdn.net/20141213140549984?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  


**共享磁盘**：任意CPU都能访问任何的磁盘，但是只能访问自己的主存。优点是可用性和扩展性比较好，缺点是实现复杂以及潜在的性能问题。

![](http://img.blog.csdn.net/20141213140602937?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  


**不共享**：任意CPU都只能访问自己的主存和磁盘。优点也是扩展性和可用性，缺点是实现复杂以及复杂均衡。

![](http://img.blog.csdn.net/20141213140525779?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  


**混合型**：系统整体上是shared nothing架构，但结点内部可能是其他架构。这样就混合了多种架构的优点。

![](http://img.blog.csdn.net/20141213140630390?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  


## 数据分区

数据分区的目的就是：让数据库能够并行地读写数据，最大程度地挖掘I/O的潜力。常见的分区算法有：round-robin、范围索引、哈希。

![](http://img.blog.csdn.net/20141213140645937?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  


## 关系运算并行化

**关系代数自身的属性允许关系操作的并行化**。

![](http://img.blog.csdn.net/20141213140607182?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  


并行查询处理主要分为四步：

Ø**翻译**：将关系代数表达式翻译成查询树。

Ø**优化**：重排join顺序，并选择不同join算法来最小化执行开销。

Ø**并行**：将查询树转换成物理操作树，并加载到处理器。

Ø**执行**：并行运行最终的执行计划。

首先将一条SQL语句翻译成查询树。

![](http://img.blog.csdn.net/20141213140619397?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  


然后根据表大小、索引等情况，重新排列join顺序，并选择合适的算法。

![](http://img.blog.csdn.net/20141213140657570?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  


关于join算法，常见的有以下几种：

Ø**Nested Loop join**：思路很简单，相当于两层循环遍历，外层是驱动表，返回满足关联条件的行。适用于驱动表小\(经过条件过滤后\)，而被驱动表上join字段有索引的情况。在两表都很大时效率很差。

for each row R1 in the outer table  
    for each row R2 in the inner table  
        if R1 joins with R2  
            return \(R1, R2\)

Ø**Sort-merge join**：思路也很简单，就是按join字段排序，然后进行归并排序。当join字段存在重复值时，相当于每个重复值形成了一个分区。Join字段是否排序和重复值的多少决定了sort-merge的效率。适用于两表都很大的情况，尤其当join字段上存在聚集索引时\(相当于已经排好序了\)，效率很高。算法主要消耗在磁盘上。

Ø**Hash join**：类似于存在重复值情况时的sort-merge，只不过是人为的使用哈希函数进行分区。思路是扫描小表建立哈希表\(build阶段，小表也叫build表\)，然后逐行扫描大表进行比较\(probe阶段，大表也叫probe表\)。适用于两表都很大又没有索引的情况，限制是只适用于等值连接。算法主要消耗在CPU上。

![](http://img.blog.csdn.net/20141213140802890?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  


此外，对于子查询还有**semi join**和**anti join**等算法。



最后将查询树变成物理操作树，也就是真正的执行计划。然后根据集群的资源情况，调度到合适的结点上进行并行计算。

![](http://img.blog.csdn.net/20141213140725385?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGNfNzI2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  


## 参考资料

1 Parallel Query Processing

  


  


五大存储模型



昨天跟一同事讨论Sybase是不是关系型数据库，同事说Sybase是列式存储，应该属于NoSQL，我一直的记忆Sybase是关系型数据库，后来专门去查了资料，才发现同事所说的Sybase IO是列式存储;而我说的是Sybase SQL Server，是关系型数据库。网上看到这篇文章，算是对几种数据库模型补补课。

数据库市场需要细分，行式数据库不再满足所有的需求，而有很多需求需要通过本内存数据库和列式数据库解决，列式数据库在数据分析、海量存储、BI这三个领域有自己独到。

## 1. 关系型数据库\(行式数据库\) MySQL Sybase Oracle

定义：关系模型使用记录（行或者元祖）进行存储，记录存储在表中，表由架构界定。表中的每个列都有名称和类型，表中的所有记录都要符合表的定义。SQL是专门的查询语言，提供相应的语法查找符合条件的记录，如表联接（Join）。表联接可以基于表之间的关系在多表之间查询记录。

存储格式：行式数据库把一行中的数据值串在一起存储起来，然后再存储下一行的数据，以此类推。

例如以下的一个表：



| EmpId | Lastname | Firstname | Salary |
| :--- | :--- | :--- | :--- |
| 1 | Smith | Joe | 40000 |
| 2 | Jones | Mary | 50000 |
| 3 | Johnson | Cathy | 44000 |



  
  


> ```
> 1,Smith,Joe,40000;2,Jones,Mary,50000;3,Johnson,Cathy,44000;
> ```

特点：据以行相关的存储体系架构进行空间分配，主要适合与小批量的数据处理，常用于联机事务型数据处理。不能满足后面三个需求：对数据库高并发读写要求，对海量数据的高效率存储和访问需求，对数据库高可扩展性和高可用性。 一句话不适合分布式、高并发和海量。

## 2. 列式存储 Sybase IQ, C-Store, Vertica，Hbase

定义：什么是列式数据库?列式数据库是以列相关存储架构进行数据存储的数据库。列式存储以流的方式在列中存储所有的数据，主要适合与批量数据处理和即席查询。

存储格式 ：

列式数据库把一列中的数据值串在一起存储起来，然后再存储下一列的数据，以此类推。

> ```
> 1,2,3;Smith,Jones,Johnson;Joe,Mary,Cathy;40000,50000,44000;
> ```

特点：包括查询快，由于查询需要读取的blocks少；数据压缩比高，正因为同一类型的列存储在一起。Load快。 简化数据建模的复杂性。但是插入更新慢，不太适合数据老是变化，它是按列存储的。这时候你就知道它适做DSS（决策支持系统），BI的优秀选择，数据集市，数据仓库，它不适合OLTP。

Examples are Sybase IQ, C-Store, Vertica, VectorWise,MonetDB, ParAccel, and Infobright.

具体请参考如下地址:http://en.wikipedia.org/wiki/Column-oriented\_DBMS.

## 3. 键值存储 Cassandra, Hbase, Bigtable

即Key-Value存储，简称KV存储。它是NoSQL存储的一种方式。它的数据按照键值对的形式进行组织，索引和存储。KV存储非常适合不涉及过多数据关系业务关系的业务数据，同时能有效减少读写磁盘的次数，比SQL数据库存储拥有更好的读写性能。

典型例子 Sorted String Table即SSTable。其实STL 库中map和hash\_map, JAVA中hash\_table, hash\_map就是键值存储。 但是他们值只支持内存操作，而且map的查询效率太低，关键是他们只是简单的数据结构，不能实现较大规模存储和分布式,而且数据的修改效率比较低。 而SSTalbe就解决了这些问题。

键值存储实际是分布式表格系统的一种。

分布式key-value 系统有cassandra, hbase, bigtable etc

注：其实Hbase也属于列式存储

## 4. 文档存储

文档存储支持对结构化数据的访问，不同于关系模型的是，文档存储没有强制的架构。

事实上，文档存储以封包键值对的方式进行存储。在这种情况下，应用对要检索的封包采取一些约定，或者利用存储引擎的能力将不同的文档划分成不同的集合，以管理数据。

与关系模型不同的是，文档存储模型支持嵌套结构。例如，文档存储模型支持XML和JSON文档，字段的“值”又可以嵌套存储其它文档。文档存储模型也支持数组和列值键。

与键值存储不同的是，文档存储关心文档的内部结构。这使得存储引擎可以直接支持二级索引，从而允许对任意字段进行高效查询。支持文档嵌套存储的能力，使得查询语言具有搜索嵌套对象的能力，XQuery就是一个例子。MongoDB通过支持在查询中指定JSON字段路径实现类似的功能。

MongoDB 对SQL 和ACID 支持的比较全面的数据库了。不过， 比较多的还是介绍日志的采集和存储，小文件的分布式存储，类似互联网微博应用的数据存储等方面的内容。



## 5.图形数据库

图形数据库存储顶点和边的信息，有的支持添加注释。

图形数据库可用于对事物建模，如社交图谱、真实世界的各种对象。IMDB（Internet MovieDatabase）站点的内容就组成了一幅复杂的图像，演员与电影彼此交织在一起。

图形数据库的查询语言一般用于查找图形中断点的路径，或端点之间路径的属性。Neo4j是一个典型的图形数据库。

