# hadoop-BigData
We are creating a project in which we analyze data from twitter API

# Instructions 
1. Create folder `/techfield/orange_data/` in hdfs <br />
    `hdfs dfs -mkdir -p /techfield/orange_data/`

2. Create folder if not exits $HOME/flume/ in local directories (maybe maria_dev) <br />
    `mkdir $HOME/flume`

3. copy `twitter.conf` to $HOME/flume/ <br />
    `cd $HOME/flume/` <br />
    `wget https://github.com/jodth07/hadoop-BigData/blob/master/twitter.conf`<br />

### to run flume to get the data
`bin/flume-ng agent -name TwitterAgent --conf conf --conf-file $HOME/flume/twitter.conf -Dflume.root.logger=INFO,console`
