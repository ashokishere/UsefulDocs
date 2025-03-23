What is Apache Kafka?

Apache Kafka is an open-source distributed event streaming platform developed by the Apache Software Foundation. Originally created by LinkedIn, 
it was open-sourced in early 2011. Kafka is designed to handle real-time data feeds, enabling organizations to build robust, scalable, and fault-tolerant data pipelines.

##  Core Components of Apache Kafka

Producer: Producers are applications that send records to Kafka topics. They are responsible for choosing which partition within the topic the record should be sent to.

Consumer: Consumers are applications that read records from Kafka topics. Consumers subscribe to topics and process the messages in real time.

Broker: A Kafka broker is a server that runs Kafka. Brokers receive messages from producers, store them on disk, and serve them to consumers. A Kafka cluster consists of multiple brokers to ensure load balancing and fault tolerance.

Topic: A topic is a logical channel to which producers send records and from which consumers read. Topics are partitioned for scalability and parallelism.

Partition: Each topic is divided into partitions, which are ordered, immutable sequences of records. Partitions allow Kafka to scale horizontally and maintain the order of records within each partition.

ZooKeeper: Kafka uses Apache ZooKeeper for distributed coordination, configuration management, and leader election for Kafka brokers and topics.

## Kafka Architecture

Kafka's architecture revolves around topics, partitions, and brokers. Here's a breakdown of the key architectural elements:

Topics and Partitions: Topics are divided into partitions, which are the fundamental unit of parallelism and scalability in Kafka. Each partition is an ordered, immutable sequence of records,
and each record within a partition is assigned a unique offset. Partitions enable Kafka to scale by distributing data and load across multiple brokers.

Producers and Consumers: Producers write data to Kafka topics, and consumers read data from topics. Kafka supports a publish-subscribe model where multiple consumers can subscribe to the
same topic and process the data independently.

Brokers and Clusters: Kafka brokers are responsible for storing and serving data. A Kafka cluster consists of multiple brokers, which ensures fault tolerance and high availability. Brokers are distributed across different machines to prevent data loss in case of hardware failures.

ZooKeeper Coordination: ZooKeeper manages the configuration and coordination of Kafka brokers. It helps in leader election for partitions and keeps track of broker metadata. However, newer versions of Kafka (starting from version 2.8) are moving towards removing ZooKeeper dependency with the introduction of the KRaft mode.

## Kafka's Role as a Distributed Streaming Platform

Apache Kafka serves as a distributed streaming platform with a broad range of applications. Here are some of its key roles:

Real-Time Data Ingestion: Kafka is widely used for ingesting real-time data from various sources such as logs, sensors, and user interactions. It provides a scalable and fault-tolerant way to collect and store large volumes of data.

Stream Processing: Kafka integrates seamlessly with stream processing frameworks like Apache Flink, Apache Spark, and Kafka Streams. This allows organizations to process and analyze data in real time, enabling use cases like fraud detection, recommendation engines, and monitoring.

Data Integration: Kafka acts as a central hub for data integration, enabling the movement of data between different systems and applications. It supports connectors for various data sources and sinks, making it easy to build data pipelines.

Event Sourcing: Kafka is used for event sourcing, where state changes in an application are logged as a sequence of events. This approach provides a reliable and auditable way to track changes over time.

Message Queue: Kafka can function as a distributed message queue, enabling asynchronous communication between different parts of an application. It supports decoupling of producers and consumers, which enhances the scalability and resilience of applications.

Log Aggregation: Kafka is commonly used for log aggregation, where logs from multiple services are collected, centralized, and processed. This helps in monitoring, troubleshooting, and gaining insights from log data.

Metrics Collection and Monitoring: Kafka can be used to collect and aggregate metrics from various systems, enabling real-time monitoring and alerting. This helps in maintaining the health and performance of applications and infrastructure.

### Kafka Ecosystem

The Kafka ecosystem consists of various tools and frameworks that extend its capabilities:


Kafka Connect: Kafka Connect is a framework for connecting Kafka with external systems such as databases, key-value stores, search indexes, and file systems. It provides connectors that can move data into and out of Kafka.

Kafka Streams: Kafka Streams is a lightweight stream processing library that allows developers to build real-time applications and microservices. It provides a high-level API for processing data streams and supports stateful computations.

Kafka REST Proxy: The Kafka REST Proxy provides a RESTful interface to interact with Kafka. It allows applications to produce and consume messages using HTTP, which is useful for integrating with systems that cannot use the native Kafka clients.

