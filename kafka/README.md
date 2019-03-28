# [kafka-docker](https://github.com/wurstmeister/kafka-docker)

1. 替换KAFKA_ADVERTISED_LISTENERS中的IP为宿主机IP.
> 查看宿主机IP
```script
> hostname -i
192.168.138.110
```

2. 启动zookeeper集群
>https://github.com/xjzrc/docker-compose-file/tree/master/zookeeper

3. 启动kafka集群：docker-compose up -d

4. 进入其中一个broker容器：docker exec -it kafka_broker_0_1 bash

5. 进入kafka安装目录：cd /opt/kafka_2.11-2.0.0

6. 创建kafka主题
> Let's create a topic named "topic1" with a replication factor of three:
```script
> bin/kafka-topics.sh --create --zookeeper zoo1:2181,zoo2:2181,zoo3:2181/kafka --replication-factor 3 --partitions 1 --topic topic1
```
> We can now see that topic if we run the list topic command:
```script
> bin/kafka-topics.sh --list --zookeeper zoo1:2181,zoo2:2181,zoo3:2181/kafka
topic1
```
> Okay but now that we have a cluster how can we know which broker is doing what? To see that run the "describe topics" command:
```script
> bin/kafka-topics.sh --describe --zookeeper zoo1:2181,zoo2:2181,zoo3:2181/kafka --topic topic1
Topic:topic1   PartitionCount:1    ReplicationFactor:3 Configs:
    Topic: topic1  Partition: 0    Leader: 1   Replicas: 1,2,0 Isr: 1,2,0
```

7. 创建一个生产者发送消息
> Run the producer and then type a few messages into the console to send to the server.
```script
> bin/kafka-console-producer.sh --broker-list localhost:9092 --topic topic1
This is a message
This is another message
```

8. 创建一个消费者消费消息
> Start a consumer
```script
> bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic topic1 --from-beginning
This is a message
This is another message
```

9. 查看队列消费进度
> View queue consumption progress
```script
> bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --describe --group consumer-group-id
TOPIC     PARTITION   CURRENT-OFFSET   LOG-END-OFFSET     LAG   CONSUMER-ID     HOST      CLIENT-ID
topic1        1          301441          339135          37694      -            -           -
```
