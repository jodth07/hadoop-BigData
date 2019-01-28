# Instructions
## Part 1 : Getting Data from Twitter with Flume 
1. Create folder `/techfield/orange_data/` in hdfs <br />
    `hdfs dfs -mkdir -p techfield/orange_data/`

2. Create folder if not exits $HOME/flume/ in local directories (maybe maria_dev) <br />
    `mkdir $HOME/flume`

3. copy `twitter.conf` to $HOME/flume/ <br />
    `cd $HOME/flume/` <br />
    copy contens of twitter.conf to `flume/twitter.conf`

4. find your hdfs link
`cat /etc/hosts`


5. update info in `twitter.conf` file 
 - TwitterAgent.sources.Twitter.consumerKey = `<add your twitter app api key>`
 - TwitterAgent.sources.Twitter.consumerSecret = `<add your twitter app  api secret key>`
 - TwitterAgent.sources.Twitter.accessToken = `<add your twitter app  accessToken>`
 - TwitterAgent.sources.Twitter.accessTokenSecret = `<add your twitter app  accessTokenSecret>`
 - TwitterAgent.sinks.HDFS.hdfs.path = hdfs://`<your hdfs url>:8020>`/techfield/orange_data/


6. To run flume 
- first : move to the hadoop flume directory
`cd /usr/hdp/current/flume-server/`
- then, run flume
`./bin/flume-ng agent -name TwitterAgent --conf conf --conf-file $HOME/flume/twitter.conf -Dflume.root.logger=INFO,console`

#### Note:
if you run into a Authentication Failure, run this command <br />
`sudo ntpdate ntp.ubuntu.com` <br \>
repeat step above.

## Part 2 : Load data into Hive and analyze it
- At this point, you should have some new files, saved in `techfield/orange_data/` 

1. open the data file, and copy the header containing the schema, which should look somethign like file `tweets.avsc`

2. create an `avsc` schema file, and paste the header containt in it.
`vi $HOME/tweets.avsc` # paste contents in it

3. create two directories, for input and ouput in the techfield directory.<br />
`hdfs dfs -mkdir techfield/input`<br />
`hdfs dfs -mkdir techfield/output` <br />
`hdfs dfs -mkdir techfield/avsc` <br />

4. put schema file in hdfs
`hdfs dfs -put $HOME/tweets.avsc techfield/avsc`

5. copy the file from `orange_data` directory to `input` (for safey)<br />
`hdfs dfs -cp techfield/<nameOfFile> techfield/input/tweets`

6. create Table into `hive`
`CREATE EXTERNAL TABLE tweets ROW FORMAT SERDE "org.apache.hadoop.hive.serde2.avro.AvroSerDe" STORED AS INPUTFORMAT "org.apache.hadoop.hive.ql.io.avro.AvroContainerInputFormat" OUTPUTFORMAT "org.apache.hadoop.hive.ql.io.avro.AvroContainerOutputFormat" LOCATION "hdfs://sandbox.hortonworks.com:8020/user/maria_dev/techfield/output" TBLPROPERTIES ("avro.schema.url"="techfield/avsc/tweets.avsc");`

7. load avro file
`LOAD DATA INPATH "techfield/input/tweets" INTO TABLE tweets`