Schema Registry: The Confluent Schema Registry provides a centralized repository for managing schemas used in Kafka topics. It ensures that data is serialized and deserialized consistently, enabling schema evolution and compatibility.

KSQL: KSQL is a SQL-like stream processing engine for Kafka. It allows users to write SQL queries to process and analyze data streams in real time. KSQL simplifies stream processing by providing an intuitive and familiar query language.

##  Use Cases of Apache Kafka

Real-Time Analytics: Companies use Kafka to analyze data in real time, providing insights and enabling proactive decision-making.

Event-Driven Architectures: Kafka enables event-driven architectures where different services communicate through events, enhancing scalability and decoupling.

Microservices: Kafka facilitates communication between microservices, allowing them to exchange messages asynchronously and reliably.

Log Aggregation and Monitoring: Kafka is widely used for collecting and aggregating logs from various services, enabling centralized monitoring and alerting.

Data Integration: Kafka serves as a backbone for data integration, moving data between different systems and ensuring consistency and reliability.

Why Kafka is Used Over Other Providers

Apache Kafka is favored over other messaging and streaming platforms for several reasons, attributable to its unique architecture, robust feature set, and performance characteristics. Here’s a detailed look at why Kafka stands out:

1. High Throughput and Low Latency
Performance: Kafka is designed to handle high-throughput, real-time data streams with minimal latency. It achieves this through efficient disk storage mechanisms and high-performance networking capabilities. Kafka’s architecture allows it to process millions of messages per second, making it suitable for applications requiring high throughput.

2. Scalability
Horizontal Scalability: Kafka’s distributed nature allows it to scale horizontally by adding more brokers to a cluster. Each topic in Kafka is partitioned, and these partitions can be spread across multiple brokers. This architecture ensures that Kafka can handle increasing loads without degradation in performance.

Elasticity: Kafka’s partition-based architecture allows for dynamic scaling. As the load increases, more partitions and brokers can be added without downtime, providing elastic scalability.

3. Durability and Fault Tolerance
Replication: Kafka replicates data across multiple brokers, ensuring data durability and availability. This replication mechanism guarantees that even if one or more brokers fail, the data remains accessible.

Log-Based Storage: Kafka’s use of log-based storage ensures that data is persisted on disk in an append-only fashion. This approach minimizes data corruption and allows for efficient data recovery.

4. Flexibility and Versatility
Multiple Use Cases: Kafka is versatile and supports various use cases, including real-time analytics, event sourcing, log aggregation, metrics collection, and stream processing. Its ability to handle a wide range of scenarios makes it a preferred choice for many organizations.

Integration with Ecosystem: Kafka integrates seamlessly with a wide array of tools and frameworks, such as Kafka Connect for data integration, Kafka Streams for stream processing, and external processing frameworks like Apache Flink and Apache Spark. This extensibility makes it a central component of many data architectures.

5. Message Ordering and Guarantee
Message Ordering: Kafka ensures strict ordering of messages within a partition, which is crucial for applications where the order of events is important.

Delivery Semantics: Kafka supports various delivery semantics, including at-most-once, at-least-once, and exactly-once delivery. This flexibility allows developers to choose the appropriate level of guarantee based on their application requirements.

6. High Availability
Leader-Follower Architecture: Kafka’s leader-follower model ensures high availability. Each partition has one leader and multiple followers. If the leader fails, one of the followers automatically takes over, ensuring continuous availability without manual intervention.

7. Cost Efficiency
Efficient Resource Utilization: Kafka’s design allows for efficient use of resources, both in terms of storage and compute. Its log-structured storage mechanism minimizes disk I/O, and its distributed nature ensures load balancing across the cluster.

Open Source: As an open-source project, Kafka eliminates licensing costs associated with proprietary messaging systems, making it a cost-effective solution for many organizations.

8. Active Community and Support
Vibrant Community: Kafka has a large and active open-source community. This community continuously contributes to the platform, ensuring it evolves with new features, performance improvements, and bug fixes.

Commercial Support: Organizations like Confluent offer commercial support and additional features, making Kafka a viable choice for enterprises that require professional support and enhanced capabilities.

9. Stream Processing Capabilities
Kafka Streams: Kafka provides a native stream processing library called Kafka Streams, which allows for building real-time processing applications directly within the Kafka ecosystem. This integration simplifies the development and deployment of stream processing applications.

KSQL: Kafka also offers KSQL, a SQL-like language for stream processing. KSQL enables users to perform stream processing tasks using SQL queries, making it accessible to users who are more familiar with SQL than with traditional programming languages.

### Comparison with Other Providers

Kafka vs. RabbitMQ

