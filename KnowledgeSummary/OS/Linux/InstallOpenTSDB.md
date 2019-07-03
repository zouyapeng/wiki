# Ubuntu 16.04

## upgrade it
```bash
sudo apt-get update && sudo apt-get upgrade -y && sudo reboot now
```

## install HBase([installation doc](http://opentsdb.net/docs/build/html/installation.html))
### install JDK 8
```bash
sudo apt-get install -y default-jdk
```
### Fetch and install [the newest stable HBase binary](http://apache.claz.org/hbase/stable/)
```bash
wget http://apache.claz.org/hbase/stable/hbase-1.4.10-bin.tar.gz
tar xzvf hbase-1.4.10.tar.gz
cd hbase-1.4.10

# JAVA_HOME has to be set in the HBase env config
echo 'export JAVA_HOME=/usr' >> conf/hbase-env.sh

# edit conf/hbase-site.xml with a minimal config
# other important configurations in https://hbase.apache.org/book.html#important_configurations
<configuration>
  <property>
    <name>hbase.rootdir</name>
    <value>file:///home/ubuntu/hbase</value>
  </property>
  <property>
    <name>hbase.zookeeper.property.dataDir</name>
    <value>/home/ubuntu/zookeeper</value>
  </property>
</configuration>

# start it
bin/start-hbase.sh

# Verify it 
./bin/hbase shell
hbase(main):001:0> status
1 active master, 0 backup masters, 1 servers, 0 dead, 2.0000 average load
```

## install OpenTSDB([official docs](http://opentsdb.net/docs/build/html/installation.html))
## fetch some dependencies
```bash
sudo apt-get install -y gnuplot build-essential python autoconf
```

## download and install pkg
```bash
# https://github.com/OpenTSDB/opentsdb/releases
wget https://github.com/OpenTSDB/opentsdb/releases/download/v2.4.0/opentsdb-2.4.0_all.deb
dpkg -i opentsdb-2.4.0_all.deb
```

## create the tables
```bash
vim /usr/share/opentsdb/tools/create_table.sh
create '$TSDB_TABLE',
  {NAME => 't', VERSIONS => 1, COMPRESSION => '$COMPRESSION', BLOOMFILTER => '$BLOOMFILTER', DATA_BLOCK_ENCODING => '$DATA_BLOCK_ENCODING', TTL => '$TSDB_TTL'}
  
==>>

create '$TSDB_TABLE',
  {NAME => 't', VERSIONS => 1, COMPRESSION => '$COMPRESSION', BLOOMFILTER => '$BLOOMFILTER', DATA_BLOCK_ENCODING => '$DATA_BLOCK_ENCODING'}

# run script to create tables
env COMPRESSION=NONE HBASE_HOME=path/to/hbase /usr/share/opentsdb/tools/create_table.sh
```

## start OpenTSDB
```bash
/etc/init.d/opentsdb start
```

## Tips
```bash
# enable auto_create_metrics by your request
tsd.core.auto_create_metrics = true
```


