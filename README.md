# kafka-clusters
Kafka cluster configurations with CMAK manager
Configuración de clústers de Apache Kafka mediante ficheros docker-compose.

He recopilado dos configuraciones de clúster de Kafka para pruebas en local y desarrollos personales sin demasiada carga.
* sngl-zk-kafka-cmak-mngr.yml:
Es una configuración simple con Zookeeper, Kafaka y CMAK para administración de tópicos, etc.
* sngl-zk-kafka-multi-ui-mngr.yml: Configuración de múltiples Kafka, Zoopkeeper y CMAK.

Un especial apartado dentro de los ficheros compose, es *kafka-mktopics* que es una opción para crear tópicos en la inicialización del clúster de Kafka.

La configuración del clúster, permite conectar kafka desde Windows para emplear la integración con los servicios que se desarrollen y necesiten Kafka como Servidor de Streaming.

```
docker-compose -f sngl-zk-kafka-cmak-mngr.yml up
ó
docker-compose -f sngl-zk-kafka-multi-cmak-mngr.yml up
```

Dado que la configuración crea su propia red, que puede ser modificada al igual que lo que sea necesario modificar para mejorar o customizar, al ejecutar el clúster en Docker, se crea la red *argades_kafka_net*.

Al ejecutar un contenedor en Docker de un servicio que emplee el clúster de Kafka, el comando debe incluir la red en la que se encuentra el clúster de Kafka.

Ejemplo, para ejecutar el servidor de configuraciones para mantener las configuraciones de los servicios en la nube, sería el siguiente:

```
docker run --network=argades_kafka_net -p 8888:8888 4c28969b53d0 -it
```

La red debe ir al inicio, la he colocado al final y no la reconoce ya que realicé la comprobación de la red del clúster de Kafka y no aparecía el servicio en la misma red.