Throughput: Kafka typically offers higher throughput compared to RabbitMQ, making it more suitable for high-volume data streams.

Scalability: Kafka’s partition-based architecture scales more easily and efficiently than RabbitMQ’s queue-based model.

Durability: Kafka’s log-based storage and replication provide better durability and fault tolerance.

Kafka vs. Apache Pulsar

Architecture: Pulsar uses a layered architecture with separate serving and storage layers, which can offer advantages in some scenarios, but Kafka’s integrated architecture is simpler and has proven performance.

Maturity and Ecosystem: Kafka has a more mature ecosystem with a broader range of integrations and tools. Pulsar is newer and still catching up in terms of ecosystem and community support.

Kafka vs. Amazon Kinesis

Vendor Lock-In: Kafka is open-source and can be run on-premises or in any cloud environment, while Kinesis is a proprietary service offered by AWS, leading to potential vendor lock-in.

Feature Set: Kafka’s feature set, including Kafka Streams and Kafka Connect, offers more flexibility and integration options compared to Kinesis.

Conclusion

Apache Kafka is a powerful distributed event streaming platform that plays a crucial role in modern data architectures. Its ability to handle high throughput, provide fault tolerance, and integrate with various processing frameworks makes it an essential tool for real-time data ingestion, processing, and integration. With its robust ecosystem and wide range of use cases, Kafka continues to be a key component in building scalable and resilient data-driven applications.


### Core Components and Architecture of Kafka

Apache Kafka is a distributed streaming platform that is widely used for building real-time streaming data pipelines and applications. Kafka allows for high-throughput, fault-tolerant, publish-subscribe messaging systems. Understanding the core components and architecture of Kafka is essential for leveraging its full potential. This document will cover the foundational elements of Kafka, including brokers, producers, consumers, topics, partitions, and the architecture that ties them all together, focusing on replication and fault tolerance.

Kafka Brokers

What is a Kafka Broker?
A Kafka broker is a server in a Kafka cluster that stores data and serves clients (producers and consumers). Brokers handle all read and write operations to topics. A Kafka cluster consists of one or more brokers to ensure scalability and fault tolerance.

Role of Brokers in Kafka

Brokers receive messages from producers, assign offsets to them, and commit the messages to storage on disk. They also serve consumers by responding to fetch requests for particular topics and partitions. Brokers are responsible for replicating data to ensure fault tolerance.

# Starting a Kafka broker (simplified example)

kafka-server-start.sh config/server.properties

### Kafka Producers and Consumers

Kafka Producers

Producers are applications that publish (write) messages to Kafka topics. A producer decides which record to assign to which partition within a topic.

Producing Messages

```
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");

Producer<String, String> producer = new KafkaProducer<>(props);
producer.send(new ProducerRecord<String, String>("my-topic", "key", "value"));
producer.close();
```

Kafka Consumers

Consumers are applications that read (subscribe to) messages from Kafka topics. Consumers can read from multiple brokers and consume messages in parallel.

Consuming Messages

```
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("group.id", "test");
props.put("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
props.put("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");

Consumer<String, String> consumer = new KafkaConsumer<>(props);
consumer.subscribe(Arrays.asList("my-topic"));
while (true) {
    ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
    for (ConsumerRecord<String, String> record : records)
        System.out.printf("offset = %d, key = %s, value = %s%n", record.offset(), record.key(), record.value());
}
```

### Kafka Topics and Partitions

Topics

A topic is a category or feed name to which records are published. Topics in Kafka are always multi-subscriber; that is, a topic can have zero, one, or many consumers that subscribe to the data written to it.

Partitions

A partition is a division of a topic. Topics may have many partitions, so they can handle an arbitrary amount of data. Partitions also allow topics to be parallelized by splitting the data across multiple brokers.

# Creating a topic with multiple partitions

```/root/kafka/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 3 --topic my-first-topic```

### Kafka Architecture

Kafka's architecture is designed to be fault-tolerant, scalable, and capable of handling high volumes of data. Let's delve into some key architectural components.

Role of Brokers in Architecture

Brokers form the backbone of the Kafka cluster. Each broker can handle terabytes of messages without impacting performance. Brokers work together to serve and balance client requests and data.

Leader and Follower Replicas

For each partition of a topic, one broker serves as the leader, and the others serve as followers. The leader handles all read and write requests for the partition, while the followers replicate the leader to ensure data redundancy and fault tolerance.

# Describing topic to see leader and replicas

``` /root/kafka/bin/kafka-topics.sh --describe --bootstrap-server localhost:9092 --topic my-topic 
```

