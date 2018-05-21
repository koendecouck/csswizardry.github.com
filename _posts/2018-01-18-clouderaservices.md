---
layout: post
title: "Hadoop Cloudera Services"
date: 2018-01-18 12:19:58
categories: Cloudera
meta: "Reference for cluster administrators"
---

The following is a cheatlist of the most popular services on Hadoop Cloudera cluster. It is not meant to be a complete overview. You may refer to this overview from time to time, while getting to know each service.
The italic text is the 'official' definition. Default font denotes either my own definition or any expansion or clarification I make to the offical definition.

## Alphabetical list

<figure>
  <img src="/posts/20180118-clouderaservices/accumulo.png" alt="">
</figure>
**Accumulo**
_The Apache Accumulo sorted, distributed key/value store is a robust, scalable, high performance data storage and retrieval system. This service only works with releases based on Apache Accumulo 1.6 or later_

<figure>
  <img src="/posts/20180118-clouderaservices/flume.png" alt="">
</figure>
**Flume**
_Flume collects and aggregates data from almost any source into a persistent store such as HDFS_

<figure>
  <img src="/posts/20180118-clouderaservices/hbase.png" alt="">
</figure>
**HBase**
_Apache HBase provides random, real-time, read/write access to large data sets (requires HDFS and ZooKeeper)._

<figure>
  <img src="/posts/20180118-clouderaservices/hdfs.png" alt="">
</figure>
**HDFS**
_Apache Hadoop Distributed File System (HDFS) is the primary storage system used by Hadoop application. HDFS creates multiple replicas of data blocks and distributes them on compute hosts throughout a clouster to enable reliable, extremely rapid computations._

<figure>
  <img src="/posts/20180118-clouderaservices/hive.png" alt="">
</figure>
**Hive**
_Hive is a data warehouse system that offers a SQL-like language called HiveQL._

<figure>
  <img src="/posts/20180118-clouderaservices/hue.png" alt="">
</figure>
**Hue**
_Hue is a graphical user interface to work with the Cloudera Distribution including Apache Hadoop (requires HDFS, MapReduce, and Hive)_

<figure>
  <img src="/posts/20180118-clouderaservices/impala.png" alt="">
</figure>
**Impala**
_Impala provides a real-time SQL query interface for data stored in HDFS and HBase. Impala requires Hive service and shares Hive Metastore with Hue._

<figure>
  <img src="/posts/20180118-clouderaservices/isilon.png" alt="">
</figure>
**Isilon**
_EMC Isilon is a distributed filesystem._

<figure>
  <img src="/posts/20180118-clouderaservices/javakeystorekms.png" alt="">
</figure>
**Java Keystore KMS**
_The Hadoop Key Management Service with file-based Java KeyStore. Maintains a single copy of keys, using simple password-based protection. Requires CDH 5.3+. Not recommended for production use._

<figure>
  <img src="/posts/20180118-clouderaservices/kafka.png" alt="">
</figure>
**Kafka**
_Apache Kafka is publish-subscribe messaging rethought as a distributed commit log._

<figure>
  <img src="/posts/20180118-clouderaservices/keyvaluestoreindexer.png" alt="">
</figure>
**Key-Value Store Indexer**
_Key-Value Store Indexer listens for changes in data inside tables contained in HBase and indexes them using Solr._

<figure>
  <img src="/posts/20180118-clouderaservices/kudu.png" alt="">
</figure>
**Kudu**
_Kudu is a true column store for the hadoop ecosystem._

<figure>
  <img src="/posts/20180118-clouderaservices/oozie.png" alt="">
</figure>
**Oozie**
_Oozie is a workflow coordination service to manage data processing jobs on your cluster._

<figure>
  <img src="/posts/20180118-clouderaservices/s3connector.png" alt="">
