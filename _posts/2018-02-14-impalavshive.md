---
layout: post
title: "Same query, different results (Impala VS Hive)"
date: 2018-02-14 13:13:00
categories: cloudera, hive, impala
meta: "impala hive assumption differences"
---

This post will only apply if your company uses a Cloudera Hadoop cluster with Impala. For whatever reason (compatibility with external software?) your cluster also has the Hive service running. 
Both Impala and Hive are very similar in the problem they try to solve. Both are excellent database warehouse services, with Impala being Cloudera's exclusive performance improver over Hive. Both use SQL-like language and both use the underlying HDFS system for data storage. Hence query structure and the query's result will in most cases be similar, if not identical.

Regardless, here are some important differences I found working on a system that depends on both Impala AND Hive.

## Keeping in sync

Hive will 'see' changes to the data warehouse faster than Impala does. For example, when you create a new Impala table, Hive will near instantly detect the new table and you'll be able to use it, just as if it was created by Hive itself. When you create a new Hive table, Impala will NOT detect the new table until its metadata cache is refreshed.

Impala's metadata seems to get refreshed every so ofte (cfr. your Impala settings in Cloudera Manager), but if you don't want to wait the following command will force a metadata refresh.

```
-- Impala
invalidate metadata; 
```

You can also include this in your scripts (or run it as a cronjob) to make sure Impala's metadata stays current.

## Counting

Hive starts counting at position 0, while impala starts counting at position 1. 
This behavior could throw off your scripts if for example they include string manipulation. The query below is supposed to strip a prefix from an old filename (everything before position 43 is left out) and insert that data as a new filename. The result will differ in Impala vs Hive.

```
INSERT into TABLE database.newtable
SELECT id,
substr(cast(old_filename as string),43,999) AS new_filename
FROM database.oldtable;
```

There is no real way to protect against this, so I always recommend putting a warning as an in-script comment, as a courtesy to future developers.

## Time zones and timestamp data


You may notice strange things happening when querying timestamp information too. In this case the exact same record in Hive and Impala will show a different timestamp, even though the record was only inserted once!

What causes this? 
The reason here lies with how Impala deals with time zones and daylight savings time. Impala implicitly assumes any stored timestamp is UCT time (whether it actually is or not), and when queried will attempt to convert that UCT time to your system time. It does the same convertion when writing timestamps to HDFS, hence its assumption that the HDFS data was originally written/converted by Impala upon registration, and that it is now converting it back. 
If your original data was however written by Hive, then this can really mess you up. Hive doesn't do this 'intelligent' handling and will simply read/write the timestamp as it is.

Best case scenario this behavior threw off some of your SELECT scripts, and your reported time is off by a few hours. Worst case scenario you've been using converted timestamps for your partitioning, only to find out that data isn't necessarily placed where you thought it would be.

**A possible solution

As far as I know there is no way to turn off this behavior in Impala. It seems to be hardcoded on a very deep level. If you're going to be using both Impala and Hive then the solution is to let departments know that all timestamps are UTC time, and to make sure Hive mimicks the same 'intelligent' behavior as Impala does, i.e. by converting timestamps to UTC when you first insert them in a table.

The following example shows how you can pass and convert time zones in Hive:

```
-- Hive:
INSERT into TABLE database.newtable
SELECT id,
  from_utc_timestamp(eventtime, 'CET'),
  CAST(YEAR(from_utc_timestamp(eventtime, 'CET')) AS STRING) AS year,
  LPAD(CAST(MONTH(from_utc_timestamp(eventtime, 'CET')) AS STRING), 2, "0") AS month,
  LPAD(CAST(DAY(from_utc_timestamp(eventtime, 'CET')) AS STRING), 2, "0") AS day
FROM database.oldtable;
```

Note how this example also prefixes a zero to all single digit days and months (although this requires storing the information as strings).
