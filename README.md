[![Gitter chat](https://badges.gitter.im/gitterHQ/gitter.png)](https://gitter.im/big-data-europe/docker-hadoop-spark-workbench)

# How to use HDFS/Spark Workbench

To start an HDFS/Spark Workbench:
```
    docker-compose up -d
```

docker-compose does not work to scale up spark-workers, for distributed setup see [swarm folder](./swarm) 

## Starting workbench with Hive support

Before starting the next command, check that the previous service is running correctly (with docker logs servicename).
```
docker-compose -f docker-compose-hive.yml up -d namenode hive-metastore-postgresql
docker-compose -f docker-compose-hive.yml up -d datanode hive-metastore
docker-compose -f docker-compose-hive.yml up -d hive-server
docker-compose -f docker-compose-hive.yml up -d spark-master spark-worker spark-notebook hue
```

## Interfaces

* Namenode: http://localhost:50070
* Datanode: http://localhost:50075
* Spark-master: http://localhost:8080
* Spark-notebook: http://localhost:9001
* Hue (HDFS Filebrowser): http://localhost:8088/home

## Important

When opening Hue, you might encounter ```NoReverseMatch: u'about' is not a registered namespace``` error after login. I disabled 'about' page (which is default one), because it caused docker container to hang. To access Hue when you have such an error, you need to append /home to your URI: ```http://docker-host-ip:8088/home```

## Docs
* [Motivation behind the repo and an example usage @BDE2020 Blog](http://www.big-data-europe.eu/scalable-sparkhdfs-workbench-using-docker/)

## Count Example for Spark Notebooks
```
val spark = SparkSession
  .builder()
  .appName("Simple Count Example")
  .getOrCreate()

val tf = spark.read.textFile("/data.csv")
tf.count()
```

## Maintainer
* Ivan Ermilov @earthquakesan

Note: this repository was a part of BDE H2020 EU project and no longer actively maintained by the project participants. 


### Notes
Used the ReadMe.md for instructions on getting up and running
https://github.com/big-data-europe/docker-hadoop-spark-workbench
1.  docker-compose up -d

  a. --re-ran this command a few times on my windows10 box before it showed no errors
  
  b. shows starting and creating statuses as done without errors
  
2. docker-compose -f docker-compose-hive.yml up -d namenode hive-metastore-postgresql
a. pulls dbe2020/hive-metastore-postgresql , creates the dokerhadoopsparkworkerbenchmaster_hive-metastore-postgresql
b. recreates namenode
3. docker-compose -f docker-compose-hive.yml up -d datanode hive-metastore
a. pulling dbe2020/hive
b. namenode is up to date, recreating datanode_1
c. creating hive-metastore
4. docker-compose -f docker-compose-hive.yml up -d hive-server
a. namenode up to date, creating hive-server, datnode_1 is up to date
5. docker-compose -f docker-compose-hive.yml up -d spark-master spark-worker spark-notebook hue
a. recreating spark-master, spark-notebook , hue_1 is up to date
b. recreating spark-worker_1 done
6. Now test the interface urls to see if we can hit them

* Namenode: http://localhost:50070
* Datanode: http://localhost:50075
* Spark-master: http://localhost:8080
* Spark-notebook: http://localhost:9001
* Hue (HDFS Filebrowser): http://localhost:8088/home
