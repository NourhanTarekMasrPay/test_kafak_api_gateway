# Kafka Topic Management: Create, Produce, and Consume
This guide outlines the essential steps to interact with a Kafka cluster running in Docker, specifically focusing on creating a topic, sending messages as a producer, and receiving messages as a consumer.

## Prerequisites
A running Docker environment with Kafka and Zookeeper containers (as indicated by your docker ps output).
## 
## Step 1: Access the Kafka Container
  First, you need to get an interactive shell inside your running Kafka Docker container to execute Kafka commands.

  `docker exec -it kafka_container bash`

## step 2: List Existing Kafka Topics (Optional, for verification)
  It's good practice to check if any topics already exist before creating a new one.
  `kafka-topics.sh --bootstrap-server localhost:9092 --`

## Step 3: Create a New Kafka Topic
 Now, create your desired Kafka topic. In this example, we'll create order-created with 1 partition and a replication factor of 1.

`kafka-topics.sh --bootstrap-server localhost:9092 --create --topic order-created --partitions 1 --replication-factor 1`

  Explanation of Options:
  
  --bootstrap-server localhost:9092: Specifies the Kafka broker to connect to.
  
  --create: Indicates that you want to create a new topic.
  
  --topic order-created: Sets the name of the topic.
  
  --partitions 1: Defines the number of partitions for the topic.
  
  --replication-factor 1: Sets how many copies of each partition will be maintained across brokers.

## Step 4: Produce Messages to the Topic
  Once the topic is created, you can start sending messages to it using the console producer.
  
    kafka-console-producer.sh --broker-list localhost:9092 --topic order-created
  
  After running this command, your cursor will move to a new line, indicated by a >. Type your messages and press Enter after each one.
  
    >hi nourhan this is my first working kafka with docker
    >hi nourhan again
    >hi nourhan from kafka
  
  To exit the producer, press Ctrl + C.
  
  ## step 5: Consume Messages from the Topic
  To read messages from the topic, you'll use the console consumer. You can open a new terminal window and access the Kafka container again (Step 1) or run this command in the same shell after exiting the producer.
  
  - Option A: Consume from the beginning of the topic
    This command will read all messages currently in the topic, starting from the very first one.
  
        kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic order-created --from-beginning
  
  - Option B: Consume only new messages
  This command will only show messages that are produced after the consumer starts.
  
        kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic order-created
  
 -   Explanation of Options:
    
      --bootstrap-server localhost:9092: Specifies the Kafka broker.
      
      --topic order-created: The topic you want to consume from.
      
      --from-beginning: (Optional) Tells the consumer to read messages from the earliest offset available in the topic. If omitted, it will only read new messages.
      
      Once the consumer is running, you will see the messages you produced appear in the console. To exit the consumer, press Ctrl + C.
