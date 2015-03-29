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

Java Program for sample producer

```
package hadoop.kafka;

import java.util.*;

import kafka.javaapi.producer.Producer;
import kafka.producer.KeyedMessage;
import kafka.producer.ProducerConfig;
 
public class TestProducer {
    public static void main(String[] args) {
        long events = Long.parseLong(args[0]);
        Random rnd = new Random();
 
        Properties props = new Properties();
        props.put("metadata.broker.list", "localhost:9092,localhost:9093");
        props.put("serializer.class", "kafka.serializer.StringEncoder");
        props.put("partitioner.class", "hadoop.kafka.SimplePartitioner");
        props.put("request.required.acks", "1");
 
        ProducerConfig config = new ProducerConfig(props);
 
        Producer<String, String> producer = new Producer<String, String>(config);
 
        for (long nEvents = 0; nEvents < events; nEvents++) { 
               long runtime = new Date().getTime();  
               String ip = "192.168.2." + rnd.nextInt(255); 
               String msg = runtime + ",www.arun.com," + ip; 
               KeyedMessage<String, String> data = new KeyedMessage<String, String>("page_visits", ip, msg);
               producer.send(data);
        }
        producer.close();
    }
}
```

Output seen using consumer

```
arun:kafka arun$ bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic page_visits --from-beginning
1427661888490,www.arun.com,192.168.2.197
1427661889100,www.arun.com,192.168.2.34
1427661889108,www.arun.com,192.168.2.16
1427661889113,www.arun.com,192.168.2.196
1427661889118,www.arun.com,192.168.2.131
1427662002244,www.arun.com,192.168.2.31
```
