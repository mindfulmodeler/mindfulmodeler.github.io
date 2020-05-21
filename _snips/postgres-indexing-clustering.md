---
layout: page
sidebar: left
subheadline: 
title: "Database Indexing and Clustering"
teaser: "Introduction to SQL indexing and clustering"
breadcrumb: true
tags:
    - postgres
    - database
    - optimization
    - SQL
categories:
    - tutorial
header:
    image_fullwidth: "/unsplash-db.jpg" #"/db-unsplash.jpg"
show_meta: true
comments: true
---

# Indexing
When talking about databases, an **index** is essentially a shortcut that allows direct access to data using an index term or a keyword. It is similar to the index at the end of this book, except that instead of just being organized alphabetically, it could be organized in a linear, hierarchical (tree-structured), or some other fashion.

As you build up your database, you will naturally start to look for ways to increase its performance. Once your data tables grow beyond a few thousand rows, you may want to build an index to speed up searches of the data (unless all your searches are based on attributes, in which case you’ll want to build a normal index on the attribute fields). SQL naturally creates indexes on primary keys, which helps for sorting. If a certain column is not sorted however, you have to search through entire column. Unless you create an index. So a secondary index helps if you wish to search for something else (besides the primary key)

For really large datasets, indexes are what makes databases possible. Without indexing, any search for a feature would require a "sequential scan" of every record in the database. Indexing speeds up searching by organizing the data into a search tree which can be quickly traversed to find a particular record.

PostgreSQL allows the use of multiple indexes in a single query. Of course, this makes sense if many columns are queried at the same time. However, that's not always the case. It can also happen that a single index is used multiple times to process the very same column. Abusing indexes, however, can do more harm than good performance-wise, so it's important to think carefully about when you need to create one. The syntax for creating a new index on a field is trivial:

{% highlight ruby %}
create index students_name
{% endhighlight %}
<!-- On students*name); -->

# Clustering
Clustering allows the re-ordering of a table on the physical disk based on some index. The table is essentially completely rewritten from an initial unordered state into an ordered state. This ensures that records with similar attributes have a high likelihood of being found in the same page, reducing the number of pages that must be read into memory for some types of queries. 

For spatial data, clustering is harder to perform. That's because it's harder to cluser spatial data, since they don't have a simple linear order. However, spatial clusering is still possible - and the goal is the same. Geometries that are near each other in space are near each other on disk. 

In PostgreSQL, there is a command called CLUSTER that allows us to rewrite a table in the desired order. It is possible to point to an index and store data in the same order as the index.

{% highlight ruby %}
CLUSTER denver_streets USING denver_streets_gix;
ANALYZE denver_streets;
{% endhighlight %}

While it is possible to create multiple indexes on a set of data, data can only be clustered according to a single index. You cannot order a table by postal code, name, ID, birthday, and so on, *at the same time*. It means that using CLUSTER will make the most sense if the data have a single obvious search criteria.

## What is the advantage of clustered tables?
Consider you want to read a whole area of data. This might be a certain time range, some physical block, group of IDs, or something similar. The runtime of such queries will vary depending on the amount of data and the physical arrangement of data on the disk. So, even if you are running queries that return the same number of rows, two systems might not provide the answer within the same time span, as the physical disk layout might make a difference. 


# Spatial Indexing
There are two componetns of Spatial Access Methods:
    -	Indexing: knowing the storage location fast (computer/disk/memory) when searching for certain objects. An index is an additional structure to help point in the right direction.
    -	Clustering: physically storing objects close together, which are also often selected together (e.g. because they are nearby in space)


## What do we mean by Spatial Indexing?
Spatial Indexing is a special case of regular database indexing. If you had a set of administrative data (for instance, a long list of postal codes or building names) you could organize them numerically or alphabetically and then create an index on them so that reading them from memory is faster. However, multidimensional data cannot be sorted in this way. 

For example, if you sort on longitude, the latitudes may still be very far away so it is not very efficient. We can speed up determining the relationship between two geometries by first determining the relationship between the bounding boxes of the geometries. Therefore, we try to index the **bounding boxes** of the geometry rather than the geometry itself. **R-Tree** is a common method for doing this. By storing these bounding boxes in an R-Tree index, the boxes can be quickly located and compared and the number of full geometry comparisons reduced before the geometry is ever read from disk.


## You might also like:
{: .t60 }
{% include list-posts tag='SQL' %}
