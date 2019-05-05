# Einstein
![Einstein](https://github.com/mostafa-asg/einstein/blob/master/images/einstein.jpg)  
This repo contains commands with various tools that I 've been working with them. I want to work faster so 
I do not want to type each command, and above all, to memorize them so I created this repo to easily 
copy and paste commands that I need.

## Kafka
###### create a topic
```
./kafka-topics.sh --zookeeper localhost --create --topic YOUR_TOPIC --partitions 1 --replication-factor 1
```

###### delete a topic
```
./kafka-topics.sh --zookeeper localhost --delete --topic YOUR_TOPIC
```

###### consuming from a topic
```
./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic YOUR_TOPIC --from-beginning
```

###### send records to a topic
```
./kafka-console-producer.sh --broker-list localhost:9092 --topic YOUR_TOPIC
```

###### see information about consumer groups including lag
```
./kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group YOUR_GROUP_ID --describe
```

###### start kafka as a docker container
```
version: '3.7'
services:
  zookeeper:
    image: wurstmeister/zookeeper
    ports:
      - "2181:2181"

  kafka:
    image: wurstmeister/kafka:2.12-2.0.1
    ports:
      - "9092:9092"
    depends_on:
      - zookeeper
    environment:
      KAFKA_ADVERTISED_HOST_NAME: 127.0.0.1
      KAFKA_CREATE_TOPICS: "test:1:1"
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```

## Elasticsearch
###### list all indices
```
http GET localhost:9200/_cat/indices?v
```

###### get information about some indices, for example all start with 'twi'
```
http GET localhost:9200/_cat/indices/twi*?v
```

###### Which index has the largest number of documents?
```
http GET localhost:9200/_cat/indices?v&s=docs.count:desc
```

## Maven
###### create a fat jar
```
 <build>
        <plugins>
            <plugin>
                <artifactId>maven-assembly-plugin</artifactId>
                <version>2.5.3</version>
                <configuration>
                    <!-- get all project dependencies -->
                    <descriptorRefs>
                        <descriptorRef>jar-with-dependencies</descriptorRef>
                    </descriptorRefs>
                    <!-- MainClass in manifest make a executable jar -->
                    <archive>
                        <manifest>
                            <mainClass>YOUR_MAIN_CLASS</mainClass>
                        </manifest>
                    </archive>

                </configuration>
                <executions>
                    <execution>
                        <id>create-archive</id>
                        <phase>package</phase>
                        <goals>
                            <goal>single</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
```
###### create a fat jar with custom name
Add these to `maven-assembly-plugin`'s configuration
```
 <finalName>callbacker.jar</finalName>
 <appendAssemblyId>false</appendAssemblyId>
```

## Typesafe (Lightbend) config
###### Which file should be loaded from resources?
```
java -jar -Dconfig.resource=production.conf YOUR_JAR
```

## curl
###### set http body from file
```
curl -X POST -H "Content-Type: application/json" --data-binary "@{FILE_PATH}" http://httpbin.org
```
