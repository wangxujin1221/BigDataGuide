# BigDataGuide
### 查询/搜索/分析引擎

+ **[深入理解Presto](https://zhuanlan.zhihu.com/p/101366898)** 

+ **[ Impala](https://zhuanlan.zhihu.com/p/87020775)**

  **实时SQL查询引擎Impala**可以直接从HDFS或HBase中用SELECT、JOIN和统计函数查询数据，在众多大数据框架中，Impala定位类似Hive，不过Impala更关注即席查询SQL的快速解析，对于执行时间过长的SQL，仍旧是Hive更合适。对于GroupBy等SQL查询，Impala进行的是内存计算，因而Impala对机器配置要求较高，官方建议内存128G以上，此类问题Hive底层对应的是传统的MapReduce计算框架，虽然执行效率低，但是稳定性好，对机器配置要求也低。Impala本身不提供数据的存储服务，其底层数据可来自HDFS、Kudu、Hbase甚至亚马逊S3。

  impala和kudu集成：https://blog.csdn.net/qq_35741557/article/details/82690607

+ **Pig**

  是一个基于Hadoop的大规模数据分析工具，它提供的SQL-LIKE语言叫Pig Latin，该语言的编译器会把类SQL的数据分析请求转换为一系列经过优化处理的MapReduce运算。

+ **ElasticSearch**

+ **Solr**

+ **apache lucence**

### 流程调度

+ **Yarn**

  构建与hadoop之上的资源管理和job调度框架。yarn负责给运行在hadoop上的任务分配资源，以及设置任务运行的节点。

+ **Oozie**

+ **Dolphin Schedule** https://dolphinscheduler.apache.org/

+ **Azkaban** 

### 文件系统

+ **HDFS**
+ **S3**
+ **NFS**

### 数据库/数据仓库/数据湖

+ **HBase**

+ **[Hudi](https://hudi.apache.org/)**  https://hudi.apache.org/docs

  **数据湖和数据仓库** https://searchaws.techtarget.com/definition/data-lake ; https://www.zhihu.com/question/279097731

+ **Hive**

  是基于Hadoop的一个数据仓库工具，可以将结构化的数据文件映射为一张数据库表，通过类SQL语句快速实现简单的MapReduce统计，不必开发专门的MapReduce应用，十分适合数据仓库的统计分析。

+ **[Kudu](http://kudu.apache.org/)** 

  Kudu的大部分场景和Hbase类似，其设计降低了随机读写性能，提高了扫描性能，在大部分场景下，Kudu在拥有接近Hbase的随机读写性能的同时，还有远超Hbase的扫描性能。相比HDFS+Parquet+Impala的传统架构，Kudu+Impala在绝大多数场景下拥有更好的性能。kudu在某些特性上和Hbase很相似，难免会放在一起比较。然而Kudu和Hbase有如下两点本质不同。

  + Kudu的数据模型更像是传统的关系型数据库，Hbase是完全的no-sql设计，一切皆是字节。
  + Kudu的磁盘存储模型是真正的列式存储，Kudu的存储结构设计和Hbase区别很大。
    综合而言，纯粹的OLTP请求比较适合Hbase，OLTP与OLAP结合的请求适合Kudu。

+ **[Amazon's Dynamo](https://www.allthingsdistributed.com/2007/10/amazons_dynamo.html)**

  亚马逊提供的高可用的key-value存储系统

+ **Druid** https://druid.apache.org/docs/latest/design/index.html

  阿里开源的实时分析数据库，面向大数据集合OLAP的实时查询分析。

  https://www.jianshu.com/p/6f822e0f538c

+ **Neo4j** https://www.cnblogs.com/huangwentian/p/14448399.html

+ **ArangoDB** https://www.jianshu.com/p/d86b0fddea0e

+ **Datahub**(阿里云) https://help.aliyun.com/document_detail/158841.html

+ **Janus** 

### 计算框架

+ **Spark**

+ **Flume**

  是一个分布的、可靠的、高可用的海量日志聚合的系统，可用于日志数据收集，日志数据处理，日志数据传输。

+ **Storm**

+ **Flink** 

+ **MapReduce**

### 配置管理

+ **Apollo** 

  分布式配置中心

+ **服务发现机制SPI（Service Provider Interface）** https://www.jianshu.com/p/3a3edbcd8f24 

+ **Swagger** https://www.jianshu.com/p/349e130e40d5

  Swagger 是一个规范且完整的框架，用于生成、描述、调用和可视化 RESTful 风格的 Web 服务。

  - 支持 API 自动生成同步的在线文档
  - 提供 Web 页面在线测试 API：光有文档还不够，Swagger 生成的文档还支持在线测试。参数和格式都定好了，直接在界面上输入参数对应的值即可在线测试接口

### RPC和序列化

+ **什么是RPC？** https://www.jianshu.com/p/7d6853140e13

  **RPC**就是为了解决 **不同服务之间的调用问题**, 它一般会包含有 **传输协议** 和 **序列化协议** 这两个。

+ **Avro **

  是Apache下的一个数据序列化系统，设计用于支持数据密集型，大批量数据交换的应用。Avro是新的数据序列化格式与传输工具，将逐步取代Hadoop原有的IPC机制

+ **Hessian**

+ **Thrift** https://www.cnblogs.com/cyfonly/p/6059374.html https://www.jianshu.com/p/346910faefe7?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation

  一个高效的RPC框架，提供序列化协议来实现数据在客户端和服务端之间的传输。通过read和write方法实现序列化和反序列化

  测试遇到问题：org.apache.thrift.transport.TTransportException: java.net.ConnectException: Connection refused: connect

  两种原因：1.服务端进程未启动（先于客户端启动）；2.端口未启用

### 文件格式

+ **Record Columnar File RC File**
+ **Optimized Record Columnar ORC**
+ **Parquet** https://blog.csdn.net/yu616568/article/details/50993491

### 权限管理

+ **Kerberos**[/ˈkərbərəs/https://www.cnblogs.com/artech/archive/2007/07/05/807492.html https://web.mit.edu/kerberos/www/dialogue.html

  网络授权协议 kerberos是支持单点登录的，一次鉴权就可以访问多个服务

+ **Apache Ranger** https://ranger.apache.org/ https://blog.csdn.net/qq475781638/article/details/90247153

  用于hadoop平台之上，实现全面的启用、监控、管理数据安全。Apache Ranger提供一个集中式安全管理框架, 并解决授权和审计。它可以对Hadoop生态的组件如HDFS、Yarn、Hive、Hbase等进行细粒度的数据访问控制。通过操作Ranger控制台,管理员可以轻松的通过配置策略来控制用户访问权限。

  支持的组件：

  - [Apache Hadoop HDFS](https://www.cloudera.com/products/open-source/apache-hadoop/hdfs-mapreduce-yarn.html)
  - [Apache Hive](https://www.cloudera.com/products/open-source/apache-hadoop/apache-hive.html)
  - [Apache HBase](https://www.cloudera.com/products/open-source/apache-hadoop/apache-hbase.html)
  - Apache Storm
  - [Apache Knox](https://www.cloudera.com/products/open-source/apache-hadoop/apache-knox.html)
  - Apache Solr
  - [Apache Kafka](https://www.cloudera.com/products/open-source/apache-hadoop/apache-kafka.html)
  - [Apache NiFi](https://www.cloudera.com/products/open-source/apache-hadoop/apache-nifi.html)
  - [YARN](https://www.cloudera.com/products/open-source/apache-hadoop/hdfs-mapreduce-yarn.html)

  还可以安装es，presto，kylin，sqoop插件

+ **Apache Sentry** https://blog.csdn.net/qq475781638/article/details/90247153

+ **AK/SK** 公有云API的认证方式 https://blog.csdn.net/makenothing/article/details/81158481

### 重要算法

+ **Raft协议**

  https://juejin.cn/post/6907151199141625870

  http://thesecretlivesofdata.com/raft/ 动画演示

+ **ZAB协议**

+ **Paxos协议**

+ **Work Stealing算法**

  java并发中使用的Fork/Join框架中使用到了这种算法。Work-Stealing 的适用场景是不同的任务的耗时相差比较大，即某些任务需要运行较长时间，而某些任务会很快的运行完成，这种情况下用 Work-Stealing 很合适；但是如果任务的耗时很平均，则此时 Work-Stealing 并不适合，因为窃取任务时不同线程需要抢占锁，这可能会造成额外的时间消耗，而且每个线程维护双端队列也会造成更大的内存消耗。所以 `ForkJoinPool` 并不是 `ThreadPoolExecutor` 的替代品，而是作为对 `ThreadPoolExecutor` 的补充。

  https://segmentfault.com/a/1190000008140126

  https://www.baeldung.com/java-work-stealing

### 名词概念

+ **原语** https://blog.csdn.net/qq_34612223/article/details/109668692

+ **Daas数据即服务** https://blog.csdn.net/jinseshanguang/article/details/84321742

+ **MVCC** https://www.cnblogs.com/liulvzhong/articles/9242299.html https://www.jianshu.com/p/8845ddca3b23

+ **LDAP** 轻型目录访问协议https://www.cnblogs.com/wilburxu/p/9174353.html

+ **JAAS** java验证和授权服务

+ **Exactly-once** 

  confluent.io/blog/exactly-once-semantics-are-possible-heres-how-apache-kafka-does-it/

+ **消息队列中的topic/queue** https://www.cnblogs.com/lemon-flm/p/7676047.html

+ **Serverless架构** https://www.jdon.com/soa/serverless.html

  Serverless不代表再也不需要服务器了，而是说：开发者再也不用过多考虑服务器的问题，计算资源作为服务而不是服务器的概念出现。Serverless是一种构建和管理基于微服务架构的完整流程，允许你在服务部署级别而不是服务器部署级别来管理你的应用部署，你甚至可以管理某个具体功能或端口的部署，这就能让开发者快速迭代，更快速地开发软件。

### 其它

+ -**javaagent** 热部署的实现方式 https://www.cnblogs.com/rickiyang/p/11368932.html https://www.jianshu.com/p/63c328ca208d

  https://www.jianshu.com/p/b72f66da679f

+ **信号处理方式**  https://www.jianshu.com/p/3cb9aacc26a2

+ **Cassandra的各种key说明** https://www.baeldung.com/cassandra-keys 

+ **数据透传** https://blog.csdn.net/chenlycly/article/details/7391038

### 其它组件

+ **Netty**

  Netty就是基于Java NIO技术封装的一套框架。为什么要封装，因为原生的Java NIO使用起来没那么方便，而且还有臭名昭著的bug，Netty把它封装之后，提供了一个易于操作的使用模式和接口，用户使用起来也就便捷多了

+ **Sqoop**

  是一个用来将Hadoop和关系型数据库中的数据相互转移的工具，可以将一个关系型数据库（MySQL ,Oracle ,Postgres等）中的数据导进到Hadoop的HDFS中，也可以将HDFS的数据导进到关系型数据库中。

+ **ODPS（MaxCompute） **https://help.aliyun.com/document_detail/27800.html

  开发数据处理服务(Open Data Processing Service，简称ODPS)，2016年后更名MaxComputer。ODPS是一种由阿里云自主研发，针对TB/PB级数据、实时性要求不高的分布式处理服务。主要服务于批量结构化数据的存储和计算，可以提供海量数据仓库的解决方案以及针对大数据的分析建模服务。

+ **Apache Knox Gateway**

  是用于与Apache Hadoop部署的RESTAPI和UI交互的应用程序网关。Knox Gateway为与Apache Hadoop集群的所有REST和HTTP交互提供一个单一的访问点。KNOX提供三组面向用户的服务：

　　　　代理服务：Apache Knox项目的主要目标是通过代理HTTP资源提供对Apache Hadoop的访问。

　　　　认证服务：对USTAPI访问以及UIS的WebSSO流进行身份验证。LDAP/AD，基于头的PROAUTH，Kerberos，SAML，OAUTH都是可用的选项。

　　　　客户服务：可以通过DSL编写脚本或直接将Knox Shell类作为SDK来完成客户端开发。

+ **Apache NiFi**

  Apache NiFi 可在不同的数据源和系统之间自动移动数据，从而使数据摄取快速、轻松。Apache NiFi 是一个集成的数据物流平台，用于自动化不同系统之间的数据移动。它提供实时控制，可以轻松管理任何来源和任何目的地之间的数据移动。

+ **Apache HttpComponents**  http://hc.apache.org/index.html

  基于http和相关协议创建和维护的基于java的工具集

  
