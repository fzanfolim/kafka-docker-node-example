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