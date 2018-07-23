---
title: "Kafka Useful Cmds"
date: 2018-07-23T15:30:19+03:00
draft: false
rtl: false
---

## Start Kafka 

    confluent start

OR

    zookeeper-server-start ~/Downloads/confluent-4.0.0/etc/kafka/zookeeper.properties&
    kafka-server-start ~/Downloads/confluent-4.0.0/etc/kafka/server.properties&

If using Avro:
    
    schema-registry-start ~/Downloads/confluent-4.0.0/etc/schema-registry/schema-registry.properties&

## Topics 

    kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
    kafka-topics --delete --zookeeper localhost:2181 --topic test
    kafka-topics --list --zookeeper localhost:2181
to describe info of a topic (leader, #partitions, #replications etc)

    kafka-topics --describe --zookeeper localhost:2181 --topic test

## Console

    kafka-console-producer --broker-list localhost:9092 --topic test
    kafka-console-consumer --bootstrap-server localhost:9092 --topic test
If serialization needed for consumer use:

    kafka-console-consumer --bootstrap-server localhost:9092 \
    --topic benchmark-test-out \
    --from-beginning \
    --formatter kafka.tools.DefaultMessageFormatter \
    --property print.key=true \
    --property print.value=true \
    --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
    --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer

    kafka-avro-console-producer \
            --broker-list localhost:9092 --topic avro-test \
            --property value.schema='{"namespace": "com.WireFilter.avro",
    "type": "record",
    "name": "LogRecord",
    "fields": [
        {"name": "timestamp", "type": "double"},
        {"name": "ipSource", "type": "string"},
        {"name": "tcpStatus", "type": "string"},
        {"name": "requestType", "type": "string"},
        {"name": "destinationUrl", "type": "string"},
        {"name": "destinationIp", "type": "string"}
    ]
    }'   < /Users/malsayed/workspace/access-log-reporter/access-log.avro



## Important settings

Change log retention time, to remove files in the server 

    vi ~/Downloads/confluent-4.0.0/etc/kafka/server.properties

add:

    log.retention.ms = 1000
then:

    kafka-server-stop
    kafka-server-start ~/Downloads/confluent-4.0.0/etc/kafka/server.properties&

OR clean kafka log dir (specified by the log.dir attribute in kafka config file ) as well the zookeeper data.

## Monitoring Kafka with JMX
https://www.robustperception.io/monitoring-kafka-with-prometheus/

## Running application

    java -cp target/access-log-reporter-1.0-SNAPSHOT.jar com.WireFilter.app.App
OR

    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 

## Running jmx with java.
    KAFKA_OPTS="$KAFKA_OPTS -javaagent:$PWD/Downloads/prometheus_kafka/jmx_prometheus_javaagent-0.6.jar=7071:$PWD/Downloads/prometheus_kafka/kafka-0-8-2.yml" \
    
    kafka-server-start ~/Downloads/confluent-4.0.0/etc/kafka/server.properties&

    java -jar /Users/malsayed/workspace/access-log-reporter/target/access-log-reporter-1.0-SNAPSHOT.jar

    java -javaagent:/Users/malsayed/Downloads/prometheus_kafka/jmx_prometheus_javaagent-0.6.jar=8080:/Users/malsayed/Downloads/prometheus_kafka/my-application.yml -jar /Users/malsayed/workspace/access-log-reporter/target/access-log-reporter-1.0-SNAPSHOT.jar  com.WireFilter.app.StreamAnalyzer



          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.25</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-simple</artifactId>
            <version>1.7.25</version>
        </dependency>