Achieving Fault Tolerance through Replication

Kafka replicates the log for each partition across a configurable number of servers. This ensures that, even in the case of server failure, the data can be recovered from another broker that holds a replica of the partition.

By understanding these core components and the architecture of Kafka, users can better design and implement robust, scalable, and fault-tolerant streaming applications.


### Introduction to Kafka Producers and Consumers

Apache Kafka is a distributed streaming platform that allows for the building of real-time streaming data pipelines and applications. At its core, Kafka manages records in a fault-tolerant and scalable way. This guide focuses on two essential components of Kafka: producers and consumers. We will explore their roles, how they interact with Kafka, and provide practical examples using Kafka CLI to produce and consume messages.

## Understanding Kafka Producers

A Kafka producer is responsible for publishing records (messages) to Kafka topics. Think of a Kafka topic as a category or feed name to which records are published. Producers send data to Kafka brokers, which then ensure that the data is stored and replicated for fault tolerance.

## How Producers Work

Producers serialize the data (convert it into bytes) and then send it over the network to the Kafka cluster. The cluster, based on the partition strategy defined (e.g., round-robin, key-based partitioning), stores the data in the appropriate partitions of the topic.

Example: Producing Messages
To produce messages to a Kafka topic, you can use the Kafka CLI command kafka-console-producer. Here's a simple example:

```
/root/kafka/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic exampleTopic
```

This command opens a prompt where you can enter messages. Each line you enter gets published to the exampleTopic topic on the Kafka cluster running on localhost:9092.


## Important Kafka Producer Configurations

linger.ms: This configuration controls how long the producer will wait before sending a batch of messages. Setting this to a higher value can increase throughput by allowing more messages to be sent at once, but may also increase latency.

acks: The acks setting determines how many acknowledgments the producer waits for before considering a message as sent. Setting acks=all ensures the leader waits for acknowledgments from all replicas, providing durability at the cost of potential increased latency.

batch.size: Controls the maximum size (in bytes) of the batch that the producer will attempt to send. A larger batch can improve throughput but requires more memory.

##  Understanding Kafka Consumers

Kafka consumers read records from topics. A consumer subscribes to one or more topics and reads the records in the order in which they were produced.

##  How Consumers Work
Consumers use a pull model to fetch data from brokers. They keep track of the records they have consumed by managing offsets, which are essentially pointers to the last record the consumer has read. Kafka stores these offsets, allowing consumers to resume reading from where they left off, even after restarts or failures.

## Consumer Groups
Kafka consumers can work as part of consumer groups. When multiple consumers are part of the same group, Kafka ensures that each partition is only consumed by one consumer from the group. This mechanism allows for distributing the data processing across many consumers for scalability and fault tolerance.

Example: Consuming Messages

To consume messages from a Kafka topic, you can use the Kafka CLI command kafka-console-consumer. Here's how to consume messages from the beginning of the exampleTopic:

```/root/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic exampleTopic --from-beginning```

This command will display messages from exampleTopic as they are produced, starting from the earliest records.

##  Important Kafka Consumer Configurations

from-beginning: Using this flag with the consumer command allows the client to consume messages from the earliest offset available for the topic. Without this flag, the consumer will only read from the latest offset.

group.id: This defines the consumer group to which a Kafka consumer belongs. Kafka ensures that only one consumer in the group processes a partition at a time, distributing the load across multiple consumers.

isolation.level: This setting controls whether the consumer reads committed or uncommitted messages when working with transactional topics. Setting it to read_committed ensures the consumer only reads fully committed messages.

Practical Considerations

When working with Kafka producers and consumers, it's essential to consider serialization/deserialization, partitioning, and offset management. These aspects significantly impact the efficiency and reliability of your Kafka-based applications.

Serialization/Deserialization

Producers serialize messages into bytes before sending them to Kafka. Consumers must deserialize these bytes back into the original data format. Kafka supports multiple serialization formats, including JSON, Avro, and Protobuf.

Partitioning
Proper partitioning ensures efficient data distribution across the Kafka cluster. Producers can specify a key for each message, which Kafka uses to determine the partition within the topic where the message will be stored.

Offset Management
Consumers track their progress using offsets. It's crucial to manage these offsets carefully to ensure that your application processes all messages exactly once and in order.

Conclusion
Kafka producers and consumers play vital roles in the Kafka ecosystem, enabling the efficient and reliable exchange of data between applications. By understanding how to work with these components, developers can leverage Kafka's power to build scalable and fault-tolerant streaming applications. The examples provided here should help you get started with producing and consuming messages using Kafka's CLI tools, forming the basis for more complex Kafka-based solutions.

