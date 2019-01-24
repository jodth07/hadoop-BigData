# hadoop-BigData
We are creating a project in which we analyze data from twitter API

# Instructions 
1. Create folder `/techfield/orange_data/` in hdfs <br />
    `hdfs dfs -mkdir -p /techfield/orange_data/`

2. Create folder if not exits $HOME/flume/ in local directories (maybe maria_dev) <br />
    `mkdir $HOME/flume`

3. copy `twitter.conf` to $HOME/flume/ <br />
    `cd $HOME/flume/` <br />
    copy contens of twitter.conf to `flume/twitter.conf`

4. update info in `twitter.conf` file
 - TwitterAgent.sources.Twitter.consumerKey = <add your twitter app api key>
 - TwitterAgent.sources.Twitter.consumerSecret = <add your twitter app  api secret key> 
 - TwitterAgent.sources.Twitter.accessToken = <add your twitter app  accessToken> 
 - TwitterAgent.sources.Twitter.accessTokenSecret = <add your twitter app  accessTokenSecret>

### to run flume to get the data 
- as of now, this instruction does not work. Working on fixing it.
`bin/flume-ng agent -name TwitterAgent --conf conf --conf-file $HOME/flume/twitter.conf -Dflume.root.logger=INFO,console`
