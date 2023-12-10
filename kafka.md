# References

https://www.conduktor.io/kafka/how-to-start-kafka-using-docker

# Table of Contents

- [Download](#download)
- [Start](#start)
- [Stop](#stop)
- [Down](#down)
- [Check services are running](#check-services-are-running)
- [Fundamentals](#fundamentals)
  - [Topic](#topic)
    - [Listing all topics](#listing-all-topics)
    - [Create](#create-new-topic)
    - [Delete](#delete-a-topic)
    - [Describe](#describe-a-topic)
    - [Increase partitions](#increase-the-number-of-partitions)
  - [Producer](#producer)
  - [Consumer](#consumer)
  - [Consumer Group](#consumer-group)
    - [Create](#create-new-consumer-group)
    - [Delete](#delete-a-consumer-group)
  - [Group Management](#consumer-group-management)
    - [Listing state](#listing-consumer-groups-state)
    - [Describe](#describe-a-consumer-group)
    - [Reset offsets](#reset-the-offsets)
    - [Delete offsets](#delete-offsets)
  - [Kafka Connect](#kafka-connect)

# Download

```bash
git clone https://github.com/conduktor/kafka-stack-docker-compose.git
```

# Start

```bash
docker-compose -f zk-single-kafka-single.yml up -d
```

# Stop

```bash
docker-compose -f zk-single-kafka-single.yml stop
```

# Down

```bash
docker-compose -f zk-single-kafka-single.yml down
```

# Check services are running

```bash
docker-compose -f zk-single-kafka-single.yml ps
```

# Fundamentals

```bash
docker exec -it kafka1 /bin/bash
```

## Topic

### Listing all topics

```bash
kafka-topics --bootstrap-server localhost:9092 --list
```

### Create new topic

```bash
kafka-topics --bootstrap-server localhost:9092 --create --topic ${TOPIC_NAME}
```

With options

```bash
kafka-topics --bootstrap-server localhost:9092 --create --topic ${TOPIC_NAME} --partitions ${NUMBER} --replication-factor ${NUMBER}
```

### Delete a topic

```bash
kafka-topics --bootstrap-server localhost:9092 --delete --topic ${TOPIC_NAME}
```

### Describe a topic

```bash
kafka-topics --bootstrap-server localhost:9092 --describe --topic ${TOPIC_NAME}
```

- Leader: 1 means that for partition 0, the broker with the ID 1 is the leader.

- Replicas: 1 means that for partition 0, the broker with the ID 1 is a replica.

- Isr: 1 means that for partition 0, the broker with the ID 1 is an in-sync replica.

### Increase the number of partitions

Altering the Kafka topic to have more partitions

```bash
kafka-topics --bootstrap-server localhost:9092 --alter --topic ${TOPIC_NAME} --partitions ${NUMBER}
```

## Producer

With text

```bash
kafka-console-producer --bootstrap-server localhost:9092 --topic ${TOPIC_NAME}
```

With key:value

```bash
kafka-console-producer --bootstrap-server localhost:9092 --topic ${TOPIC_NAME} --property parse.key=true --property key.separator=:
```

From the file

```bash
kafka-console-producer --bootstrap-server localhost:9092 --topic ${TOPIC_NAME} < ${FILE_NAME}.txt
```

## Consumer

Consuming only the future messages of a Kafka topic

```bash
kafka-console-consumer --bootstrap-server localhost:9092 --topic ${TOPIC_NAME}
```

Options:

<!-- Consuming all historical messages and future ones in a Kafka topic -->

--from-beginning

<!-- To display messages in a particular format -->

--formatter: kafka.tools.DefaultMessageFormatter --property print.timestamp=true --property print.key=true --property print.value=true ...

More properties:

- print.partition
- print.offset
- print.headers
- key.separator
- line.separator
- headers.separator

## Consumer Group

### Create new consumer group

```bash
kafka-console-consumer --bootstrap-server localhost:9092 --topic ${TOPIC_NAME} --group ${GROUP_NAME}
```

### Partitioner setting

Custom logic to determine partition based on `key`
The incoming message must be in the form `key:value`, or if it is a string, it must be different from the `key`

### Delete a consumer group

```bash
kafka-consumer-groups --bootstrap-server localhost:9092 --delete --group ${GROUP_NAME}
```

## Consumer Group management

### Listing consumer groups state

```bash
kafka-consumer-groups --bootstrap-server localhost:9092 --list --state
kafka-consumer-groups --bootstrap-server localhost:9092 --describe --all-groups --state
```

### Describe a consumer group

```bash
kafka-consumer-groups --bootstrap-server localhost:9092 --describe --group ${GROUP_NAME}
```

### Reset the offsets

<code>
Using <b>--dry-run</b> to show the expected result, but does not actually run the command
</code>

To the earliest position

```bash
kafka-consumer-groups --bootstrap-server localhost:9092 --topic ${TOPIC_NAME} --group ${GROUP_NAME} --reset-offsets --to-earliest --execute
```

By shifting by ${INTEGER}

```bash
kafka-consumer-groups --bootstrap-server localhost:9092 --topic ${TOPIC_NAME} --group ${GROUP_NAME} --reset-offsets --shift-by ${INTEGER} --execute
```

More options:
--to-datetime
--by-period
--to-latest
--from-file
--to-current

### Delete offsets

Delete offsets for a specific topic (helpful when your consumer group is reading from multiple topics)

```bash
kafka-consumer-groups --bootstrap-server localhost:9092 --topic ${TOPIC_NAME} --group ${GROUP_NAME} --delete-offsets
```

## Kafka Connect

"In order to get data into Apache Kafka, we have seen that we need to leverage Kafka producers. Over time, it has been noticed that many companies shared the same data source types (databases, systems, etc...) and so writing open-source standardized code could be helpful for the greater good. The same thinking goes for Kafka Consumers.

Kafka Connect is a tool that allows us to integrate popular systems with Kafka. It allows us to re-use existing components to source data into Kafka and sink data out from Kafka into other data stores."

---
