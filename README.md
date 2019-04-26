# docker_hdp_services
```
cd docker_hdp_services/
```

# Configure Docker to allow pulling from this insecure registry. 

1. Modify /etc/docker/daemon.json on all nodes in the cluster to include the following configuration options.

```
{
 "live-restore" : true,
 "debug": true,
 "insecure-registries" : ["<docker registry>:5000"],
 "dns": ["<yarn registry dns ip addr>"]
}
```

2. Restart Docker on all nodes.



# HBASE

```
cd hbase/
```
  
 # Build hbase image, tag it and push it to you docker registry
```
docker build -t hbase .

docker tag hbase <docker registry>:5000/hbase
docker push <docker registry>:5000/hbase
```
  
# Copy core-site, hdfs-site.xml to user dir in HDFS

```
hdfs dfs -copyFromLocal /etc/hadoop/conf/core-site.xml .
hdfs dfs -copyFromLocal /etc/hadoop/conf/hdfs-site.xml .
```

# Launch the app using the Yarn Services API
```
yarn app -launch hbase hbase.json
```



# HIVE

```
cd hive/
```

# Build hive image, tag it and push it to you docker registry
```
docker build -t hive .

docker tag hive <docker registry>:5000/hive
docker push <docker registry>:5000/hive
```

# Copy core-site, hdfs-site.xml, yarn-site.xml to user dir in HDFS

```
su - hive
hdfs dfs -copyFromLocal /etc/hadoop/conf/core-site.xml .
hdfs dfs -copyFromLocal /etc/hadoop/conf/hdfs-site.xml .
hdfs dfs -copyFromLocal /etc/hadoop/conf/yarn-site.xml .
```

# Launch the app using the Yarn Services API
```
yarn app -launch hive hive.json
```


