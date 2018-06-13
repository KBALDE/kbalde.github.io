---
published: false
---
## How to configure jdbc connection using beeline through Apache Knox

Let’s say that  you have a cluster where APIs or SQL Query Clients use Apache Knox  secured gateway to have access to their data.

To configure a jdbc client connection , you better try to test it with beeline client.

Beeline is a jdbc Hive Client that help to interact with Hive Data Bases. either remotely or not.

Untar hadoop  and Hive tarballs from Apache archive site

```
# untar them on slash opt
tar xzvf   apache-hive-1.2.2bin.tar.gz    
tar xzvf   hadoop-2.7.6.tar.gz           
```
Think of exporting Hadoop Home like this: export HADOOP_HOME='/opt/hadoop-2.7.6 

Now you can launch beeline client and the  configure the connection  as follow

/opt/apache-hive-1.2.2-bin/bin/beeline

>!connect "jdbc:hive2://<KNOX FQDN>:8443/;ssl=true;twoWay=true;\
sslTrustStore=/etc/pki/java/cacerts;trustStorePassword=changeit;sslKeyStore=clients.keystore.jks;\
keyStorePassword=changeit;transportMode=http;httpPath=gateway/default/hive"


This example of connection is made in  2 Way SSL Configured connection. Therefore we have an SSL TrustStore played by the cacerts and an SSL KeyStore, a custom one containing client private and public key.