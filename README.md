Deprecation Notice
===

This is used for building images for version 5.3.x or lower, and should not be used for adding new images.

For the 5.4.0 release and greater the images have been migrated to the following repositories:

* [common-docker](https://github.com/confluentinc/common-docker)
* [control-center-images](https://github.com/confluentinc/control-center-images)
* [kafkacat-images](https://github.com/confluentinc/kafkacat-images)
* [kafka-images](https://github.com/confluentinc/kafka-images)
* [kafka-mqtt-images](https://github.com/confluentinc/kafka-mqtt-images)
* [kafka-replicator-images](https://github.com/confluentinc/kafka-replicator-images)
* [kafka-rest-images](https://github.com/confluentinc/kafka-rest-images)
* [kafka-streams-examples](https://github.com/confluentinc/kafka-streams-examples)
* [ksql-images](https://github.com/confluentinc/ksql-images)
* [schema-registry-images](https://github.com/confluentinc/schema-registry-images)

# Docker Images for Confluent Plaform


Docker images for deploying and running the Confluent Platform.  The images are currently available on [DockerHub](https://hub.docker.com/u/confluentinc/).  They are currently only available for Confluent Platform 3.0.1 and after.

Full documentation for using the images can be found [here](https://docs.confluent.io/current/installation/docker/index.html).

# Networking and Kafka on Docker

When running Kafka under Docker, you need to pay careful attention to your configuration of hosts and ports to enable components both internal and external to the docker network to communicate. You can see more details in [this article](https://rmoff.net/2018/08/02/kafka-listeners-explained/).

# Known issues on Mac/Windows
	
For more details on known issues when running these images on Mac/Windows, you can refer to the following links:

* [Hostname Issue](https://forums.docker.com/t/docker-for-mac-does-not-add-docker-hostname-to-etc-hosts/8620/4)
* Host networking on Docker for Mac: [link 1](https://forums.docker.com/t/should-docker-run-net-host-work/14215), [link 2](https://forums.docker.com/t/net-host-does-not-work/17378/7), [link 3](https://forums.docker.com/t/explain-networking-known-limitations-explain-host/15205/4)

# Building

Use `make` to perform various builds and tests


# Docker Utils

See [Docker Utils](DOCKER_UTILS.md)


# Contribute

Start by reading our guidelines on contributing to this project found [here](CONTRIBUTING.md).

- Source Code: https://github.com/confluentinc/cp-docker-images
- Issue Tracker: https://github.com/confluentinc/cp-docker-images/issues


# License

The project is licensed under the Apache 2 license. For more information on the licenses for each of the individual Confluent Platform components packaged in the images, please refer to the respective [Confluent Platform documentation for each component](http://docs.confluent.io/current/platform.html).  

# Comandos

 - Criar topico 

docker-compose exec kafka  kafka-topics --create --topic dev4brothers-topic --partitions 1 --replication-factor 1 --if-not-exists --zookeeper zookeeper:2181

 - Verifica se foi criado 
docker-compose exec kafka  kafka-topics --describe --topic dev4brothers-topic --zookeeper zookeeper:2181

 - Envia 100 mensagens para o Topico

docker-compose exec kafka  \
  bash -c "seq 100 | kafka-console-producer --request-required-acks 1 --broker-list localhost:9092 --topic dev4brothers-topic && echo 'Produced 100 messages.'"


  - consumindo as mensagem 

docker-compose exec kafka  \
  kafka-console-consumer --bootstrap-server localhost:9092 --topic dev4brothers-topic --from-beginning --max-messages 100


# Teste 

    -  Dentro da pasta ./examples/kafka-single-node 
    - subir docker com comando docker-compose up -d
    - feito isso entre na pasta consumer e rode node consumer_avg.js e node consumer_sum.js 
    - feito isso os consumers ja estao olhando o topic dev4brothers-topic ai rode o comando para enviar 100 mensagens 