### Kafka Topics and Partitions Simplified

In this guide, we'll demystify two core concepts of Apache Kafka: topics and partitions. Kafka, a distributed streaming platform, allows for high-throughput, fault-tolerant handling of
real-time data feeds. Understanding topics and partitions is crucial for effectively using Kafka, whether you're a beginner or looking to deepen your knowledge. Let's dive into 
how topics are used to categorize messages and how partitions enable Kafka's scalability and parallel processing capabilities.

### Understanding Kafka Topics

Imagine a Kafka topic as a category or a folder where messages are stored. Topics in Kafka are the way producers (those who publish messages) and consumers (those who subscribe to messages) communicate. 
Each message published to a Kafka cluster is assigned to a specific topic, making that message available to any consumer group subscribed to the topic.

###Creating a Kafka Topic
To create a topic in Kafka, you use the kafka-topics command-line tool provided with Kafka. Here's a simple example:

```
/root/kafka/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 3 --topic my-first-topic
```
This command creates a topic named my-first-topic with 3 partitions and a replication factor of 1.

###Listing Kafka Topics
To see what topics exist in your Kafka cluster, you can list them using:
```
/root/kafka/bin/kafka-topics.sh --list --bootstrap-server localhost:9092
```

### Understanding Topic Characteristics
Immutability: Once a message is written to a topic, it cannot be changed. This immutability is a key feature of Kafka's design.
Retention Policy: Kafka topics come with a configurable retention policy, determining how long messages are kept before being deleted. This can be based on time or size
.
### Kafka Partitions Explained
Partitions are Kafka's way of scaling and ensuring fault tolerance. Each topic can be divided into multiple partitions, each of which can be hosted on different Kafka brokers in a cluster.
This allows for messages within a topic to be distributed across the cluster, enabling parallel processing and increasing throughput.

Why Partitions?
Parallelism: Partitions allow multiple consumers to read from a topic in parallel, significantly increasing the system's throughput.
Scalability: As the volume of messages grows, more partitions can be added to distribute the load across more brokers.
Creating Partitions
When you create a topic, as shown previously, you specify the number of partitions. However, you can also alter the number of partitions for an existing topic:
```
/root/kafka/bin/kafka-topics.sh --alter --bootstrap-server localhost:9092 --topic my-first-topic --partitions 6
```

This command increases the number of partitions for my-first-topic to 6.

### How Partitions Work

Ordering: Messages within a partition are guaranteed to be in the order they were written. However, across partitions, this order is not guaranteed.
Consumer Groups: Each partition is consumed by only one member of a consumer group at a time, ensuring that messages are processed in order.
Practical Example: Producing and Consuming Messages
Producing Messages to a Topic

```
/root/kafka/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic my-first-topic
```

> Hello, Kafka!
> This is a message.
> 

Consuming Messages from a Topic

```
/root/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic my-first-topic --from-beginning
```

This command will display all messages from my-first-topic, starting from the beginning.

Summary

Kafka topics and partitions are fundamental concepts that enable Kafka's high performance, scalability, and fault tolerance. Topics act as categories for messages, while partitions allow
for distributed storage and parallel processing. Understanding these concepts is crucial for designing effective Kafka-based systems. Through practical examples of creating topics, 
producing, and consuming messages, we've seen how these elements play out in a Kafka environment. Whether you're just starting with Kafka or looking to optimize your use of it, 
mastering topics and partitions is a step toward building robust, scalable streaming applications.



### Kafka Environment Setup for Beginners

Apache Kafka is a powerful distributed streaming platform that enables you to build real-time streaming data pipelines and applications. Setting up a Kafka environment involves 
installing Kafka itself along with ZooKeeper, which Kafka uses for cluster management. This guide will walk you through the process of setting up a Kafka environment from scratch, 
making it as straightforward as possible for beginners.

Prerequisites

Before diving into the Kafka setup, ensure you have the following prerequisites covered:

A Linux-based system (the commands here are tailored for a Linux environment)

Basic command-line knowledge

curl installed on your system to download Kafka
tar for extracting the Kafka archive

Java installed, as Kafka requires it to run
Root or sudo privileges for creating service files

Step 1: Downloading Kafka

Apache Kafka is available for download on its official website. However, for convenience, we'll use curl to download Kafka directly from the command line. The following commands download Kafka version 3.7.1. Make sure to navigate to the Kafka download page to check if a newer version is available.

curl -L https://downloads.apache.org/kafka/3.7.1/kafka_2.13-3.7.1.tgz -o ~/Downloads/kafka.tgz

