```shell
db.stats()  
{  
    "db" : "test",               #查看的数据库名称  
    "collections" : 19,        #数据库中的集合数  
    "objects" : 119,           #对象的数量  
    "avgObjSize" : 612.4033613445379,   #对象平均大小  
    "dataSize" : 72876,                  #数据大小  
    "storageSize" : 1196032,         #占用存储空间大小  
    "numExtents" : 21,                   #数据库所有集合中的片区计数  
    "indexes" : 21,                         #索引数量  
    "indexSize" : 171696,               #索引大小  
    "fileSize" : 50331648,               #文件大小  
    "nsSizeMB" : 16,                       #数据库命名空间文件的总大小  
    "ok" : 1  
}  
```





```shell
{
    'db': 'DemoFile',  # 代表当前数据库的名称
    'collections': 5,  # 当前数据库中集合的数量
    'views': 0,  # 当前数据库中视图的数量
    'objects': 5, # 当前数据库中所有文档的数量
    'avgObjSize': 5358.4,  # 数据库中文档的平均大小
    'dataSize': 26792.0,  # 当前数据库的数据大小，单位是byte
    'storageSize': 98304.0,  # 当前数据库占用硬盘空间的大小，单位是byte
    'numExtents': 0, #当前数据库中所有集合extents扩展的数量统计
    'indexes': 9,  # 当前数据库中的索引数量
    'indexSize': 147456.0, # 当前数据库中的索引代销，单位是byte
    'fsUsedSize': 12825751552.0,  # 当前mongodb所在的硬盘已经使用的空间大小
    'fsTotalSize': 42140479488.0, #  当前mongodb所在的硬盘总共的空间大小
    'ok': 1.0 # 1表示成功，0表示失败
}
```





# MongoDB 监控工具mongostat和mongotop的使用

这篇文章主要介绍了MongoDB 监控工具mongostat和mongotop的使用方法，帮助大家更好的理解和学习使用MongoDB，感兴趣的朋友可以了解下

  mongodb中自带两个监控的工具，分别是[mongostat](http://www.zzvips.com/article/66899.html)和mongotop，今天我们看看这两个工具的使用方法。

### MONGOSTAT

mongostat工具提供了mongod和mongos的运行状态和数据，可以从mongostat工具的执行结果中获取如下信息：

这里有必要将其中的某些关键列说明一下：

insert、query、update、delete 分别代表每秒的操作次数

getmore代表当前批量查询得到的文档个数，如果查询的文档多，mongodb会自动批量查询

command代表primary和secondary的节点指令个数，如果是在从库上执行，则代表从库执行的命令数据以及复制从库的其他实例的命令执行情况，二者通过|分割。

dirty代表wiretiger存储引擎的缓冲中脏字节的百分比。

used代表已经使用的wiretiger存储引擎缓存比例

flushed对于wiretiger存储引擎，表示触发检查点的次数；对于mmapv1存储引擎，表示当前将数据写入磁盘的次数

vsize：程序应用的虚拟内存大小

res：当前已经使用的物理内存量，单位为mb

qrw：等待读取的文档个数与等待写入的文档个数

arw：正在执行的读取文档个数与正在执行的写入文档个数

net_in|net_out 进出的网络流量

conn：当前连接数

需要注意的是mongostat是一个持续输出的命令，只要我们不手动终止，它会一直运行，输出到屏幕上。

### MONGOTOP

相比mongostat，mongotop输出的内容有限，来看下面的例子：

ns，集合名字

total：读写花费时间(单位是ms)

read：读花费时间

write：写花费时间

mongotop输出的内容表示每个集合的每个表读写情况，它打印了每个库里面读写花费的时长，单位是ms，可以帮助快速定位读写瓶颈。

mongotop这个命令只运行一次，如果想每间隔一段时间，就运行一次，则可以使用：

mongotop 30

这样的写法，可以让mongotop命令每30s运行一次，这样可以持续的检测mongodb的运行状态。

### 除了这两个工具之外，还有一些其他的命令可以查看集群的状态：

 

-  db.serverstatus()
-  db.stats()
-  db.collstats()
-  rs.status()

下面分别解释这几个命令。

**db.serverstatus()**

这条命令会列出mongodb的整体情况，包含主机名字、版本、进程、连续运行时间、连接状态以及操作状态。因为它显示的结果比较长，这里我们只说说常用的几个信息：

```
host：主机名字

version：mongodb版本

process：pid进程号

uptime：主机的运行时间

asserts：mongodb启动后报警的统计数量

connections：mongodb的连接统计信息

network：mongodb的网路情况

storageengine：存储引擎信息

mem：当前使用的内存信息
```

**db.stats（）**

该命令显示的是db的信息，没有server层面的信息，我们解释下下面db的意思。

```
db：代表当前数据库的名称

collections：当前数据库中集合的数量

view：当前数据库中视图的数量

objects：当前数据库中所有文档的数量

avgobjsize：数据库中文档的平均大小

datasize：当前数据库的数据大小，单位是byte

storagesize：当前数据库占用硬盘空间的大小，单位是byte

numextents：当前数据库中所有集合extents扩展的数量统计

indexes：当前数据库中的索引数量

indexsize：当前数据库中的索引代销，单位是byte

fsusedsize：当前mongodb所在的硬盘已经使用的空间大小

fstotalsize：当前mongodb所在的硬盘总共的空间大小

ok：1表示成功，0表示失败
```

**db.coll.stats()**

这个函数返回的是集合的状态信息，由于输出的内容很多，这里我们仅说明重要的几个部分：

```
ns：当前集合的名称

size：当前集合的大小，单位是byte

count：当前集合的文档数量

nindexes：当前集合中索引的数量

totalindexsize：当前集合中所有索引的大小，单位是byte
```

**rs.status()**

这个函数是用来查看副本集中的成员的状态信息，如下：

下面对常用的字段进行描述：

```
set：副本集的名称

date：当前的时间

mystate：当前副本集节点的状态

term：副本集的选举数

syncingto:从哪个副本集同步数据，如果这里是空值，则代表当前副本是primary

syncsourcehost、syncsourceid分别代表同步目标节点的host和id值

heartbeatintervalmills：副本集心
```



- [ref](http://www.zzvips.com/article/162555.html)