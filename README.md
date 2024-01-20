# Setting up Apache Kafka with Docker Compose

In this guide, we'll use Docker Compose to run Kafka and ZooKeeper servers instead of installing them locally. Follow the steps below:

### Prerequisites:

- For Mac users: Install Kafka using Homebrew. if not you should install kafka for run 2. step
  ```bash
  brew install kafka
  ```
- Install Docker Desktop for Mac or Windows.
- Install Docker Compose.
- Docker pull kafka image
  ```bash
  docker pull bitnami/kafka
  ```
- Docker pull zookeeper image
  ```bash
  docker pull zookeeper
  ```

### Steps:

#### 1. Check Kafka Installation:

> Make sure Kafka is installed by running the following command. If there's no error, it means Kafka is installed.

```
kafka-topics
```

#### 2. Clean Up Data Directories:

> On the first clone, if there's existing data in the Kafka and ZooKeeper folders, remove it.

```
rm -rf ./kafka/*
rm -rf ./zookeeper/*
```

#### 3. Start Zookeeper & Kafka with Docker Compose:

> Run the following command to start ZooKeeper and Kafka servers using Docker Compose.

```
docker-compose up
```

#### 4. Create 2 Topics:

> Create three topics using the bootstrap server address (localhost:9092).

```
kafka-topics --bootstrap-server=localhost:9092 --topic=hellokafka --create
kafka-topics --bootstrap-server=localhost:9092 --topic=hellokafka2 --create
```

#### 5. Check Created Topics:

> Verify that the topics have been created.

```
kafka-topics --bootstrap-server=localhost:9092 --list
```

#### 6. Create 3 Consumers:

> Create three consumers with three different groups in separate terminal windows.

```
kafka-console-consumer --bootstrap-server=localhost:9092 --topic=hellokafka --group=group1
```

```
kafka-console-consumer --bootstrap-server=localhost:9092 --topic=hellokafka2 --group=group1
```

```
kafka-console-consumer --bootstrap-server=localhost:9092 --topic=hellokafka2 --group=group2
```

7. Create 2 Producers:

```
kafka-console-producer --broker-list=localhost:9092 --topic=hellokafka
```

```
kafka-console-producer --broker-list=localhost:9092 --topic=hellokafka2
```

8. Send Messages:
   > Send messages from the producers and see how the consumers receive them.

### Note:

- "group" is the consumer group name. If the Kafka broker goes down, messages in the group will be sent to consumers once the broker is back up.

- "topic" is the topic name.

- "bootstrap-server" is the Kafka server address.

- "broker-list" is the Kafka server address.

- "create" is used to create a topic.

- "list" is used to list all topics.

- "rm -rf" is used to remove a folder.

- "rm" is used to remove a file.

- "up" is used to start Docker Compose.

- "down" is used to stop Docker Compose.

- "kafka-topics" is a command for creating and listing topics.

- "kafka-console-consumer" is a command for creating consumers.

- "kafka-console-producer" is a command for creating producers.
