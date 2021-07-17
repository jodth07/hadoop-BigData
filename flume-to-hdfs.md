## Part 1 : Getting Data from Twitter with Flume 
1. Create folder `$home/orange_data/` in hdfs <br />
    `hdfs dfs -mkdir -p $home/orange_data/`


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
 - TwitterAgent.sinks.HDFS.hdfs.path = hdfs://`<your hdfs url>:8020>` $home/orange_data/



6. To run flume 
- first : move to the hadoop flume directory<br />
`cd /usr/hdp/current/flume-server/`<br />
- then, run flume<br />
`./bin/flume-ng agent -name TwitterAgent --conf conf --conf-file $HOME/flume/twitter.conf -Dflume.root.logger=INFO,console`

#### Note:
if you run into a Authentication Failure, run this command <br />
`sudo ntpdate ntp.ubuntu.com` <br \>
repeat step above.


7. Check that you have stored the data <br />
`hdfs dfs -ls $home/orange_data/`
there should be some new created files.