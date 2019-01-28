## Part 2 : Load data into Hive and analyze it
- At this point, you should have some new files, saved in `techfield/orange_data/` 

1. open the data file, and copy the header containing the schema, which should look somethign like file `tweets.avsc`

2. create an `avsc` schema file, and paste the header containt in it. 
`vi $HOME/tweets.avsc` # paste contents in it

3. create two directories, for input and ouput in the techfield directory.<br />
`hdfs dfs -mkdir techfield/input`<br />
`hdfs dfs -mkdir techfield/output` <br />
`hdfs dfs -mkdir techfield/avsc` <br />

- check that directories (folders) have been created <br />
`hdfs dfs -ls techfield/`

4. put schema file in hdfs <br />
`hdfs dfs -put $HOME/tweets.avsc techfield/avsc`

5. copy the file from `orange_data` directory to `input` (for safey)<br />
`hdfs dfs -cp techfield/<nameOfFile> techfield/input/tweets`

6. create Table into `hive`<br />
`CREATE EXTERNAL TABLE tweets ROW FORMAT SERDE "org.apache.hadoop.hive.serde2.avro.AvroSerDe" STORED AS INPUTFORMAT "org.apache.hadoop.hive.ql.io.avro.AvroContainerInputFormat" OUTPUTFORMAT "org.apache.hadoop.hive.ql.io.avro.AvroContainerOutputFormat" LOCATION "hdfs://sandbox.hortonworks.com:8020/user/maria_dev/techfield/output" TBLPROPERTIES ("avro.schema.url"="techfield/avsc/tweets.avsc");`


7. load avro file <br />
`LOAD DATA INPATH "techfield/input/tweets" INTO TABLE tweets`


8. Check that the data is loaded into the table <br />
`SELECT * FROM tweets LIMIT 1`