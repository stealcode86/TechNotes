# TechNotes

1) Start the ZooKeeper service by doing the following:
$bin/zookeeper-server-start.sh config/zookeeper.properties

2) To start the Kafka broker service, open a new terminal and type the following commands:
$ bin/kafka-server-start.sh config/server.properties

3) To increase the number of partitions to five, use the following command:
./bin/kafka-topics.sh --alter --zookeeper localhost:2181 --topic sample-topic --partitions 5

4) Knowing topic config
   Navigate to kafka > windows > bin and enter the below command 
   kafka-topics.bat --describe --zookeeper isvkafkap01:2181,isvkafkap02:2181,isvkafkap03:2181,isvkafkap04:2181,isvkafkap05:2181 --topic prod.Attendance.raw
   
5) Listening to topic
   Navigate to kafka > windows > bin and enter the below command 
   kafka-console-consumer.bat --bootstrap-server isvkafkap01:9092,isvkafkap02:9092,isvkafkap03:9092,isvkafkap04:9092,isvkafkap05:9092 --topic Att.prd.GICS
   
6) Listening to topic from beginning ( Last 7 or 14 days based on config )
   kafka-console-consumer.bat --bootstrap-server isvkafkap01:9092,isvkafkap02:9092,isvkafkap03:9092,isvkafkap04:9092,isvkafkap05:9092 --topic Att.prd.Travel --from-beginning
   
7) Creating topic
   kafka-topics.bat --create --zookeeper 10.68.191.69:2181,10.68.191.36:2181,10.68.191.34:2181 --replication-factor 1 --partitions 1 --topic att.dev.flr
   
8) To list all the topics present in a broker
   kafka-topics.bat --list --zookeeper isvkafkap01:2181,isvkafkap02:2181,isvkafkap03:2181,isvkafkap04:2181,isvkafkap05:2181

9) To create connectors in kafka 

   {
    "name": "Att.test.Travel",
    "config": {
        "connector.class": "io.confluent.connect.jdbc.JdbcSourceConnector",
        "timestamp.column.name": "dtLastModified",
        "connection.password": "${vault1:test1/abckafkaconnect:Password_Keyword}",
        "tasks.max": "3",
        "query": "select EmpNo as txtEmpNo, SourceSystem as txtSource, StartDate as dtAttendance, EmpCompany as txtCompany, UniqueId, txtRequestStatus, Enddate, SapCountryCode as txtSAPCountry, cast(dtLastModified as smalldatetime) as dtLastModified from testowner.viewITMEmpItravelDetails (nolock)",
        "mode": "timestamp",
        "topic.prefix": "Att.test.Travel",
        "connection.user": "${vault1:test1/abckafkaconnect:Username_Keyword}",
        "poll.interval.ms": "12000",
        "value.converter.schemas.enable": "false",
        "name": "Att.test.Travel",
        "connection.url": "jdbc:sqlserver://10.82.6.321\\INST2:7020;databaseName=PADB",
        "value.converter": "org.apache.kafka.connect.json.JsonConverter"
    }
}

10) Checking connector config, getting connector status, restarting connectors and tasks 
   
   GET Method
   http://10.69.132.21:30817/connectors/Att.prd.Travel
   http://10.69.132.21:30817/connectors/Att.prd.Travel/status
   
   POST Method
   http://10.68.169.21:30807/connectors/Att.prd.Travel/restart
   http://10.68.169.21:30807/connectors/Att.prd.Travel/tasks/restart/0