</figure>
**S3 Connector**
_The S3 Connector Service securely provides a single set of AWS credentials to Impala and Hue. This enables Hue administrators to browse the S3 filesystem and define Impala tables backed by S3 data authorized to that AWS identity, and also enables Impala users to query S3-backed tables without directly providing AWS credentials, subject to having the proper permissions defined via Sentry. The S3 Connector only supports the S3A protocol._

<figure>
  <img src="/posts/20180118-clouderaservices/sentry.png" alt="">
</figure>
**Sentry**
_Sentry service stores authorization policy metadata and provides clients concurrent and secure access to this metadata._

<figure>
  <img src="/posts/20180118-clouderaservices/solr.png" alt="">
</figure>
**Solr**
_Solr is a distributed service for indexing and searching data stored in HDFS._

<figure>
  <img src="/posts/20180118-clouderaservices/spark.png" alt="">
</figure>
**Spark**
_Apache Spark is an open source cluster computing system. This service runs Spark as an application on YARN._

<figure>
  <img src="/posts/20180118-clouderaservices/spark.png" alt="">
</figure>
**Spark (Standalone)**
_Apache Spark is an open source cluster computing system. This is the standalone version of the service which does not use YARN for resource management. Cloudera recommends using Spark on YARN instead of this standalone version._

<figure>
  <img src="/posts/20180118-clouderaservices/sqoop.png" alt="">
</figure>
**Sqoop 1 Client**
_Configuration and connector management for Sqoop 1_

<figure>
  <img src="/posts/20180118-clouderaservices/sqoop.png" alt="">
</figure>
**Sqoop 2**
_Sqoop is a tool designed for efficiently transferring bulk data between Apache Hadoop and structured datastores such as relational databases. The version supported by Cloudera Manager is Sqoop 2._

<figure>
  <img src="/posts/20180118-clouderaservices/yarn.png" alt="">
</figure>
**Yarn (MR2 Included)**
_Apache Hadoop Mapreduce 2.0 (MRv2), or YARN, is a data computation framework that supports MapReduce applications (requires HDFS)._

<figure>
  <img src="/posts/20180118-clouderaservices/zookeeper.png" alt="">
</figure>
**Zookeeper**
_Apache Zookeeper is a centralized service for maintaining and synchronizing configuration data._


## Critical services

These services are mandatory to any Hadoop Cloudera cluster. The cluster will not work without them.

<figure>
  <img src="/posts/20180118-clouderaservices/hdfs.png" alt="">
</figure>
**HDFS**
_Apache Hadoop Distributed File System (HDFS) is the primary storage system used by Hadoop application. HDFS creates multiple replicas of data blocks and distributes them on compute hosts throughout a clouster to enable reliable, extremely rapid computations._

<figure>
  <img src="/posts/20180118-clouderaservices/yarn.png" alt="">
</figure>
**Yarn (MR2 Included)**
_Apache Hadoop Mapreduce 2.0 (MRv2), or YARN, is a data computation framework that supports MapReduce applications (requires HDFS)._

<figure>
  <img src="/posts/20180118-clouderaservices/zookeeper.png" alt="">
</figure>
**Zookeeper**
_Apache Zookeeper is a centralized service for maintaining and synchronizing configuration data._


## Highly recommended services

These services are not strictly necessary to the cluster, but severe restraints will be in place if they are not.

<figure>
  <img src="/posts/20180118-clouderaservices/hive.png" alt="">
</figure>
**Hive**
_Hive is a data warehouse system that offers a SQL-like language called HiveQL._

<figure>
  <img src="/posts/20180118-clouderaservices/impala.png" alt="">
</figure>
**Impala**
_Impala provides a real-time SQL query interface for data stored in HDFS and HBase. Impala requires Hive service and shares Hive Metastore with Hue._

<figure>
  <img src="/posts/20180118-clouderaservices/spark.png" alt="">
</figure>
**Spark**
_Apache Spark is an open source cluster computing system. This service runs Spark as an application on YARN._


## Optional services

These services have certain specialized use cases, which may or may not be relevant to your situation.

