# Learn Hadoop Using Docker
This is just for learning intention, not recomended for production. Use Hortonworks or Cloudera for production instead or you can just setup using cloud service. In GCP there is Dataproc or in AWS there is EMR (Elastic Map Reduce).

#### Have fun !

# Download hadoop binary
This Dockerfile build from existing hadoop image but, if you want to download the binary first instead build your own Dockerfile image :
https://archive.apache.org/dist/hadoop/common/hadoop-3.3.1/hadoop-3.3.1.tar.gz

# Kick-off Cluster
1. Clone this repos to your project directory, and `cd hadoop-in-docker`
2. If you are in Linux/MAC Just simply run `./run_cluster.sh`
3. If you are in Windows try run this command `docker build -t hadoop-base:3.2.1 . && docker-compose up`

# How to run MapReduce Job
1. There is `ratings_breakdown.py` python file in `map_reduce` directory, we can run this file on a local python mode or in Hadoop world
2. For python mode local run command `python3 map_reduce/ratings_breakdown.py input/u.data`
3. To run this file in Hadoop run this command `python3 map_reduce/ratings_breakdown.py -r hadoop --hadoop-streaming-jar /opt/hadoop-3.3.1/share/hadoop/tools/lib/hadoop-streaming-3.3.1.jar input/u.data`
4. Path `/opt/hadoop-3.3.1/share/hadoop/tools/lib/hadoop-streaming-3.3.1.jar` might be different for users or if you are using different version of Hadoop, run command `find / hadoop-streaming-$(HADOOP_VERSION).jar` to find it

# Running with hadoop command
1. Make sure you have `input` directory in HDFS, if it's not exist just run this command `hadoop fs -mkdir -p input`
2. Put your data in `input` directory in your local project `hdfs dfs -put ./input/* input`
3. And ready to run
```
hadoop jar /opt/hadoop-3.3.1/share/hadoop/tools/lib/hadoop-streaming-3.3.1.jar \
-file /path/to/mapper.py    -mapper /path/to/mapper.py \
-file /path/to/reducer.py   -reducer /path/to/reducer.py \
-input input -output output
```

credit to : https://github.com/wxw-matt/docker-hadoop
That inspired me, and i make it less complicated to make it simple to learn
