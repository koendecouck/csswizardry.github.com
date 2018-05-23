---
layout: post
title: "Renaming Hive Partition Values"
date: 2016-12-13 15:24:00
categories: Cloudera, Hortonworks, Hive
meta: "Problems with Hive Partition Renames"
---

You're running queries on a Hive partitioned table on your Hadoop cluster. For some reason, you need to alter some of the partition values.
Typically you'd do this via an ALTER TABLE PARTITION() statement, like the example below:

```sql
ALTER TABLE examples PARTITION (
createyear='2015'
) RENAME TO PARTITION (
createyear='2016'
);
```

However Hive versions predating v0.14 have a major bug in them that can cause those Hive queries to fail. Instead you'd get a general, non-descriptive error from Hive:
Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask. null

The issue seems to be fixed in v0.14, but in case version updating is not an option for you, disabling the file cache first acts as a simple workaround:

```sql
set fs.hdfs.impl.disable.cache=false; 
set fs.file.impl.disable.cache=false; 
ALTER TABLE examples PARTITION (
createyear='2015'
) RENAME TO PARTITION (
createyear='2016'
);
```

Details about [HIVE-7623](https://issues.apache.org/jira/browse/HIVE-7623)

