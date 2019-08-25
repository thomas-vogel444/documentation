# Kafka Overview

From https://dzone.com/articles/kafka-architecture

## Abstractions

- Records
    - Immutable
    - Have keys (optional), values, timestamps
- Topics
    - Stream of receords
- Consumers
- Consumer Group
    - Multi-threaded or multi machine consumption from Kafka topics
    - One consumer in the consumer group is assigned a consumer group
- Producers
- Brokers
    - Node in a Kafka cluster
- Logs
    - Topic storage on disk
- Partitions
    - Logs are sharded, i.e. broken into partitions and segments
- Cluster
    - A cluster is formed of one or more brokers

## Architecture

Zookeeper manages the cluster of brokers. 
- coordinates the cluster topology. 
- is a consistent file system for configuration information. 
- used for leadership election for broker topics partition leaders
- manages service discovery for Kafka brokers

## Producers, Consumers and Topics

- Producers write to Topics
- Consumers read from Topics
- A topic is associated with a log. Kafka appends records from a producer to the end of a topic log.
- Topic logs are partitioned and spread over all the brokers
- Consumers read topics at their own pace, incrementing an offset

## Topic partition, Consumer, Consumer Group, Offset, and Producers

- Speed
    - Kafka writes to the filesystem sequentially, which is fast (up to 700MB/s).
- Replication
    - You can specify a replication factor for fail-over
    - Use Mirror Maker (from Kafka core) for disaster recovery
        - It replicates a Kafka cluster to another datacentre 







