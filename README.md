# hadoop-BigData
We are creating a project in which we analyze data from twitter API

# commands
### Create hdfs folder
`hdfs dfs -mkdir -p /techfield/orange_data/`

### to run flume to get the data
`bin/flume-ng agent -name TwitterAgent --conf conf --conf-file /root/flume/orange.conf -Dflume.root.logger=INFO,console`