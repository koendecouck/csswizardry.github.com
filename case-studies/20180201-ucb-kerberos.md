---
layout: post
title: "UCB: Kerberos Security"
meta: "Safeguarding Hadoop access with Kerberos"
permalink: /case-studies/20180201-ucb-kerberos/
next-case-study-title: "3D printed MRI data"
next-case-study-url: /case-studies/20140809-3dprintedbrain/
hide-hire-me-link: true
---

[UCB (Union Chimique Belge)](http://www.ucb.com) is a multinational biopharmaceutical company headquartered in Brussels, Belgium. UCB focuses primarily on research and development, specifically involving medications centered on epilepsy, Parkinson's, and Crohn's diseases. Hence they manage large amounts of data on research results, medical data and patient information.

Early 2017 the UCB data architecture team, lead by Didier Chalon, asked for help in setting up 4 Hortonworks Hadoop clusters. The job requirements were to setup a separate cluster for development, acceptance, staging and production. This was a work intensive assignment under a tight deadline, as this work was one part of a much larger project with many other actors involved.
In practise I ended up doing a lot of troubleshooting and tutoring for the data scientists, most of whom were new to the Apache Hadoop ecosystem that Hortonworks provides. 

During this time I mostly worked on site in French speaking Belgium, alternating with other days on site at other clients. The full project lasted about eight months (project time, not development time). The privacy sensitive nature of the data required a lot of added security layers, some of them custom written, which was simultaneously the hardest and most rewarding part of the job.

## Summary

* Deployment and integration of DEV/ACC/DR/PROD clusters (Hortonworks Hadoop), including Kerberos Security, Ranger authorization and auditing, Hive with Oracle database, HBase with custom Java load balancer and reverse proxy, Informatica configuration and integration testing, LDAP Active Directory user management.
* Hortonworks Hadoop HDP 2.5, HDFS, Hive, Oracle, Kerberos/KDC, Apache Ranger, RHEL 7.2, Informatica PowerCenter/Informatica BDM 10.1

## The project

I describe the setup of an Hadoop Hortonworks cluster in a [separate post](/case-studies/20180201-ucb-hortonworks/). Here, I'd like to go into more specifics regarding security. Most notably, this involved Kerberos. The setup and configuration of Kerberos is actually part of the setup of a Hortonworks cluster, one of the later steps, but deserves special attention since if this is not done exactly right, no one will be able to access any of the data. This is because the Kerberos default setting is to block any access attempt. It also has to play nicely with Ranger authorization, file permissions, LDAP and/or other security features that may be in place.

## Kerberos

The initial setup was based on a local Kerberos key distributing centre (KDC), which involved manually creating principals and distributing keytab files to users of the system.

To access the hadoop components with a specific username on the cluster the username has to get a ticket to authorize from Kerberos.

Here is an example to authenticate the user 'infa' (= the user used for informatica tools)

  #1. The linux user “infa” has to be added to the servers on the cluster : 
    $ sudo adduser  -g hdfs infa

  #2. Create the principal:
    $ Kadmin.local  –q  ‘addprinc -randkey infa@DEV.SERVERNAME.LOCAL’

  #3. Generate the keytab for this principal:
    $ Kadmin.local –q ‘xst -k /etc/security/keytabs/infa.keytab infa@DEV.SERVERNAME.LOCAL’

  #4. Set the proper permissions on the keytab file:
    $ sudo chmod 644 /etc/security/keytabs/infa.keytab

This keytab file has to be located somewhere on the local machine of windows users as well, often in a certain path depending on what program is used to connect with the cluster's service.s

  #5. Get a ticket for the user:
    $ kinit -k -t /etc/security/keytabs/infa.keytab infa@DEV.ONETRUTH.LOCAL 

  #6. Add the proxyuser properties for the corresponding user to 'core-site.xml'

In ambari by navigating  to hdfs -> config -> advanced -> Custom core-site -> add these properties:
          Hadoop.proxyuser.infa.hosts= gdcdrwhap801.dir.ucb-group.com
          Hadoop.proxyuser.infa.groups= *
The infa user is accessing the cluster from the server ‘gdcdrwhap801’ so in  the hosts the FQDN of this server has to be inserted.

  #7. login into one of the servers using “infa” user and create home directory for the user on hdfs 
    $ Hadoop fs  –mkdir /user/infa

and make sure this directory is owned by infa:hdfs    
  #8. Now you can authenticate to hadoop services using “infa” user.

You may have to stop and restart the ambari-server for the change to take effect.

    $ sudo ambari-server stop

This process had to be done four times (once for every environment). Since the environments were independent, with independent hostnames, four sets of local Kerberos keytabs were created.

However since the client already had an Active Directory system in place, we agreed to integrate Kerberos with Active Directory. We provided a document with keytab names and SPNs to the IT system admin team, and worked with the system admin team to implement the changes. We used customized Kerberos principals and keytabs.

Some lessons learned:

** One has to be very careful when adding/removing Kerberos. Ambari has a Kerberos setup wizard, but here it failed repeatedly and with little or no direction as to why. Even worse, after a crash it was prone to be stuck in an inconsistent state. Stay safe, be patient and wait until the wizard is completely finished.
The Ambari logs are of little help in monitoring what is going on with Kerberos, but the Kerberos log itself sometimes points you in the right direction. Access them via the terminal on the KDC machine, as there seems to be no way to go through them via Ambari UI.

** Underscores in Kerberos principal names can mean trouble.

** Kerberos processes write to multiple log files, be sure that you're looking at the correct 'master' log of the KDC machine when troubleshooting.

** System admins are generally unfamiliar with Kerberos and need a lot of guidance in what exactly they need to do, to the point where you'd wish you could walk over to their desks and sit next to them. That wasn't possible in this case, where we had to make do with screen sharing and skype calls.

** As a sanity Check at the end, test the Kerberos configuration by trying command 'hdfs dfs ls /' while logged into an authorized and unauthorized user. Kerberos should intervene for the unauthorized user.

## Ranger

Basically Ranger is to Hortonworks, what Sentry is to Cloudera. Ranger supports HDFS, Hive, HBase, Storm, Knox, Solr, Kafka, and YARN but not Cloudera's Impala whereas Sentry would.

Installing Ranger is fairly easy and can be done entirely from within Ambari. Make sure you have a database hostname, name, user and password on hand. Tricky part is integrating it with Kerberos after you've done that setup.


{% include promo-next.html %}