Step 2: Extracting Kafka

Once the download is complete, you'll need to extract the Kafka archive to a directory of your choice. The following commands create a new directory for Kafka in your home directory and extract the archive there.

mkdir ~/kafka && cd ~/kafka
tar -xvzf ~/Downloads/kafka.tgz --strip 1 -C ~/kafka

Step 3: Setting Up ZooKeeper

Kafka uses ZooKeeper to manage cluster metadata and configurations. Although Kafka comes with a ZooKeeper configuration out of the box, we'll need to create a system service for ZooKeeper to ensure it starts automatically with your system.

Creating a ZooKeeper Systemd Service

Create a systemd service file for ZooKeeper using the following command. This will open a text editor in your terminal where you can paste the service configuration.

sudo nano /etc/systemd/system/zookeeper.service

Paste the following configuration into the editor.

```
[Unit]
Requires=network.target remote-fs.target
After=network.target remote-fs.target

[Service]
Type=simple
User=root
ExecStart=/root/kafka/bin/zookeeper-server-start.sh /root/kafka/config/zookeeper.properties
ExecStop=/root/kafka/bin/zookeeper-server-stop.sh
Restart=on-abnormal

[Install]
WantedBy=multi-user.target
```
Save and close the editor (in nano, press CTRL+X, then Y, and Enter to save changes).


Step 4: Setting Up Kafka Server

Similar to ZooKeeper, Kafka also requires a system service for automatic management. Use the following command to create a Kafka service file.

sudo nano /etc/systemd/system/kafka.service

Paste the following configuration into the editor.

```
[Unit]
Requires=zookeeper.service
After=zookeeper.service

[Service]
Type=simple
User=root
ExecStart=/bin/sh -c '/root/kafka/bin/kafka-server-start.sh /root/kafka/config/server.properties > /root/kafka/kafka.log 2>&1'
ExecStop=/root/kafka/bin/kafka-server-stop.sh
Restart=on-abnormal

[Install]
WantedBy=multi-user.target
```

Again, save and close the editor.



Step 5: Starting the Services

With both service files in place, you can now enable and start ZooKeeper and Kafka.
```
sudo systemctl enable zookeeper
sudo systemctl start zookeeper
sudo systemctl enable kafka
sudo systemctl start kafka
```

Verifying the Installation

To verify that Kafka and ZooKeeper are running correctly, you can use the systemctl status command.
```
sudo systemctl status zookeeper
sudo systemctl status kafka
```

If everything is set up correctly, you should see that both services are active.

Conclusion

Congratulations! You have successfully set up a Kafka environment on your system. This setup provides a solid foundation for developing real-time streaming applications and data pipelines. As you become more familiar with Kafka, you can explore advanced configurations, 
cluster setup, and Kafka's vast ecosystem of tools and extensions.


### Writing Kafka Producers

Apache Kafka is a distributed streaming platform that enables the publication and subscription of streams of records in a fault-tolerant, durable manner. Kafka producers are responsible for sending data to Kafka topics, where it can be processed by consumers. This document provides a detailed explanation of creating Kafka producers in both Java and Python, focusing on establishing connections, sending messages, and handling errors.

Table of Contents

Introduction to Kafka Producers
Creating a Kafka Producer in Java
Setting Up a Gradle Project
Establishing Connection
Sending a Message
Error Handling
Creating a Kafka Producer in Python
Setting Up a Python Project
Establishing Connection
Sending a Message
Error Handling

1. Introduction to Kafka Producers

Kafka producers are applications that send records to Kafka topics. They handle the serialization of data into byte streams and the distribution of records across the various partitions of a topic. Kafka producers are designed to be efficient, scalable, and resilient.

2. Creating a Kafka Producer in Java

Setting Up a Gradle Project

Create a New Directory for the Project:
   mkdir kafka-producer
   cd kafka-producer

Initialize the Gradle Project:
   gradle init --type java-application.
   
Add Kafka Dependencies:
Modify the build.gradle file to include the Kafka dependencies:
   plugins {
       id 'application'
   }

   repositories {
       mavenCentral()
   }

   dependencies {
       implementation 'org.apache.kafka:kafka-clients:3.0.0'
   }

   application {
       mainClassName = 'com.example.SimpleProducer'
   }

Establishing Connection

Create a Java Class for the Producer:

