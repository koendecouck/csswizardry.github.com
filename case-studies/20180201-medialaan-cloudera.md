---
layout: post
title: "Medialaan: Hadoop Cloudera setup and administration"
meta: "Maintaining a Hadoop Cloudera on premise cluster"
permalink: /case-studies/20180201-medialaan-cloudera/
next-case-study-title: "3D printed MRI data"
next-case-study-url: /case-studies/20140809-3dprintedbrain/
hide-hire-me-link: true
---

[Medialaan](http://medialaan.be) is Belgium's largest private media company. Based on the outskirts of Brussels, Medialaan owns a wide range of national TV stations, radio stations and mobile operators. That makes them a very data-driven company, processing live video information, ratings, call records etc. 
Mid-2017 I was asked by Jose Rotsaert - Medialaan's IT director - to help them migrate a production grade [Cloudera](http://www.cloudera.com/products/open-source/apache-hadoop.html) cluster from Amazon AWS to an on-premise data centre. This was meant to only be a short-term engagement (setup, migration and basic tutorial to the inhouse IT team), but evolved into a durable longterm relationship of day-to-day administration and support. During this time I worked on site as an external consultant.

## Summary

* Migration of Cloudera Hadoop production deployment from Amazon AWS Cloud to on-premise data centre.
* Setup of Cloudera Hadoop development deployment
* Daily governance of Cloudera Hadoop on-premise clusters: LDAP, data migrations, version upgrades, Pentaho Jobs, complex queries in Hive/Impala/Kudu (incl. as part of commandline jobs)
* SCRUM development: build new data workflows in Python and Scala (sbt), using Kafka Streams and Kafka topics, including unit testing.
* Cloudera Hadoop, HDFS, Spark, Yarn, Zookeeper, Oozie, Flume, Hue, Sentry, Hive, Impala, Kudu, Kafka, Active Directory, SSSD, HA Proxy, MySQL, Pentaho

## The project

My daily work varied a lot according to sprint goals and department demands. This particular case study focuses on aspects of the Apache Hadoop setup and administration.

When I joined, the Medialaan team had already been using an Hadoop build hosted on Amazon EC2. For reasons of control, price and data security Medialaan liked to migrate this build over to their on-premise data centre. The first step in that was making a list of our hardware requirements for the on-premise servers, then installing all the needed OS services, followed by installing Hadoop Cloudera and then migrating over all the settings and data.

<figure>
  <img src="/case-studies/20180201-medialaan-cloudera/project1.png" alt="">
  <figcaption>Hadoop Cloudera manager <a href="/case-studies/20180201-medialaan-cloudera/project1.png">View full size/quality (179KB).</a></figcaption>
</figure>

I've documented the full setup process as part of my responsabilities, being as detailed as possible. The result is a 43page PDF consisting of mostly terminal commands and code snippets. Despite the impressive page count, getting set up with Cloudera is mostly smooth work, with most of the developer's attention focused on avoiding particular pitfalls (or otherwise fixing them).

Once the cluster was up and running, I was retained to troubleshoot any issues that arose as part of daily use. I showed other departments how to access data from the Hive/Impala databases. I made performance tweaks, was responsible for version upgrades, security upgrades etc.

## Screenshots

<figure>
  <img src="/case-studies/20180201-medialaan-cloudera/20161128-112343.png" alt="">
  <figcaption>Linux lsblk disk usage and mountpoints <a href="/case-studies/20180201-medialaan-cloudera/20161128-112343.png">View full size/quality (76KB).</a></figcaption>
</figure>
Linux lsblk disk usage and mountpoints. The early steps in the process are very intensive in Linux commands. The IT services team of the client typically does the initial setup, but once the hand-over occurs the OS settings have to be checked and finetuned.

<figure>
  <img src="/case-studies/20180201-medialaan-cloudera/20161201-114659.png" alt="">
  <figcaption>Parquet file format plugin for use with Pentaho <a href="/case-studies/20180201-medialaan-cloudera/20161201-114659.png">View full size/quality (100KB).</a></figcaption>
</figure>
Parquet file format plugin for use with Pentaho. Apache Parquet files are column-oriented data storage formats of the Apache Hadoop ecosystem. It is compatible with most of the data processing frameworks in the Hadoop environment, but not necessarily with non-hadoop services like Pentaho. This fileformat plugin helped to carry the client over to the new system while Pentaho usage was phazed out.

<figure>
  <img src="/case-studies/20180201-medialaan-cloudera/20161128-155611.png" alt="">
  <figcaption>Hadoop Cloudera manager - All nodes offline in a 6 node cluster <a href="/case-studies/20180201-medialaan-cloudera/20161128-155611.png">View full size/quality (392KB).</a></figcaption>
</figure>
Hadoop Cloudera manager - All nodes offline in a 6 node cluster. While working on the cluster, you may need to take nodes' manager services offline (or at least cut their connection to Cloudera manager) while working on them.

<figure>
  <img src="/case-studies/20180201-medialaan-cloudera/20161128-155632.png" alt="">
  <figcaption>Hadoop Cloudera manager - Services <a href="/case-studies/20180201-medialaan-cloudera/20161128-155632.png">View full size/quality (325KB).</a></figcaption>
</figure>
Hadoop Cloudera Manager - Services. This image shows some of the essential services involved in a Hadoop Cloudera cluster. 
HDFS (Hadoop distributed file system) stores files in a distributed fashion across all nodes. 
Hive and Impala are distributed database services, with an SQL-like query language. Hue is an interface to those database services. 
MapReduce is the innate processing component of Hadoop, and important to the cluster's inner operations. 
Oozie is a workflow scheduler system to manage Apache Hadoop jobs, with a nice visual interface and overview. The jobs can be triggered at certain times or upon data availability. It's scheduler ability is similar to crontab, except it looks cluster wide.
Spark is an open-source framework for data processing, related in task and function to MapReduce but considered faster and more powerful. It works on top of the HDFS service, creating resilient distributed datasets. MR2 refers to MapReduce 2.
Yarn is the resource management center of the cluster, scheduling tasks and allocating system resources.
Zookeeper provides operational services for an Hadoop cluster. Distributed applications use Zookeeper to store and mediate updates to important configuration information.

<figure>
  <img src="/case-studies/20180201-medialaan-cloudera/20161208-162010.png" alt="">
  <figcaption>Detail of the Yarn service <a href="/case-studies/20180201-medialaan-cloudera/20161208-162010.png">View full size/quality (172KB).</a></figcaption>
</figure>
Detail of the Yarn service.

<figure>
  <img src="/case-studies/20180201-medialaan-cloudera/20161130-161334.png" alt="">
  <figcaption>Accessing the Impala shell from terminal <a href="/case-studies/20180201-medialaan-cloudera/20161130-161334.png">View full size/quality (139KB).</a></figcaption>
</figure>
Accessing the Impala shell from terminal. The Hue service provides a visually much nicer and powerful interface to Impala, but it can be accessed directly via the terminal as well. This is important for troubleshooting Hue issues, or when you want to incorporate Impala into job scripts. Communication with Impala was necessary for both the Python and Scala workflows I designed and build.

{% include promo-next.html %}
