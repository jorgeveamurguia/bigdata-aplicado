# bigdata-aplicado

https://cwiki.apache.org/confluence/display/AMBARI/Quick+Start+Guide


# download ambari
wget https://downloads.apache.org/ambari/ambari-2.7.6/apache-ambari-2.7.6-src.tar.gz
tar xfvz apache-ambari-2.7.6-src.tar.gz
cd apache-ambari-2.7.6-src
mvn versions:set -DnewVersion=2.7.6.0.0
 
pushd ambari-metrics
mvn versions:set -DnewVersion=2.7.6.0.0
popd

# build ambari
mvn -B clean install jdeb:jdeb -DnewVersion=2.7.6.0.0 -DbuildNumber=5895e4ed6b30a2da8a90fee2403b6cab91d19972 -DskipTests -Dpython.ver="python >= 2.6"
