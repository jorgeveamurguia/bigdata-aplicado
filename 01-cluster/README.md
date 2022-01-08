# Instalación de un cluster Ambari 

siguiendo al guia de 
https://cwiki.apache.org/confluence/display/AMBARI/Quick+Start+Guide

## instalacion de dependencias

### install maven
apt-get install maven 

## download ambari
wget https://downloads.apache.org/ambari/ambari-2.7.6/apache-ambari-2.7.6-src.tar.gz
tar xfvz apache-ambari-2.7.6-src.tar.gz
cd apache-ambari-2.7.6-src
mvn versions:set -DnewVersion=2.7.6.0.0
 
pushd ambari-metrics
mvn versions:set -DnewVersion=2.7.6.0.0
popd

## Instalacion de java 1.8 deprecate, ya que Build fail: "javax.xml.bind.annotation does not exist"
sudo apt install openjdk-8-jdk
sudo update-alternatives --config java

# instalar dependencias de python
sudo apt-get install python-dev

##  install ambari web 
apt-get install npm
npm install --global yarn

## añadir la limitacion de dependecias   
``` -PallModules -Drat.numUnapprovedLicenses=200  ```

## construir build ambari
mvn -B clean install jdeb:jdeb -PallModules -Drat.numUnapprovedLicenses=200  -DnewVersion=2.7.6.0.0 -DbuildNumber=5895e4ed6b30a2da8a90fee2403b6cab91d19972 -DskipTests -Dpython.ver="python >= 2.6"

## si falla poner mvn -rf <nombre del modulo que dío el fallo>

# Step 3: Install Ambari Server

sudo apt-get install  ./ambari-server/target/ambari-server_2.7.6.0-0-dist.deb

# apt-get install ./ambari-server*.deb

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

# Version Definition File ambari github 

https://gist.githubusercontent.com/ferdinandosimonetti/4ba2e7f512af8d0d8a5d11dc40177c3f/raw/6d45fb0fd523971fd75d8e43db1282f507e67cc2/HDP-2.6.5.0-292.xml