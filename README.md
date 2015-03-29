# Kafka

# Traditional Queue
Problems
```
 - Scalable
 - Parallism
 - Availability
 - Data reply
 ```
## Kafka

Topics and partitions

1 Topic with n partitions

producer writes to topic (partition)
consumer read from topic (partition)

topic will have a retension policy on time and data space

#Attributes required to create topic

```
Partition
Replica
Name
```

Kafka does not guarantee a order across the partitions
In terms of consumer, offset is an index
saving is offset is called check pointing

```
Kafka maintains feeds of messages in categories called topics.
We'll call processes that publish messages to a Kafka topic producers.
We'll call processes that subscribe to topics and process the feed of published messages consumers..
Kafka is run as a cluster comprised of one or more servers each of which is called a broker.



producer
  | | |
Kafka Server     } Zookeeper to maintain the state
  | | |
Consumer  

```

# Two features

```
Mirroring
Camus
```
http://kafka.apache.org/documentation.html#quickstart

Tasks
```
- Setup Kafka
- Perform in and out
- Java API for producer
```


#Useful Commands

Start Zookeeper

```
arun:kafka arun$ bin/zookeeper-server-start.sh config/zookeeper.properties

```

Start Kafka Server 1

```
bin/kafka-server-start.sh config/server.properties
```

Start Kafka Server 2

```
bin/kafka-server-start.sh config/server-1.properties
```

Start Kafka Server 3

```
bin/kafka-server-start.sh config/server-2.properties
```

Create a topic and send message using producer

```
bin/kafka-console-producer.sh --zookeeper localhost:2181 --topic test
```
