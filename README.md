**啟動 zookeeper 指令如下：**
```
# /opt/zookeeper-3.4.6/bin/zkServer.sh start 
```

**啟動 Kafka Service 指令如下：**
```
# /opt/confluent-4.0.0/bin/kafka-server-start -daemon /opt/confluent-4.0.0/etc/kafka/server.properties
```

**顯示有哪些的 Topic 指令如下：**
```
# /opt/confluent-4.0.0/bin/kafka-topics --list --zookeeper localhost:2181
```

**建立 Topic 指令如下：**
```
# /opt/confluent-4.0.0/bin/kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic connect-test
```

**顯示 Topic 的資料指令如下：**
```
# /opt/confluent-4.0.0/bin/kafka-console-consumer --zookeeper localhost:2181 --topic=test-connect --from-beginning
```
