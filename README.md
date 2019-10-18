# HDFS
Installation and Setting up the Environment

1) Download hadoop 2.7.7.tar.gz package
     Unzip it using below command
     [root@localhost~] tar -xvf hadoop-2.7.7.tar.gz 

2) After installing hadoop, configure following files
    set Java path in hadoop-env.sh as export JAVA_HOME=/usr/lib/jvm/jdk1.7.0_67

3) Configure below files accordingly,
Firstly, configure .bashrc file to set environment variables of Hadoop, Sqoop, Pig, Hive, HBase when they are downloaded.

.bashrc file
# set hadoop related environment variables
export HADOOP_HOME=/root/hadoop-2.7.7
export HADOOP_CONF_DIR=/root/hadoop-2.7.7/etc/hadoop
export HADOOP_MAPRED_HOME=/root/hadoop-2.7.7
export HADOOP_COMMON_HOME=/root/hadoop-2.7.7
export HADOOP_HDFS_HOME=/root/hadoop-2.7.7
export YARN_HOME=/root/hadoop-2.7.7
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib"

#set Java Home
export JAVA_HOME=/usr/lib/jvm/jdk1.7.0_67
export PATH=$PATH:/usr/lib/jvm/jdk1.7.0_67/bin

#Add hadoop bin directory to path
export PATH=$PATH:/root/hadoop-2.7.7/bin
export HADOOP_PID_DIR=/root/hadoop-2.7.7/hadoop2_data/hdfs/pid

#set sqoop path
export SQOOP_HOME=/root/sqoop-1.4.6.bin__hadoop-2.0.4-alpha
export PATH=$PATH:/root/sqoop-1.4.6.bin__hadoop-2.0.4-alpha/bin

#set Hive path
export HIVE_HOME=/root/apache-hive-1.2.2-bin
export PATH=$PATH:/root/apache-hive-1.2.2-bin/bin






                                                                      


#set pig path
export PIG_HOME=/root/pig-0.15.0
export PATH=$PATH:/root/pig-0.15.0/bin

#set hbase path
export HBASE_HOME=/root/hbase-0.98.12-hadoop2
export PATH=$PATH:/root/hbase-0.98.12-hadoop2/bin

Also configure below files,

core-site.xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
<property>
<name>fs.default.name</name>
<value>hdfs://localhost:9000</value>
</property>
</configuration>


hdfs-site.xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
<property>
<name>dfs.replication</name>
<value>1</value>
</property>
<property>
<name>dfs.permission</name><value>false</value>
</property>
<property>
<name>dfs.namenode.name.dir</name>
<value>/root/hadoop-2.7.7/hadoop2_data/hdfs/namenode</value>
</property>
<property>
<name>dfs.datanode.data.dir</name>
<value>/root/hadoop-2.7.7/hadoop2_data/hdfs/datanode</value>
</property>
</configuration>


                                                                    




mapred-site.xml
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
<property>
<name>mapreduce.framework.name</name>
<value>yarn</value>
</property>
</configuration>





yarn-site.xml
 <configuration>
<property>
<name>yarn.nodemanager.aux-services</name>
<value>mapreduce_shuffle</value>
</property>
<!--<property>
<name>yarn.nodemanager.auxservices.mapreduce.shuffle.class</name>
<value>org.apache.hadoop.mapred.ShuffleHandler</value>
</property-->
</configuration>

Using Apache Hive with RDBMS
hive> create table dataset(k string, i int, j string) row format delimited fields   
	            terminated by ',' stored as textfile;

hive>load data local in path '/home/dataset.txt into table dataset;

                          

Using Apache Sqoop to import Data from Relational Databases:

Once Sqoop is configured for hadoop run below command to import MySql Database.

[root@localhost~]# sqoop import --connect jdbc:mysql://localhost/project --username root --password root --table class


Using Apache Sqoop To export Data From HDFS To MySql:

[root@localhost~]# sqoop export --connect jdbc:mysql://localhost/project --username root --password root --table exportedclass --export-dir /user/root/class



