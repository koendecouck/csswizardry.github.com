---
layout: post
title: "Medialaan: Building with Scala"
meta: "Demonstration of Scala coding"
permalink: /case-studies/20180201-medialaan-scala/
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

My daily work varied a lot according to sprint goals and department demands. This particular case study focuses on the creation of new workflows in Scala. I created a [similar case study to demonstrate the use of Python](/case-studies/20180201-medialaan-python/).


## Screenshots

<figure>
  <img src="/case-studies/20180201-medialaan-scala/20180201-000000.png" alt="">
  <figcaption>Milestone planning cdrs-flow <a href="/case-studies/20180201-medialaan-scala/20180201-000000.png">View full size/quality (179KB).</a></figcaption>
</figure>
This pictures illustrates our Sprint planning for the project: 47 story points assigned to the CDR'S project, which involved a complete Scala rewrite of existing code. The project is divided into multiple tickets for team members to work on, and different milestones.

<figure>
  <img src="/case-studies/20180201-medialaan-scala/20180201-000001.png" alt="">
  <figcaption>Workflow solution design cdrs-flow <a href="/case-studies/20180201-medialaan-scala/20180201-000001.png">View full size/quality (179KB).</a></figcaption>
</figure>
A paper notepad sketch of a proposed engineering solution (my handwriting). This picture shows the different elements involved in taking event data out of Amazon Kinesis (left side), checking it against an external database (top), and injecting it into the Kudu service of our local cloud. Flume is mentioned as a possible solution for reading from Amazon Kinesis. This workflow required several different interfaces, modules, tables and clients and was a major focus for the entire squad for several weeks. Very complex, but very educational and rewarding to finish.

<figure>
  <img src="/case-studies/20180201-medialaan-scala/20180201-000002.png" alt="">
  <figcaption>Scala project code cdrs-flow <a href="/case-studies/20180201-medialaan-scala/20180201-000002.png">View full size/quality (179KB).</a></figcaption>
</figure>
A sample of the IntelliJ scala project code, showing some of the project's dependencies. The entire workflow was implemented in Scala, with some of the interesting dependencies being shapeless, akkastreams, avro4s. There are also email-related dependencies meant to notify an IT administrator of any potential problems.
Shapeless: type class and dependent type based generic programming library for Scala
Akkastreams: A library to do asynchronous stream processing. We wanted to receive the data as a stream instead of the previous version that only checked for new data at fixed times of the day.
Avro4s: Provides schema/class generation and serializing/deserializing library for Apache Avro (which itself is a data serialization system, encoding data into a fast binary format plus schema, which then needs to be deserialized again).

Note: this project was a wider team effort, I definitely did not do everything myself here. My main collaborator on this project was a Russian former Yandex ('Russian Google') employee, a very fruitful pairing.

{% include promo-next.html %}
