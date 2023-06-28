# Elastic Search

- Open source analytics and full text search engine
- built in java
- Easy to use highly scalable
- Used for features like autocompleting, correcting typos and handling synonyms

# Kibana

- Dashboard for analysing and visualization like creating pi chart and statistics.

# Logstash

- Earlier it was used to process logs and send it to elastic search.
- Overtime it has evolved, now it is free and open source server side `data processing pipeline` that ingests data from multitude of sources, transforms it and then sends it to the desired `stash` like elastic-search/kafka

eg: newline log file event -> logstash -> elasticsearch/kafka

# X-Pack

Adds additional feature to elastic stack.

- Security
- Monitoring
- Machine learning
- Graph (analyse relationship/relevance in data useful for recommendation)
- ES SQL (SQL API, Translate API: converts SQL Query to Query DSL)

# Beats

`Collection of data shippers`, these are light weight agents which send data from hundreds or thousands of machines and systems (beats installed in those systems) to `Logstash` or `Elasticsearch`. Different kind of beats do different kind of tasks.

## Types of Beats

- Filebeat
- Metricbeat
- Packetbeat
- Winlogbeat
- Auditbeat
- Heartbeat
- Functionbeat

Center is elasticsearch, where all the data is present. We can put the data into elasticsearch through beats or logstash or even through directly using elasticsearch APIs.

Kibana is UI that seats over elasticsearch and visualize elasticsearch's data.

# ES Architecture and How data is stored

## Node and Cluster

Whenever a node is created it is assigned to a cluster according to configuration provided. If there is no configuration present a node is assigned to default cluster

## ES document format

- json
- json + metadata
- keys: \_index, \_source etc.

Actual data resides in `_source`

### Analogies

document === row in sql

fields === column in sql

index === table in sql

# Rest API from Kibana console

### API format:

<method_name> <api_name>/<command_name>

Get health information of cluster

- `GET _cluster/health`

Get information about nodes

- `GET _cat/nodes?v`

Get information about indices(tables)

- `GET _cat/indices?v`

Get information about hidden indices as well

- `GET _cat/indices?v&expand_wildcards=all`

Get information about shards

- `GET _cat/shards?v`

Create an index

- `PUT /fruits`

Delete an index

- `DELETE /fruits`

# Rest API from command line

Curl to get the health information of the node

- `curl -X GET -k -u elastic:TlQOmfepeYn-XFNqm0UQ https://localhost:9200/_cluster/health`

# Sharding in ES

- Sharding is way to divide indices into smaller pieces.
- Each piece is called Shard.
- Sharding is done at index level.
- Sharding improves performance by parallelization of queries.

Total data size: 900 GB

students (800 GB)

teacher (100 GB)

Resource available: 500 GB + 500 GB

### Solution:

student = 400 + 400

teacher = 50 + 50

450 + 450 on both node

Thats why it is called sharding is done at index level.

## Limitations of Shard

Every index has one default shard and every shard has a limitation of 2B documents. If there is more than that then a new shard is required.

### Split API

API to increase number of shards.

### Shrink API

API to decrease number of shards.

# Replication of ES

Replication: process of copying the shards.

Replication Group: combination of Primary(original) shards + Replica shards

Advantage:

- Fault tolerant
- Parallelization

# ES Node Roles

- Data is stored in shards
- Shards are stored in Nodes

It means Node contains shards and hence data. But this is not true always, it is defined by node roles that which node will play which role.

Types of Nodes:

- Master Node: The master node is responsible for light-weight cluster wide actions such as creating or deleting an index, assigning shards to the nodes, tracking all the nodes in the cluster.

  Master node is created by changing the configuration file and setting the value

  `Node.master : true`

  `Node.data : false`

- Data Node: Data nodes hold the shards that contain the documents indexed.

  `Node.data : true`

  No shards will be saved in case of false, In case of master node we set this flag as false as there are other important task to be done by master node.

- Ingest Node: It is enables to run ingest pipeline, manipulate documents before adding index to them, like removing some useless fields and adding some more information. It is just like simplified version of logstash directly within ES.

  `Node.ingest : true`

  In case of filebeat, it is set to false

- ML Role:

  `Node.ml : true` -> jobs enable disable

  `xpack.ml.enabled : true` -> api enable disable

