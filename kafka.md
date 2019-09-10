##kafka

###partion分区

同一groupid对同一topic，只能有一个消费，即：两个consumer，group相同，都订阅topic为test的消息，那一条消息如果被consumer1消费了，则consumer2不会再消费

如果group不同，对同一topic，多个consumer都会消费，即：两个consumer3，consumer4，group不相同，但都订阅topic为test的消息，那么consumer3和4都可以消费到test的消息。



ProduceConfig有个batch.size参数，就是消息达到一定量进行批量发送，如果一直打不到设定的那个量呢？比如batch.size=100，producer只累积了80条就没产生新消息了，这时还有一个参数LINGER_MS_CONFIG达到指定时间就进行发送。



producer的topic发到哪个partition，根据key进行随机算法的选择。

##rebalance：

* 当分区数发生变化
* 消费者数量发生变化



策略

* Ranage

* RoundRobin

* Stricky

  尽可能均匀



kafka里默认会创建一个topic，分区数50

* __consumer_offset_partitionid

  

coordinate



leader epoch  (epoch,offset)



零拷贝：

~~~sequence
a.xx,x
~~~









rabbitMQ

exchange交换机类型：

* Direct直连   binding key绑定键，routing key路由键
* topic主题类型，绑定键可以使用通配符  #  0个或者多个单词，*  不多不少一个单词   
* 广播类型交换机，不需要路由键  



TTL

死信队列：

1、消息被消费者拒绝

2、消息过期

3、队列到达最大长度

死信队列的作用：

延迟队列的总体方案



rabbitmq-delayed-message-exchange的实现





服务端流控

x-max-length

x-max-length-bytes



prefetch count 

Spring AMQP



#消息可靠性投递

服务端确认机制

* Transaction模式  channel.txSelect();channel.txCommit();channel.txRollback();
* confirm模式channel.confirmSelect();    channel.waitForConfirms();
* 批量确认模式channel.confirmSelect();   channel.waitForConfirmsOrDie();只要没有抛出异常
* 异步确认channel.addConfirmListener();



无法路由的消息   mandatory= true+returnBack

持久化

队列持久化~

交换机持久化

消息持久化

集群持久化



$fff $

$44444$$bbbbbb$



自动ACK

接收到消息就ACK还是执行方法的末尾ACK，答案是接收到消息就发送ACK

手动ACK



AcknowledgeMode，NONE，MANUAL，AUTO

AmqpRejectAndRequeueException

AmqpRejectAndDontRequeueException



生产者怎么才能知道消费者消费了消息

1.消费者调用生产者自定义的API

2.消费者给生产者应答一条消息



ZABBIX



Firehose记录日志流入流出

Tracing GUI

面试题分析：

消息队列的作用和使用场景

channel和vhsot的作用是什么：channel减少tcp连接

vhsot提示硬件资源利用率和资源隔离

有哪些路由方式？使用的业务场景是什么？

DIRECT，TOPIC（过滤），FANOUT（广播类型，通用信息）

交换机与队列，队列与消费者的绑定关系：

多对多。一条消息只能被一个消费者消息

队列：消费  1对多？轮询（prefetch count）



无法路由的消息，去了哪里？

1.直接丢弃

2.回发

3.备份



消息在什么时候会变成DeadLetter（死信）

1.消息过期

2.超过队列容量

3.消费者：reject Nack request



![1566741834514](C:\Users\ADMINI~1\AppData\Local\Temp\1566741834514.png)

多个ConnectionFactory   template  ListenerContainer



如何实现延迟队列

* 登记数据库，定时任务扫描
* TTL死信队列，被监听了死信队列的消费者拿到
* 插件



哪些情况会导致消息丢失，怎么解决？





一个队列最多可以存放多少条消息

存放在内存还是磁盘

取决于硬件配置，还有x-max-length和。





如何提高消息的消费速率？

 增加消费者



如何动态的创建队列和消费者





如何保证消息的顺序性？

那就一个队列只配一个消费者



大量消息堆积怎么办？





![1566742714194](C:\Users\ADMINI~1\AppData\Local\Temp\1566742714194.png)







设计一个MQ

