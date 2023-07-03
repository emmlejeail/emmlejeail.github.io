---
layout: post
title:  "How to build a Kafka cluster locally with Docker"
author: emmanuelle
categories: [ kafka, docker, tutorial ]
tags: [red, yellow]
image: assets/images/kafka-logo.png
description: "A short tutorial on how to build a local kafka cluster with docker for testing purpose or just to experiment"
featured: true
hidden: true
rating: 4.5
---

## How to Build a Kafka Cluster Locally with Docker

<img src="{{ baseurl }}/assets/images/kafka_logo.png" alt="kafka logo" style="height: 150px;"/> + <img src="{{ baseurl }}/assets/image/docker-logo.png" alt="docker logo" style="height: 150px;"/>

Apache Kafka is a popular distributed streaming platform that can handle real-time data feeds with ease. It is a reliable and scalable system that can handle millions of messages per second, making it an ideal choice for many use cases. However, setting up a Kafka cluster can be a daunting task. Fortunately, with Docker, you can create a local Kafka cluster quickly and easily.

In this tutorial, we will walk you through the steps required to build a Kafka cluster with Docker.

### Step 1: Install Docker

The first step is to ensure that you have Docker installed on your local machine. You can download Docker from their official website for your specific operating system.

### Step 2: Create a Docker Network

Next, you need to create a Docker network that will allow the containers to communicate with each other. Run the following command to create a new Docker network:

```sh
docker network create kafka-net
```
### Step 3: Create a ZooKeeper Container

Kafka requires a ZooKeeper instance to manage the Kafka brokers. We will start by creating a ZooKeeper container. Run the following command to create a ZooKeeper container:

```sh
docker run --name zookeeper --network kafka-net -d zookeeper
```

### Step 4: Create the Kafka Brokers

Next, we will create the Kafka brokers. Run the following command to create a Kafka broker container:

```sh
docker run --name kafka-broker-1 --network kafka-net -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://kafka-broker-1:9092 -d wurstmeister/kafka
```

You can adjust the number of Kafka brokers that you want to create by changing the container name and port number accordingly.

### Step 5: Test the Kafka Cluster

Once you have created the Kafka brokers, you can test your Kafka cluster by creating a topic and publishing a message to it. Run the following commands to create a topic and publish a message to it:

```sh
docker exec -it kafka-broker-1 bash
kafka-topics.sh --create --topic test --partitions 3 --replication-factor 1 --bootstrap-server kafka-broker-1:9092
kafka-console-producer.sh --topic test --bootstrap-server kafka-broker-1:9092
```

You can now publish a message to the topic by typing it in the console.

### Step 6: Scale the Kafka Cluster

One of the main benefits of using Docker to create a Kafka cluster is the ability to scale it easily. You can add more Kafka brokers to your cluster by running the same command as Step 4 but with a different container name and port number.

```sh
docker run --name kafka-broker-2 --network kafka-net -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://kafka-broker-2:9092 -d wurstmeister/kafka
```

With this, you have successfully created a Kafka cluster locally with Docker. You can now start building and testing your Kafka applications locally before deploying them to a production environment. Happy coding!