<figure>
  <img src="/posts/20180118-clouderaservices/accumulo.png" alt="">
</figure>
**Accumulo**
_The Apache Accumulo sorted, distributed key/value store is a robust, scalable, high performance data storage and retrieval system. This service only works with releases based on Apache Accumulo 1.6 or later_

<figure>
  <img src="/posts/20180118-clouderaservices/flume.png" alt="">
</figure>
**Flume**
_Flume collects and aggregates data from almost any source into a persistent store such as HDFS_

<figure>
  <img src="/posts/20180118-clouderaservices/hbase.png" alt="">
</figure>
**HBase**
_Apache HBase provides random, real-time, read/write access to large data sets (requires HDFS and ZooKeeper)._

<figure>
  <img src="/posts/20180118-clouderaservices/hue.png" alt="">
</figure>
**Hue**
_Hue is a graphical user interface to work with the Cloudera Distribution including Apache Hadoop (requires HDFS, MapReduce, and Hive)_

<figure>
  <img src="/posts/20180118-clouderaservices/isilon.png" alt="">
</figure>
**Isilon**
_EMC Isilon is a distributed filesystem._

<figure>
  <img src="/posts/20180118-clouderaservices/javakeystorekms.png" alt="">
</figure>
**Java Keystore KMS**
_The Hadoop Key Management Service with file-based Java KeyStore. Maintains a single copy of keys, using simple password-based protection. Requires CDH 5.3+. Not recommended for production use._

<figure>
  <img src="/posts/20180118-clouderaservices/kafka.png" alt="">
</figure>
**Kafka**
_Apache Kafka is publish-subscribe messaging rethought as a distributed commit log._

<figure>
  <img src="/posts/20180118-clouderaservices/keyvaluestoreindexer.png" alt="">
</figure>
**Key-Value Store Indexer**
_Key-Value Store Indexer listens for changes in data inside tables contained in HBase and indexes them using Solr._

<figure>
  <img src="/posts/20180118-clouderaservices/kudu.png" alt="">
</figure>
**Kudu**
_Kudu is a true column store for the hadoop ecosystem._

<figure>
  <img src="/posts/20180118-clouderaservices/oozie.png" alt="">
</figure>
**Oozie**
_Oozie is a workflow coordination service to manage data processing jobs on your cluster._

<figure>
  <img src="/posts/20180118-clouderaservices/s3connector.png" alt="">
</figure>
**S3 Connector**
_The S3 Connector Service securely provides a single set of AWS credentials to Impala and Hue. This enables Hue administrators to browse the S3 filesystem and define Impala tables backed by S3 data authorized to that AWS identity, and also enables Impala users to query S3-backed tables without directly providing AWS credentials, subject to having the proper permissions defined via Sentry. The S3 Connector only supports the S3A protocol._

<figure>
  <img src="/posts/20180118-clouderaservices/sentry.png" alt="">
</figure>
**Sentry**
_Sentry service stores authorization policy metadata and provides clients concurrent and secure access to this metadata._

<figure>
  <img src="/posts/20180118-clouderaservices/solr.png" alt="">
</figure>
**Solr**
_Solr is a distributed service for indexing and searching data stored in HDFS._

<figure>
  <img src="/posts/20180118-clouderaservices/spark.png" alt="">
</figure>
**Spark (Standalone)**
_Apache Spark is an open source cluster computing system. This is the standalone version of the service which does not use YARN for resource management. Cloudera recommends using Spark on YARN instead of this standalone version._

<figure>
  <img src="/posts/20180118-clouderaservices/sqoop.png" alt="">
</figure>
**Sqoop 1 Client**
_Configuration and connector management for Sqoop 1_

<figure>
  <img src="/posts/20180118-clouderaservices/sqoop.png" alt="">
</figure>
**Sqoop 2**
_Sqoop is a tool designed for efficiently transferring bulk data between Apache Hadoop and structured datastores such as relational databases. The version supported by Cloudera Manager is Sqoop 2._


