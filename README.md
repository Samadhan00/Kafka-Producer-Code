# Kafka-Producer-Code

from kafka import KafkaProducer
import os
from time import sleep
from json import dumps
producer = KafkaProducer(bootstrap_servers=['localhost:9092'],
                         value_serializer=lambda x:
                         dumps(x).encode('utf-8'))
data="C:\\bigdata\\livedata\\"
filelist = os.listdir(data)
for file in filelist:
    with open(data+str(file),errors="ignore") as f:
        line = f.read()
        print(line)
        producer.send("indaus",line)
        sleep(5)
        
 
 ...............................................................................................................
 
 EXPLAINATION:-
 
 What is kafka?
Kafka is a message broker..



#in terminal if u want to execute anything u must be within this path only.
cd C:\bigdata\kafka_2.12-2.8.1
#Start zookeeper
bin\windows\zookeeper-server-start.bat config\zookeeper.properties
#start kafka server 
bin\windows\kafka-server-start.bat config\server.properties

# Topic creation .. very imp its same like table in sql 

bin\windows\kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic indaus

//aboe 3 steps mandatory in any env ..(learning, development, production env )
#test really topic is created or not!
bin\windows\kafka-topics.bat --list --zookeeper localhost:2181

#below 2 steps only testing purpose in learning env only using 
# as of now there is no live data in ur hand so generate live data using this command    with that topics.
bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic indaus
 
#kafka consumer api read data from kafka brokers test purpose use this . read and print 
bin\windows\kafka-console-consumer.bat  --topic indaus --from-beginning --bootstrap-server localhost:9092


https://kafka.apache.org/quickstart

#if u want to intergrate kafka and spark , a dependency required based on spark and kafka version this dependency recommended.
#download jar and place in spark/jars folder 

https://mvnrepository.com/artifact/org.apache.spark/spark-streaming-kafka-0-10_2.12/3.1.2
https://mvnrepository.com/artifact/org.apache.spark/spark-token-provider-kafka-0-10_2.12/3.1.2

#Similarly in kafka lib folder u have kafka jars u have copy to spark/jars folder at that time kafka and spark communite properly without any problems

#in realtime scenario integrations version very very difficult headache ... thats y used versioning control tools ...


#pls note: kafka producer and consumer u have to write  a code to read data from source and to send data to sink u have to write a code using python , java, scala, languages.

kafka and sqoop:
get data from oracle and store in hdfs ...sqoop ... auto generate code  thats y its data exchange framework 
but 
kafka u have to prepare code thats y its message broker 




https://kafka-python.readthedocs.io/en/master/