- Coordination Role: Routes queries to other nodes, load balancer, doesn't do anything itself.

  `Node.master : false`

  `Node.data : false`

  `Node.ingest : false`

  `Node.ml : false`

  `xpack.ml.enabled : false`

- Voting Only: Participate in voting to elect master node. But it won't become master node itself.

  `Node.voting_only : true`

# CRUD Operations in ES

## Create an ES document

```
POST student/_doc
{
  "name": "Rahul",
  "age": 25
}
```

## Create ES document with custom Id

```
POST student/_doc/4204390
{
  "name": "Rahul",
  "age": 35
}
```

## Delete ES document by Id

```
DELETE student/_doc/4204390
```

## Get ES document by Id

```
GET student/_doc/4204390
```

## Get all documents of an index

```
GET student/_search
{
  "query": {
    "match_all": {}
  }
}
```

## Update ES document by Id

```
POST student/_update/Ky1n_ogBuwhWgi6-mLZv
{
  "doc": {
    "age": 15,
    "lastName": "Sharma"
  }
}
```

## Scripted update

```
POST student/_update/Ky1n_ogBuwhWgi6-mLZv
{
  "script": {
    "source": "ctx._source.age=35"
  }
}
```

## Params in script to remove hardcode dependency

```
POST student/_update/Ky1n_ogBuwhWgi6-mLZv
{
  "script": {
    "source": "ctx._source.age=params.new_age",
    "params": {
      "new_age": 5
    }
  }
}
```

## Multiline conditional scripted update

```
POST student/_update/Ky1n_ogBuwhWgi6-mLZv
{
  "script": {
    "source": """
      if(ctx._source.age <= 0) {
        ctx.op = 'noop'
      } else {
        ctx._source.age--;
      }
    """
  }
}
```

## Multiline conditional scripted update

```
POST student/_update/Ky1n_ogBuwhWgi6-mLZv
{
  "script": {
    "source": """
      if(ctx._source.age <= 0) {
        ctx.op = 'delete'
      } else {
        ctx._source.age--;
      }
    """
  }
}
```

## Upsert by Id (If found then update else insert)

```
POST student/_update/Ky1n_ogBuwhWgi6-mLZv
{
  "script": {
    "source": "ctx._source.age++"
  },
  "upsert": {
    "name": "Rahul",
    "age": 25
  }
}
```

## Replace ES document by Id

```
PUT student/_doc/Ky1n_ogBuwhWgi6-mLZv
{
  "doc":{
    "name": "Ram",
    "age": 31
  }
}
```

# Elasticsearch Routing

- On which shard does the ES store the document.
- How does ES search for a document.

Elastic search already know which shards does have the document. As the process of resolving the shard while storing the document is same as while searching for the doc.

```
shard_num = hash(_routing) % num_primary_shards

Here, _routing is _id of ES document in case of default routing. It might change in case of custom routing.
```

Note: Once the document starts to get inserted in shard, the number of shards can be changed or modified. As it will cause error while searching as per above condition.

# How ES Reads Data

```
GET /student/_doc/100 <---> Coordination Node <---> Data Node <--routing--> Replication Group <--ARS(Adaptive replica selection i.e. less busy shard replica)--> Replica
```

# How ES Writes Data

```
PUT /student/_doc/100 <---> Coordination Node <---> Data Node <--routing--> Replication Group

1. Assign to primary shard
2. Validate
3. Primary shard saves to itself
4. Primary shard saves to replica shard
```

### Issues:

Suppose primary shard gets stopped while saving to replica shard, then voting happens and one of replica shard gets selected as Primary shard. But there is incosistency of data as the primary shard doesn't have all the data.

So there comes two terms to resolve this issue:

- Primary term: no of time primary shard has been changed
- Sequence number: counter for each write operation

## Global & Local checkpoint

- Global checkpoint: it is for complete replication group (least sequence number out of all shards in the replication group)
- Local checkpoint: it is for every replica (counter for every write op)

# Optimistic Concurrency Control

Primary term and sequence number can be used to solve the concurrency issue. It updates the doc only when the given primary term and sequence number matches, else it fetches for new primary term and sequence number and then updates it. By following such steps we can solve the concurrency control.