Create src/main/java/com/example/SimpleProducer.java and add the following code:
```
   package com.example;

   import org.apache.kafka.clients.producer.KafkaProducer;
   import org.apache.kafka.clients.producer.Producer;
   import org.apache.kafka.clients.producer.ProducerRecord;
   import java.util.Properties;

   public class SimpleProducer {
       public static void main(String[] args) {
           Properties props = new Properties();
           props.put("bootstrap.servers", "localhost:9092");
           props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
           props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");

           Producer<String, String> producer = new KafkaProducer<>(props);

           String topicName = "example-topic";
           String message = "Hello, Kafka!";

           producer.send(new ProducerRecord<>(topicName, "key1", message));
           producer.close();
       }
   }
```

Explanation:

bootstrap.servers: The address of your Kafka cluster.
key.serializer & value.serializer: How to turn the key and value objects the producer will send into bytes.
Sending a Message
To send a message, create a ProducerRecord with the topic name, key, and value, then call the send method on the producer instance.

Example code for sending a message:
```
String topicName = "example-topic";
String key = "key1";
String value = "Hello, Kafka!";

// Create a ProducerRecord
ProducerRecord<String, String> record = new ProducerRecord<>(topicName, key, value);

// Send the record
producer.send(record);
Explanation:

ProducerRecord<String, String> record = new ProducerRecord<>(topicName, key, value);: Creates a record with the specified topic, key, and value.
producer.send(record);: Sends the record to the Kafka cluster.
Error Handling
To handle errors, you can use callbacks and try-catch blocks. Modify the send method to include a callback:

producer.send(new ProducerRecord<>(topicName, key, value), (metadata, exception) -> {
    if (exception == null) {
        System.out.println("Message sent successfully to topic " + metadata.topic() + " partition " + metadata.partition() + " offset " + metadata.offset());
    } else {
        System.err.println("Error sending message: " + exception.getMessage());
    }
});
Additionally, ensure to close the producer in a finally block to release resources:

try {
    producer.send(new ProducerRecord<>(topicName, key, value), (metadata, exception) -> {
        if (exception == null) {
            System.out.println("Message sent successfully to topic " + metadata.topic() + " partition " + metadata.partition() + " offset " + metadata.offset());
        } else {
            System.err.println("Error sending message: " + exception.getMessage());
        }
    });
} catch (Exception e) {
    System.err.println("Error: " + e.getMessage());
} finally {
    producer.close();
}
```

Explanation:

try-catch-finally: Ensures that the producer is closed properly even if an error occurs.

Callback: Handles the result of the send operation, printing success or error messages.


3. Creating a Kafka Producer in Python

Setting Up a Python Project

Create a New Directory for the Project:
   mkdir kafka-producer
   cd kafka-producer

Create and Activate a Virtual Environment:
   python3 -m venv venv
   source venv/bin/activate

Install Kafka-Python:
   pip install kafka-python

Establishing Connection

Create a file named producer.py and add the following code:

```
from kafka import KafkaProducer

producer = KafkaProducer(bootstrap_servers='localhost:9092',
                         key_serializer=lambda k: k.encode('utf-8'),
                         value_serializer=lambda v: v.encode('utf-8'))

topic_name = 'example-topic'
message = 'Hello, Kafka!'

producer.send(topic_name, key='key1', value=message)
producer.close()
Explanation:

bootstrap.servers: The address of your Kafka cluster.
key_serializer & value_serializer: How to turn the key and value objects the producer will send into bytes.
Sending a Message
To send a message, use the send method with the topic name, key, and value. The serializers ensure the key and value are encoded to bytes.

Example code for sending a message:

topic_name = 'example-topic'
key = 'key1'
value = 'Hello, Kafka!'

# Send the message
producer.send(topic_name, key=key, value=value)
Explanation:

producer.send(topic_name, key=key, value=value): Sends the message to the Kafka cluster with the specified topic, key, and value.
Error Handling
Use the try-except block to handle errors. Modify the send method to include error handling:

from kafka.errors import KafkaError

try:
    future = producer.send(topic_name, key='key1', value=message)
    record_metadata = future.get(timeout=10)
    print(f'Message sent successfully to topic {record_metadata.topic}, partition {record_metadata.partition}, offset {record_metadata.offset}')
except KafkaError as e:
    print(f'Error sending message: {e}')
finally:
    producer.close()
Explanation:

try-except-finally: Ensures that the producer is closed properly even if an error occurs.
KafkaError: Catches exceptions specific to Kafka operations.
future.get(timeout=10): Waits for the send operation to complete and retrieves metadata or raises an error.
```

By following the steps outlined in this document, you will be able to create Kafka producers in both Java and Python, establish connections, send messages, and handle errors efficiently.


Writing Kafka Consumers

