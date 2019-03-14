# docker_hdp_services
```
cd docker_hdp_services/
```

# Build hbase image, tag it and push it to you docker registry
```
docker build -t hbase .

docker tag hbase <docker registry>:5000/hbase
docker push <docker registry>:5000/hbase
```
  
# Configure Docker to allow pulling from this insecure registry. 

1. Modify /etc/docker/daemon.json on all nodes in the cluster to include the following configuration options.

```
{
 "live-restore" : true,
 "insecure-registries" : ["<docker registry>:5000"]
}
```

2. Restart Docker on all nodes.
  
  
# Copy core-site, hdfs-site.xml to user dir in HDFS

```
hdfs dfs -copyFromLocal /etc/hadoop/conf/core-site.xml .
hdfs dfs -copyFromLocal /etc/hadoop/conf/hdfs-site.xml .
```

# Launch the app using the Yarn Services API
```
yarn app -launch hbase hbase.json
```


