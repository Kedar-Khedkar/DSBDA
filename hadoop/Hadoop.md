- `java -version`

- `sudo apt-get install default-jdk`

- `sudo addgroup hadoop`

- `sudo adduser --ingroup hadoop hduser`

- `sudo adduser hduser sudo`

- `which ssh`

- `which sshd`

- `sudo apt-get install openssh-server`

- `su hduser`

- `cd`

- `ssh-keygen -t rsa -P ""`

- press enter

- `cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys`

- `ssh localhost`

- `exit`
---------------------------------------------------------------------------------------------------
- download hadoop 
- https://archive.apache.org/dist/hadoop/common/hadoop-2.9.0/hadoop-2.9.0.tar.gz

- extract the file after it is downloaded

- right click on extracted folder, go to properties and copy the path. open terminal and type
<br>
 `sudo mv /home/pranaypawar/Downloads/hadoop-2.9.0 /usr/local/hadoop`
<br>
- (change your path according to your system)
<br>
`sudo chown -R hduser /usr/local/`
---------------------------------------------------------------------------------------------------
`update-alternatives --config java`
<br>
- (check the java version using this command and make changes in bashrc and hadoopenv.sh)
- <br>
---------------------------------------------------------------------------------------------------
<br>
`sudo nano ~/.bashrc`
<br>
- copy paste the below lines 
<br>

`#HADOOP VARIABLES START`


`export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64` 


`export HADOOP_HOME=/usr/local/hadoop` 


`export PATH=$PATH:$HADOOP_HOME/bin` 


`export PATH=$PATH:$HADOOP_HOME/sbin` 


`export HADOOP_MAPRED_HOME=$HADOOP_HOME` 


`export HADOOP_COMMON_HOME=$HADOOP_HOME` 


`export HADOOP_HDFS_HOME=$HADOOP_HOME` 


`export YARN_HOME=$HADOOP_HOME` 


`export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native` 


`export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib"` 
<br>

`#HADOOP VARIABLES END` 
<br>

- after copy pasting do ctrl + x, Y , Enter
<br>

`source ~/.bashrc`

<br>
---------------------------------------------------------------------------------------------------
<br>

`sudo nano /usr/local/hadoop/etc/hadoop/hadoop-env.sh`
<br>

- add this line in the file **change the java version accordingly**
<br>

`export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64`
<br>
- after copy pasting do ctrl + x, Y , Enter

---------------------------------------------------------------------------------------------------
<br>

`sudo nano /usr/local/hadoop/etc/hadoop/core-site.xml`
- copy paste the below lines 
  
`<property>
<name>fs.default.name</name>
<value>hdfs://localhost:9000</value>
</property>`

- after copy pasting do ctrl + x, Y , Enter
---------------------------------------------------------------------------------------------------
`sudo nano /usr/local/hadoop/etc/hadoop/mapred-site.xml.template`
<br>
- copy paste the below lines 

`<property>
<name>mapreduce.framework.name</name>
<value>yarn</value>
</property>`
<br>
- after copy pasting do ctrl + x, Y , rename the file to mapred-site.xml and hit enter , Y
---------------------------------------------------------------------------------------------------
`sudo nano /usr/local/hadoop/etc/hadoop/hdfs-site.xml`
##copy paste the below lines 

`<property>
<name>dfs.replication</name>
<value>1</value>
</property>
<property>
<name>dfs.namenode.name.dir</name>
<value>file:/usr/local/hadoop_tmp/hdfs/namenode</value>
</property>
<property>
<name>dfs.datanode.data.dir</name>
<value>file:/usr/local/hadoop_tmp/hdfs/datanode</value>
</property>`

- after copy pasting do ctrl + x, Y , Enter
---------------------------------------------------------------------------------------------------
- `sudo mkdir -p /usr/local/hadoop_tmp/hdfs/namenode`

- `sudo mkdir -p /usr/local/hadoop_tmp/hdfs/datanode`

- `sudo chown -R hduser:hadoop /usr/local/hadoop_tmp`
---------------------------------------------------------------------------------------------------
- `sudo nano /usr/local/hadoop/etc/hadoop/yarn-site.xml `
  <br>
- copy paste the below lines 

`<property>
<name>yarn.nodemanager.aux-services</name>
<value>mapreduce_shuffle</value>
</property>
<property>
<name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
<value>org.apache.hadoop.mapred.ShuffleHandler</value>
</property>`

- after copy pasting do ctrl + x, Y , Enter
---------------------------------------------------------------------------------------------------
- `hadoop namenode -format`
---------------------------------------------------------------------------------------------------
- To start hadoop

- cd /usr/local/hadoop/sbin

- start-dfs.sh

- start-yarn.sh

- jps

- **if all 5 are showing its working**