# kafka-market-stock

## Introduction
Kafka is crucial in the stock market for its ability to handle real-time data streams, ensuring efficient processing, analysis, and distribution of vast amounts of trading data, which enables faster decision-making and enhances market operations.

After studying the theoretical aspects of Apache Kafka, I embarked on a practical journey to test Kafka's functionality. 
This project demonstrates setting up Kafka, creating a producer and consumer, and integrating Kafka with Python and AWS services such as S3 and Athena.

## 1.Using Terminal to Send, Write, and Read Data in Real Time:

## Kafka Setup and Usage:
### Download and Extract Kafka
```sh
wget https://archive.apache.org/dist/kafka/3.3.1/kafka_2.12-3.3.1.tgz
```
```sh
tar -xzf kafka_2.12-3.3.1.tgz
```
### Install and Verify Java:
```sh
sudo amazon-linux-extras enable corretto8
```
```sh
sudo yum install -y java-1.8.0-amazon-corretto-devel
```
```sh
java -version
```

### Navigate to Kafka Directory:
```sh
cd kafka_2.12-3.3.1
```

### Start ZooKeeper:
```sh
bin/zookeeper-server-start.sh config/zookeeper.properties
```

### Start Kafka Server:
Open a new terminal window and SSH into your EC2 instance.  
Set Kafka heap options and start the Kafka server:
```sh
export KAFKA_HEAP_OPTS="-Xmx256M -Xms128M"
```
```sh
cd kafka_2.12-3.3.1
```
```sh
bin/kafka-server-start.sh config/server.properties
```

### Configure Server Properties for Public IP :
-Edit server.properties to set ADVERTISED_LISTENERS to the public IP of your EC2 instance:
```sh
sudo nano config/server.properties
```

### Create a Kafka Topic :
-Open a new terminal window and SSH into your EC2 instance:
```sh
cd kafka_2.12-3.3.1
```
```sh
bin/kafka-topics.sh --create --topic my_demo --bootstrap-server <public-IP>:9092 --replication-factor 1 --partitions 1
```

### Start Kafka Consumer :

-Open a new terminal window and SSH into your EC2 instance:
```sh
cd kafka_2.12-3.3.1
```
```sh
bin/kafka-console-consumer.sh --topic my_demo --bootstrap-server <public-IP>:9092
```

- At this point, you should be able to send data from the producer and receive it on the consumer side.

![kafka ](https://github.com/user-attachments/assets/41fab83d-ee97-4b16-bb84-52de253646fb)

 
## 2.Using Python to Send, Write, and Read Data in Real Time:

### Data Integration:
Instead of manually sending data, we can automate the process by loading data from an API or a dataset and using a Kafka producer to send this data to a consumer, which then stores it in a target location such as Amazon S3.

### Example:
- Take any data from Kaggle or another dataset.
- Loop through the data, generating and sending it randomly using a Kafka producer.
- Consume the data using a Kafka consumer and store it in Amazon S3.
This example demonstrates Kafka's mechanism using a single broker and partition on a small machine.

## Storing Data in Amazon S3:
### AWS Setup :
- Create a new S3 bucket to store data.
- Configure AWS CLI on your local machine:
  aws configure
AWS Access Key ID [key-id]
AWS Secret Access Key [secret-key-id]
Default region name [region]

### Upload Data to S3 :
After configuring AWS CLI, you can upload data from your local machine to S3.

### Building a Crawler with AWS Glue and Querying with Athena:
- Create an IAM role for Glue with access to read and write data in S3.
- Create a database for the Glue crawler.
- Use Athena to query the data stored in S3.

### Technology Used
 jupyter
 Apache Kafka
 Amazon Web Service (AWS)
- EC2
- S3 (Simple Storage Service)
- Glue Crawler /Catalog
- Athena

## Conclusion:
This project provides a practical example of how to use Apache Kafka to move data from one source to another, integrate it with AWS services, and query the data using AWS Athena.
The goal is to understand the data flow and how Kafka facilitates real-time data processing and storage.


