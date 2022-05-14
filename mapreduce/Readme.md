- Create folder Data on Desktop and copy all given files

- Open file named access_log_short.txt using libreoffice and use separator as “-”
(Uncheck remaining options), save the file as text CSV format

- `su - hduser`

- `sudo mkdir analyzelogs`

- Right click on data folder open properties and copy the path
  
`sudo cp /home/pranaypawar/Desktop/Data/* ~/analyzelogs`

(change the path according to your path)

`sudo chmod -R 777 analyzelogs`

`sudo chown -R hduser analyzelogs`

`cd analyzelogs`

`sudo chmod +r *.*`

- paste the below line in terminal

`export CLASSPATH="$HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-client-core-2.9.0.jar:$HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-client-common-2.9.0.jar:$HADOOP_HOME/share/hadoop/common/hadoop-common-2.9.0.jar:~/analyzelogs/SalesCountry/*:$HADOOP_HOME/lib/*"`

`javac -d . SalesMapper.java SalesCountryReducer.java SalesCountryDriver.java`

`sudo nano Manifest.txt`

- copy paste this line

`Main-Class: SalesCountry.SalesCountryDriver`

- after copy pasting do ctrl + x, Y , Enter

`jar -cfm analyzelogs.jar Manifest.txt SalesCountry/*.class`

`cd`

`start-dfs.sh`

`start-yarn.sh`

`jps`

- check hadoop running properly)

`cd analyzelogs`


`sudo mkdir ~/input`

`sudo cp access_log_short.csv ~/input/`


`$HADOOP_HOME/bin/hdfs dfs -put ~/input /`


`$HADOOP_HOME/bin/hadoop jar analyzelogs.jar /input /output`


`$HADOOP_HOME/bin/hdfs dfs -cat /output/part-00000`


- this gives mapreduce outputjps


`stop-dfs.sh`


`stop-yarn.sh`