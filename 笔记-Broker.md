
# kafka 0.10.2 broker 学习笔记


## zookeeper目录结构

###/brokers/topics/[topic]

```json
{
  "version": 1,
  "partitions": {"0": [0, 1, 3] }
}
```


###/brokers/topics/[topic]/partitions/[partitionId]/state

```json
{
  "version": 1,
  "isr": [0,1],
  "leader": 0,
  "controller_epoch": 1,
  "leader_epoch": 0
}
```

###/brokers/ids/[brokerId]

```json
{
  "version":3,
  "host":"localhost",
  "port":9092,
  "jmx_port":9999,
  "timestamp":"2233345666",
  "endpoints": ["PLAINTEXT://host1:9092", "SSL://host1:9093"],
  "rack": "us-east-1c"
}
```

###/controller_epoch -> int (epoch)

###/controller -> int (broker id of the controller)

###/consumers/[groupId]/ids/[consumerId]

```json
{
  "version": 1,
  "pattern": "static",
  "subscription": {"topic1": 1, "topic2": 2}
}
```

###/consumers/[groupId]/owners/[topic]/[partitionId] -> string (consumerId)

###/consumers/[groupId]/offsets/[topic]/[partitionId] -> long (offset)

###/admin/reassign_partitions

```json
{
  "version": 1,
  "partitions":
  [
    {
      "topic": "Foo",
      "partition": 1,
      "replicas": [0, 1, 3]
    }
  ]
}
```

###/admin/preferred_replica_election

应该触发首选副本选举的分区

```json
{
  "version": 1,
  "partitions":
  [
    {
      "topic": "Foo",
      "partition": 1
    },
    {
      "topic": "Bar",
      "partition": 0
    }
  ]
}
```

###/admin/delete_topics/[topic_to_be_deleted] (the value of the path in empty)

###/config/topics/[topic_name]

```json
{
  "version": 1,
  "config": {
    "config.a": "x",
    "config.b": "y"
  }
}
```