In this guide, we'll dive into the world of Kafka consumers, focusing on how to write them using the Java API with Gradle and Python. Kafka, a distributed streaming platform, enables you to process and analyze data in real-time. Consumers play a crucial role in reading data from Kafka topics. We'll explore consumer configurations, reading messages, and managing offsets to give you a comprehensive understanding of Kafka consumers.

Understanding Kafka Consumers

A Kafka consumer reads records from a Kafka cluster. Consumers subscribe to one or more topics and process the stream of records produced to them. In Kafka, the consumer is responsible for keeping track of the records it has processed—this is known as managing offsets.

Why Kafka Consumers?

Scalability: Kafka consumers can be scaled horizontally to read from topics in parallel.
Fault Tolerance: They support automatic offset commit capabilities, ensuring no data loss even in case of consumer failures.
Flexibility: Consumers can start reading from a specific offset, allowing for various processing strategies, such as reprocessing historical data.
Setting Up Your Environment
Before writing Kafka consumers, you need to set up your development environment. This involves installing Kafka and setting up a project using Gradle for Java or a suitable environment for Python.

Installing Kafka

Download and unzip Kafka from the official website. Start the Zookeeper and Kafka server:

# Start Zookeeper

bin/zookeeper-server-start.sh config/zookeeper.properties

# Start Kafka Server

bin/kafka-server-start.sh config/server.properties
Setting Up a Gradle Project for Java
Create a new directory for your project and initialize a Gradle project:

mkdir kafka-consumer-java
cd kafka-consumer-java
gradle init --type java-application
Add the Kafka clients dependency to your build.gradle file:

dependencies {
    implementation 'org.apache.kafka:kafka-clients:2.8.0'
}

Setting Up Python Environment

Ensure you have Python installed and create a new virtual environment:

python3 -m venv kafka-consumer-python
source kafka-consumer-python/bin/activate
Install the Kafka Python package:

pip install kafka-python
Writing a Simple Kafka Consumer in Java
Let's write a simple Kafka consumer that subscribes to a topic and prints the messages to the console.

Basic Consumer Configuration

Create a new Java class SimpleConsumer.java. Initialize the consumer with basic configurations:

```
import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.clients.consumer.KafkaConsumer;
import java.util.Arrays;
import java.util.Properties;

public class SimpleConsumer {
    public static void main(String[] args) {
        Properties props = new Properties();
        props.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");
        props.put(ConsumerConfig.GROUP_ID_CONFIG, "test-group");
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(ConsumerConfig.AUTO_OFFSET_RESET_CONFIG, "earliest");

        try (KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props)) {
            consumer.subscribe(Arrays.asList("test-topic"));
            // Consumer logic goes here
        }
    }
}
Reading Messages
Inside the try block, add logic to poll for new messages and print them:

while (true) {
    ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
    for (ConsumerRecord<String, String> record : records) {
        System.out.printf("offset = %d, key = %s, value = %s%n", record.offset(), record.key(), record.value());
    }
}
Writing a Simple Kafka Consumer in Python
Now, let's implement a similar consumer in Python.

Basic Consumer Configuration
Create a new Python script simple_consumer.py. Initialize the consumer with basic configurations:

from kafka import KafkaConsumer

consumer = KafkaConsumer(
    'test-topic',
    bootstrap_servers=['localhost:9092'],
    auto_offset_reset='earliest',
    group_id='test-group',
    value_deserializer=lambda x: x.decode('utf-8')
)

```
Reading Messages

Add logic to continuously read messages and print them:
```
for message in consumer:
    print(f"offset = {message.offset}, key = {message.key}, value = {message.value}")
```

Managing Offsets

Kafka consumers use offsets to keep track of the messages they have consumed. By default, offsets are committed automatically, but you can also manage them manually for finer control.

Automatic Offset Committing

Both the Java and Python consumers above use automatic offset committing. This behavior is controlled by the enable.auto.commit configuration (set to true by default).

Manual Offset Committing

To manually commit offsets in Java, set enable.auto.commit to false and use the commitSync method:

```
props.put(ConsumerConfig.ENABLE_AUTO_COMMIT_CONFIG, "false");
// Inside the polling loop
consumer.commitSync();
In Python, use the commit method:

consumer = KafkaConsumer(enable_auto_commit=False)
# Inside the message loop
consumer.commit()
```

Conclusion

Writing Kafka consumers is a fundamental skill for working with real-time data streams. By understanding consumer configurations, reading messages, and managing offsets, you can build robust applications that process data efficiently. Whether using Java with Gradle or Python, Kafka provides the flexibility and power to meet your streaming needs.
