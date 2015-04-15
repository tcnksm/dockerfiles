# Apache Kafka

This is Dockerfile for [Apache Kafka](http://kafka.apache.org/). 

To build image,

```bash
$ docekr build -t tcnksm/kafka .
```

To enter container, 

```bash
$ docker run --rm -it tcnksm/kafka /bin/bash
```

## Basic

You can try [Quick Start](http://kafka.apache.org/documentation.html#quickstart) in Docker conatainer.

To get a quick-and-dirty single-node ZooKeeper instance,

```bash
$ bin/zookeeper-server-start.sh config/zookeeper.properties &
```

To start kafka server,

```bash
$ bin/kafka-server-start.sh config/server.properties &
```

To create topic,

```bash
$ bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic tcnksm
```

- `--replication-factor` is ...
- `--partitions` is ...

To list topic,

```bash
$ bin/kafka-topics.sh --list --zookeeper localhost:2181
tcnksm
```

To send messages,

```bash
$ bin/kafka-console-producer.sh --broker-list localhost:9092 --topic tcnksm
This is message A
This is message B
```

(`0.0.0.0:9092` is `kafka.network.Acceptor`)


To start consumer,

```bash
$ bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic tcnksm --from-beginning
This is message A
This is message B
```

(We can get this message until broker deletes)

 Multi-brocker tutorial

Prepare configuration, 

```bash
$ cp config/server.properties config/server-1.properties
$ cp config/server.properties config/server-2.properties
```

Edit configuration,

```bash
config/server-1.properties:
    broker.id=1
    port=9093
    log.dir=/tmp/kafka-logs-1
```
    
```bash
config/server-2.properties:
    broker.id=2
    port=9094
    log.dir=/tmp/kafka-logs-2
```

`brocker.id` is the unique and permanent name of each node in the cluster (Need to increment from 0..?)

To start server,

```bash
$ bin/kafka-server-start.sh config/server-1.properties &
$ bin/kafka-server-start.sh config/server-2.properties &
```

To create topic with a replication factor `3`,

```bash
$ bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 3 --partitions 1 --topic my-replicated-topic
```

To describe topic (to see which broker is doing what?),

```bash
$ bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic my-replicated-topic
```

To publish message,

```bash
$ bin/kafka-console-producer.sh --broker-list localhost:9092 --topic my-replicated-topic
my test message 1
my test message 2
my test message 3
```

To consume message,

```bash
$ bin/kafka-console-consumer.sh --zookeeper localhost:2181 --from-beginning --topic my-replicated-topic
```

To check fault-tolerance, kill one broker,

```bash
$ ps aux | grep server-1
$ kill -9 ...
```

Check broker status,

```bash
$ bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic my-replicated-topic
```

To subcribe again,

```bash
$ bin/kafka-console-consumer.sh --zookeeper localhost:2181 --from-beginning --topic my-replicated-topic
```

## Reference

- [https://github.com/spotify/docker-kafka](https://github.com/spotify/docker-kafka)
