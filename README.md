# homework8

### 简述为什么会有Spark
#### 1.Spark基于内存计算思想提高计算性能，运行速度远远高于Hadoop。Spark提出了一种基于内存的弹性分布式数据集(RDD)，通过对RDD 的一系列操作完成计算任务，可以大大提高性能；同时一组RDD形成可执行的有向无环图DAG，构成灵活的计算流图；Spark覆盖了多种计算模式。
#### 2.Spark易于使用，支持多语言。Spark允许Java、Scala及Python，这允许开发者在自己熟悉的语言环境下进行工作。它自带了80多个高等级操作符，允许在shell中进行交互式查询。
#### 3.Spark支持复杂查询。在简单的“map”及“reduce”操作之外，Spark还支持SQL查询、流式查询及复杂查询。
#### 4.Spark可以与Hadoop和已存Hadoop数据整合。Spark可以独立的运行，除了可以运行在当下的YARN集群管理之外，它还可以读取已有的任何Hadoop数据。它可以运行在任何Hadoop数据源上，比如HBase、HDFS等。这个特性让用户可以轻易迁移已有Hadoop应用。

### 对比Hadoop和Spark
#### 1.Spark把中间数据放在内存中，迭代运算效率高； MapReduce中计算结果需要落地，保存到磁盘上。Spark支持DAG图的分布式并行计算，减少了迭代过程中数据的落地，提高了处理效率。 
#### 2.Spark容错性高。MapReduce使用TaskTracker节点，它为JobTracker节点提供了心跳(heartbeat)。如果没有心跳，那么JobTracker节点重新调度所有将执行的操作和正在进行的操作，交给另一个TaskTracker节点。这种方法在提供容错性方面很有效，可是会大大延长某些操作(即便只有一个故障)的完成时间。而Spark引入了RDD的抽象，它是分布在一组节点中的只读对象集合，这些集合是弹性的。在RDD计算时可以通过CheckPoint来实现容错，而CheckPoint有两种方式：CheckPoint Data和Logging The Updates。
#### 3.Spark更加通用。Hadoop只提供了Map和Reduce两种操作， Spark提供的数据集操作类型很多。另外各个处理节点之间的通信模型不再像Hadoop只有Shuffle一种，用户可以命名、物化、控制中间结果的存储、分区等。

### 简述Spark的技术特点
#### 1.RDD：Spark提出的弹性分布式数据集，是Spark最核心的分布式数据抽象，Spark的很多特性都和RDD密不可分。 
#### 2.Transformation & Action：Spark通过RDD的两种不同类型的运算实现了惰性计算，即在RDD的Transformation运算时，Spark并没有进行作业的提交；而在RDD的Action操作时才会触发SparkContext提交作业。
#### 3.Lineage：为了保证RDD中数据的鲁棒性，Spark系统通过血统关系(lineage)来记录一个RDD是如何通过其他一个或者多个父类RDD转变过来的， 当这个RDD的数据丢失时，Spark可以通过它父类的RDD重新计算。 
#### 4.Spark调度：Spark采用了事件驱动的Scala库类Akka来完成任务的启动，通过复用线程池的方式来取代MapReduce进程或者线程启动和切换的开销。
#### 5.API：Spark使用Scala语言进行开发，并且默认Scala作为其编程语言。因此，编写Spark程序比MapReduce程序要简洁得多。同时，Spark系统也支持Java、Python语言进行开发。
#### 6.Spark生态：Spark SQL、Spark Streaming、 GraphX等为Spark的应用提供了丰富的场景和模型，适合应用于不同的计算模式和计算任务。
#### 7.Spark部署：Spark拥有Standalone、Mesos、 YARN等多种部署方式，可以部署在多种底层平台上。
#### 8.适用于需要多次操作特定数据集的应用场合。 需要反复操作的次数越多，所需读取的数据量越大，受益越大，数据量小但是计算密集度较大的场合，受益就相对较小。
#### 9.由于RDD的特性，Spark不适用那种异步细粒度更新状态的应用，例如web服务的存储或者是增量的web爬虫和索引。就是对于那种增量修改的应用模型不适合。
#### 10.适用于数据量不是特别大，但是要求实时统计分析需求。

