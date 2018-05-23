---
layout: post
title: "How to sort a Spark rdd on array element"
date: 2016-04-26 8:47:00
categories: scala, apache-spark, rdd
meta: "Spark rdd manipulation"
---

Spark has multiple ways for doing sorting a dataset, sortBy() and SortByKey(). In this post I'm going to do a short application of both on a single sorting problem.

Given: A Spark resilient distributed dataset (rdd) with 10 columns/variables. 

```
rdd
org.apache.spark.rdd.RDD[Array[String]] = ...
```
Question: Sort the whole rdd on the values of column 7, and save the result.

Solution:
Normally doing a sort would be a single line command using the 'SortBy' method, like this:
```
rdd.sortBy(_._7)
```
or 
```
rdd.sortBy(x => x._7)
```

The main complication here is that the sort needs to be on an element in an array, which requires a slightly different phrasing. Note that we ask for the '6th' element, as the array starts counting at 0 not 1.

```
rdd.sortBy(_(6))
```
or
```
rdd.sortBy(arr => arr(6))
```

Method comparison: sortBy versus sortByKey
If for some reason you cannot use the preferred 'sortBy' method, you could also try 'sortByKey', however this method has the limitation that it only works on pairs. Hence - as a preliminary step - map a new dataset rdd2 that consists of a pair of column7 (string values) and the full original rdd (array of strings)

```
rdd2 = rdd.map(c => (c(7),c))
rdd2: org.apache.spark.rdd.RDD[(String, Array[String])] = ...
```

You can then apply sortByKey to create rdd3.

```
rdd3 = rdd2.sortByKey()
rdd3: org.apache.spark.rdd.RDD[(String, Array[String])] = ...
```

This created a new problem however, as rdd3 was created an unalterable tuple of (String, Array[String]). That means that the 'split' method won't work on it now.
```
val rdd4 = rdd3.map(_.split(',')(2))
<console>:33: error: value split is not a member of (String, Array[String])
```

However you can still 'split off' the result by mapping a new dataset rdd4, taking only the second part of the tuple pair.
```
val rdd4 = rdd3.map(_._2)
```

In this case sortByKey() is a more convulated, indirect way of solving the problem so sortBy() would be preferred.