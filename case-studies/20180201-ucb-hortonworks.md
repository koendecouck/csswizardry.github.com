---
layout: post
title: "UCB: Hadoop Hortonworks Ambari setup"
meta: "Setup of an Ambari Hortonworks on premise cluster"
permalink: /case-studies/20180201-ucb-hortonworks/
next-case-study-title: "3D printed MRI data"
next-case-study-url: /case-studies/20140809-3dprintedbrain/
hide-hire-me-link: true
---

[UCB (Union Chimique Belge)](http://www.ucb.com) is a multinational biopharmaceutical company headquartered in Brussels, Belgium. UCB focuses primarily on research and development, specifically involving medications centered on epilepsy, Parkinson's, and Crohn's diseases. Hence they manage large amounts of data on research results, medical data and patient information.

Early 2017 the UCB data architecture team, lead by Didier Chalon, asked for help in setting up 4 Hortonworks Hadoop clusters. The job requirements were to setup a separate cluster for development, acceptance, staging and production. This was a work intensive assignment under a tight deadline, as this work was one part of a much larger project with many other actors involved.
In practise I ended up doing a lot of troubleshooting and tutoring for the data scientists, most of whom were new to the Apache Hadoop ecosystem that Hortonworks provides. 

During this time I mostly worked on site in French speaking Belgium, alternating with other days on site at other clients. The full project lasted about eight months (project time, not development time). The privacy sensitive nature of the data required a lot of added security layers, some of them custom written, which was simultaneously the most challenging and rewarding part of the job.

## Summary

* Deployment and integration of DEV/ACC/DR/PROD clusters (Hortonworks Hadoop), including Kerberos Security, Ranger authorization and auditing, Hive with Oracle database, HBase with custom Java load balancer and reverse proxy, Informatica configuration and integration testing, LDAP Active Directory user management.
* Hortonworks Hadoop HDP 2.5, HDFS, Hive, Oracle, Kerberos/KDC, Apache Ranger, RHEL 7.2, Informatica PowerCenter/Informatica BDM 10.1

## The project

The core of my responsabilities here were setting up Apache Hadoop for Hortonworks. Most of that time went into configuring the added layers of security, which I decided to describe as a separate case study (see [UCB - Use of Kerberos](/case-studies/20180201-ucb-kerberos/)).

## Process

At UCB, the first task was to migrate the development environment (Hortonworks Ambari) from a virtual machine (VM) to a physical server. That configuration had one VM as master and a VM as slave. 

To migrate the setup, I had to:
1. Login to Ambari and provision a new, additional host (the physical server).
2. Add the appropriate roles to this new server (same ones as on the slave VM), but with different drive mountpoints for the HDFS and Yarn disk subsystem (It was important to make sure neither service mounted on the OS volume). I did this by defining a [different “host config group” for the new server] (https://docs.hortonworks.com/HDPDocuments/Ambari-2.1.1.0/bk_Ambari_Users_Guide/content/_using_host_config_groups.html).
3. Set the [HDFS replication factor](http://stackoverflow.com/questions/30558217/to-change-replication-factor-of-a-directory-in-hadoop) to 2 both at the command line and in Ambari. This triggered the copying of all data from the slave VM to the new server. (The status of replication can be seen in the HDFS service status page of Ambari).
5. Once the data was replicated, I decommissioned the VM
6. Set the HDFS replication factor down to 1 again in Ambari and at the command line
7. Communicated with the data scientist team about the install and configuration of an additional software suite on the new server, called Informatica.
8. Reviewed the YARN/Tez configuration of the new, bigger server.
9. Install Ranger
10. Install Kerberos
11. Oversee intergration of Ranger and Kerberos with the client's LDAP active directory.
12. Set up Ambari views
13. Install HBase, and create a custom Java load balancer and reverse proxy.
14. General performance improvement.

## Screenshots

<figure>
  <img src="/case-studies/20180201-ucb-hortonworks/preliminaries.png" alt="">
  <figcaption>Hortonworks itself already suggests certain OS tuning before starting... <a href="/case-studies/20180201-ucb-hortonworks/preliminaries.png">View full size/quality (179KB).</a></figcaption>
</figure>
If you're lucky enough to start from an already existing Ambari build then you don't have to go through all the preliminary steps of finetuning the OS. If however you are starting fresh, then I found the following things do help:

** Disable selinux
** Install and run ntpd on all nodes, make sure all clocks of the cluster's servers are perfectly synchronized.
** Add a line vm.swappinness to the configuration, to set swappiness to something low like 10. This has to do with the server's use of swapping memory. You need to have some to avoid 'out of memory' situations, but the default is set around 60 which is way too high and will result in a lot of server warnings about high swap memory use.
** Disable transparent huge pages, as they seem to interfer with Ambari Views.
** Disable firewalld, which interferes with services like Kerberos.
** Install any client needed to access already existing databases, e.g. sqlplus to access an Oracle database.

<figure>
  <img src="/case-studies/20180201-ucb-hortonworks/ambari.png" alt="">
  <figcaption>Ambari cluster settings, showing something resembling the initial VM configuration with 1 data node <a href="/case-studies/20180201-ucb-hortonworks/ambari.png">View full size/quality (179KB).</a></figcaption>
</figure>

Ambari Hortonworks has a rich online support community, which can make a difference when confronted with unexpected trouble.

<figure>
  <img src="/case-studies/20180201-ucb-hortonworks/ranger.png" alt="">
  <figcaption>Ranger settings <a href="/case-studies/20180201-ucb-hortonworks/ranger.png">View full size/quality (179KB).</a></figcaption>
</figure>

Apache Ranger delivers a comprehensive approach to security for a Hadoop cluster. It provides a centralized platform to define, administer and manage security policies consistently across Hadoop components. Using the Apache Ranger console, security administrators can easily manage policies for access to files, folders, databases, tables, or column. These policies can be set for individual users or groups and then enforced consistently across the stack.
In addition, the Ranger Key Management Service (Ranger KMS) provides a scalable cryptographic key management service for HDFS “data at rest” encryption.

<figure>
  <img src="/case-studies/20180201-ucb-hortonworks/views.png" alt="">
  <figcaption>Ambari Views Settings <a href="/case-studies/20180201-ucb-hortonworks/views.png">View full size/quality (179KB).</a></figcaption>
</figure>

Apache Ambari includes the Ambari Views Framework, which enables developers to create UI components, or Views, that 'plug into' the Ambari Web interface. Ambari automatically creates and presents to users some instances of Views, if the service used by that View is added to the cluster. For example, if Apache YARN service is added to the cluster, the YARN Queue Manager View displays to Ambari web users. In other cases, the Ambari Admin user must manually create a view instance. Developing and using Views enables the client to extend and customize the Ambari web interface to meet specific needs.

<figure>
  <img src="/case-studies/20180201-ucb-hortonworks/hbasecustom.png" alt="">
  <figcaption>HBase with custom Java load balancer and reverse proxy <a href="/case-studies/20180201-ucb-hortonworks/hbasecustom.png">View full size/quality (179KB).</a></figcaption>
</figure>

Aside from numerical data, the client required the secure storage and retrieval of images as well. Hbase is a distributed, non-relational open database and best suited for storing that kind of information. That is to say, we stored the binary data of the image, encrypting it, and returning it on demand via HBase reverse proxy (to handle the added security layer). This did require a custom written, bundled JAR (Java code) for the load balancer and the aforementioned reverse proxy.

{% include promo-next.html %}