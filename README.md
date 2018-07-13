# KSQL-IDE

KSQL查询结果图形化展示项目

## 什么是KSQL

[KSQL](https://www.confluent.io/product/ksql/)可以通过编写SQL语句的方式去执行kafka的[stream api](https://kafka.apache.org/documentation/streams/)所做的查询，分析，聚合等操作。使用KSQL，可以降低流式处理的门槛。

一般来说，为处理Kafka里的数据，我们需要coding，调用kafka的stream api，而这部分工作往往需要不少的时间来编写和调试程序。
而这个方案的问题在于对于数据分析师来说，也许想到了一个数据分析方案，需要马上来做验证，显然编程所花的时间太多了，而且分析师们的查询大多是随机的(ad-hoc)，于是我们需要一个轻量级，马上能直观的看到结果的工具，那么KSQL就可以轻而易举的做到这一点。

### KSQL适用于什么？

- 实时监控，实时分析
- 实时安全和异常检测
- 实时数据的连接聚合查询

### KSQL的语法

详情见[KSQL Reference](https://docs.confluent.io/current/ksql/docs/syntax-reference.html)

## 什么是KSQL-IDE

- [测试环境](http://ksql-ide-staging.guazi-cloud.com/home)
- [生产环境](http://ksql-ide.guazi-apps.com/home)

目前来说，KSQL还在飞速的发展中，其本身只提供了一个默认的控制台终端，使用起来成本太高，依赖过多，编写SQL时有诸多不便，为此我们开发了一套工具来管理KSQL及其依赖，通过web提供一种更加便捷、高效的方式来使用KSQL，同时也提供了一些对Kafka的相关功能操作的封装。

### KSQL-IDE的功能

- [直接在web页面上编写执行SQL](/guide/ksql-ui.md)
- 历史SQL的管理
- ad-hoc查询的图形化展示(*)
- 提交SQL到测试，线上环境(*)
- [topic的数据的查看、发送](/guide/topic.md)

TOPICS查看界面主要提供"了解详情、获取schema信息、查看罪行数据和发送测试数据"的功能。了解详情是获取指定topic的元数据信息，返回一个json数据，主要包括 name、configs、partitions。在每个partition显示所属分区信息、broker ID、分区副本列表等信息。获取schema功能可以将每个topic的schema信息展示出来，可以很清晰的了解注册schema数据的格式。查看最新数据功能提供了指定topic的消息队列消费每一条消息的基本信息，包括所属partition、key、offset和真实消费数据。在这个功能里提供了一个开关键，打开点解接收最新数据时，如果有生产者产生数据就可以看到消费生产的数据，如果关闭接收最新数据，即使有新的数据产生也无法消费。发送测试数据功能，主要向指定tipic发送测试数据，所发送的测试数据必需也topic的schema格式相匹配，否则会报错。在填写发送数据的时候，提供了三种方式：直接写Json数据、表单填写数据和vue-json-editor组件生成数据，这三种方式都可以发送测试数据。
- topic数据同步到elastic(*)
- schema的查看

## Table and Stream 

- [描述](/guide/table-stream.md)

## 权限控制

为了避免在测试阶段产生大量topic，所以加入了权限控制。用户可以基于topic创建STREAM和TABLE，然后通过执行查询(SELECT)语句实现连接、聚合、时间窗口等业务需求，但是不能够将结果回写到kafka的topic。也就是说没有“CREATE STREAM/TABLE AS SELECT ...”的权限。

## 附录

[stream platform](http://cwiki.guazi-corp.com/display/xn/Stream+Platform)
