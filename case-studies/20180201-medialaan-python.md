---
layout: post
title: "Medialaan: Building with Python"
meta: "Demonstration of Python coding"
permalink: /case-studies/20180201-medialaan-python/
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

My daily work varied a lot according to sprint goals and department demands. This particular case study focuses on the creation of new workflows in Python. I created a [similar case study to illustrate my use of Scala](/case-studies/20180201-medialaan-scala/).

## Screenshots

<figure>
  <img src="/case-studies/20180201-medialaan-python/20180201-000000.png" alt="">
  <figcaption>harvestor.py <a href="/case-studies/20180201-medialaan-python/20180201-000000.png">View full size/quality (76KB).</a></figcaption>
</figure>
A short script I wrote to gather information from an external web API database and build a json dataset out of it. The json file format was specified as a requirement by the data scientist.

<figure>
  <img src="/case-studies/20180201-medialaan-python/20180201-000001.png" alt="">
  <figcaption>hdfs_writer.py <a href="/case-studies/20180201-medialaan-python/20180201-000001.png">View full size/quality (76KB).</a></figcaption>
</figure>
A short script I wrote to gather information from an external web API database and build a json dataset out of it. The json file format was specified as a requirement by the data scientist's ticket.

<figure>
  <img src="/case-studies/20180201-medialaan-python/20180201-000002.png" alt="">
  <figcaption>in_sf.py <a href="/case-studies/20180201-medialaan-python/20180201-000002.png">View full size/quality (76KB).</a></figcaption>
</figure>
A temporary script to interface with Apache Kudu, an hadoop ecosystem service that addresses the gap between hdfs and hbase. It was designed to create the necessary kudu tables, download the required data (thousands of tiny csv's, I think) and insert them into kudu.

<figure>
  <img src="/case-studies/20180201-medialaan-python/20180201-000003.png" alt="">
  <figcaption>cdrsupdate.sh - A crontab script <a href="/case-studies/20180201-medialaan-python/20180201-000003.png">View full size/quality (76KB).</a></figcaption>
</figure>
I added this for completeness sake as I do get questions about this. No, you don't always need to fire up Python or Scala to solve problems. Simple recurring actions are usually phrased as scheduled shell scripts. Python gets involved as soon as the solution requires a minimum level of complexity, involving external libraries or complex functions. The example above is on the edge of that threshold. Its purpose is to check for newly created files in an Amazon S3 bucket, download the new files, put them into hadoop's distributed file system and keep the associated database tables up to date. It provided a quick solution during the transition phase at the client, where some data was posted exclusively to a remote Amazon cloud by one team, but had was needed by other teams that couldn't access this cloud.
It ran for only a little while before the client's engineers and I designed a more permanent solution. This new solution implemented streaming and live updates, while also offering improved security, latency, stability. We used Scala for the implementation.


Note: I'll probably split this point about shell scripting into a separate 'case study' at a later point.


{% include promo-next.html %}
