Kafka in Docker
===

Forked from Spotify's kafka docker on github:
https://github.com/spotify/docker-kafka

This repository provides everything you need to run Kafka in Docker.

For convenience also contains a packaged proxy that can be used to get data from
a legacy Kafka 7 cluster into a dockerized Kafka 8.

Why?
---
The main hurdle of running Kafka in Docker is that it depends on Zookeeper.
Compared to other Kafka docker images, this one runs both Zookeeper and Kafka
in the same container. This means:

* No dependency on an external Zookeeper host, or linking to another container
* Zookeeper and Kafka are configured to work together out of the box

Run
---

```bash
docker run -p 2181:2181 -p 9092:9092 --env ADVERTISED_HOST=`docker-machine ip \`docker-machine active\`` --env ADVERTISED_PORT=9092 pipeti/kafka
```

```bash
export KAFKA=`docker-machine ip \`docker-machine active\``:9092
kafka-console-producer.sh --broker-list $KAFKA --topic test
```

```bash
export ZOOKEEPER=`docker-machine ip \`docker-machine active\``:2181
kafka-console-consumer.sh --zookeeper $ZOOKEEPER --topic test
```


In the box
---
* **pipeti/kafka**

  The docker image with both Kafka and Zookeeper. Built from the `kafka`
  directory.

Public Builds
---

https://registry.hub.docker.com/u/pipeti/kafka/

https://registry.hub.docker.com/u/pipeti/kafkaproxy/

Build from Source
---

    docker build -t pipeti/kafka kafka/

Todo
---

* Not particularily optimzed for startup time.
* Better docs

