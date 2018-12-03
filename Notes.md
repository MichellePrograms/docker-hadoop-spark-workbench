### Notes
Used the ReadMe.md for instructions on getting up and running
https://github.com/big-data-europe/docker-hadoop-spark-workbench
1.  docker-compose up -d
    * re-ran this command a few times on my windows10 box before it showed no errors
    * shows starting and creating statuses as done without errors
  
2. docker-compose -f docker-compose-hive.yml up -d namenode hive-metastore-postgresql
    * pulls dbe2020/hive-metastore-postgresql , creates the dokerhadoopsparkworkerbenchmaster_hive-metastore-postgresql
    * recreates namenode
3. docker-compose -f docker-compose-hive.yml up -d datanode hive-metastore
    * pulling dbe2020/hive
    * namenode is up to date, recreating datanode_1
    * creating hive-metastore
4. docker-compose -f docker-compose-hive.yml up -d hive-server
    * namenode up to date, creating hive-server, datnode_1 is up to date
5. docker-compose -f docker-compose-hive.yml up -d spark-master spark-worker spark-notebook hue
    * recreating spark-master, spark-notebook , hue_1 is up to date
    * recreating spark-worker_1 done
6. Now test the interface urls to see if we can hit them

* Namenode: http://localhost:50070
    * http://localhost:5070/dfshealth.html#tab-overview
    
* Datanode: http://localhost:50075
    * http://localhost:50075/datanode.html
    
* Spark-master: http://localhost:8080
    * http://localhost:8080
    
* Spark-notebook: http://localhost:9001
    *  http://localhost:9001
    
* Hue (HDFS Filebrowser): http://localhost:8088/home
    * accounts/login/?next=/home
    * user: user
    * pwd: password
