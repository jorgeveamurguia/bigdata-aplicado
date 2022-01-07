# bigdata-aplicado

https://cwiki.apache.org/confluence/display/AMBARI/Quick+Start+Guide

# install maven
apt-get install maven 

# download ambari
wget https://downloads.apache.org/ambari/ambari-2.7.6/apache-ambari-2.7.6-src.tar.gz
tar xfvz apache-ambari-2.7.6-src.tar.gz
cd apache-ambari-2.7.6-src
mvn versions:set -DnewVersion=2.7.6.0.0
 
pushd ambari-metrics
mvn versions:set -DnewVersion=2.7.6.0.0
popd

# java 1.8 deprecate 
# Build fail: "javax.xml.bind.annotation does not exist"
sudo apt install openjdk-8-jdk
sudo update-alternatives --config java


# install 
apt-get install npm
npm install --global yarn
# yarn install --ignore-engines --pure-lockfile


# build ambari
mvn -B clean install jdeb:jdeb -DnewVersion=2.7.6.0.0 -DbuildNumber=5895e4ed6b30a2da8a90fee2403b6cab91d19972 -DskipTests -Dpython.ver="python >= 2.6"


# Step 3: Install Ambari Server

apt-get install ./ambari-server*.deb

# Step 4: Setup and Start Ambari Server

# setup your server
ambari-server setup

# start your server
ambari-server start

#Step 5: Install and Start Ambari Agent on All Hosts

Note: This step needs to be run on all hosts that will be managed by Ambari.

apt-get install ./ambari-agent*.deb

#Edit /etc/ambari-agent/ambari.ini

...
[server]
hostname=localhost
 
...

Make sure hostname under the [server] section points to the actual Ambari Server host, rather than "localhost".

# start ambari agent
ambari-agent start
