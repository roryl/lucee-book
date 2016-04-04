# Clustering

Clustering allows sharing data among multiple Lucee server instances for load balancing and failover. Currently the only *variable scopes* that can be shared across the cluster are Session and Client variables. To share other types of data across instances, store the data in a database, or configure a distributed cache.

##Clustering Considerations
Sharing data across a cluster has drawbacks and is not a universal solution to all performance and data sharing needs. Implementing the following recommendations will make clustering easier to achieve.

###Load Balancers
Lucee itself does not provide routing and load balancing, as this is handled by a web server (Apache, IIS, NginX). Typically Lucee is installed with Apache, and this guide describes how to configure a basic Apache load balancer. However there are many load balancing solutions. If Lucee is configured for clustering, any load balancer that you deploy should work as well as any other at the Lucee layer.

###Stateless Applications
Avoid storing application and user state in global variables (application, session, client) if this data needs to be available and synchronized across the cluster. Every bit of data that needs to be shared opens up opportunity to race conditions or forgetting to synchronize the data. Instead, keep the Lucee application *stateless* by loading all of the data necessary for each request on every request, and then naturally any request can be served by any Lucee instance in the cluster. Only seek to share the data across the cluster which is causing performance bottlenecks.

###Use Sticky Sessions
When configuring your load balancer, *sticky sessions* will ensure that a single Lucee instance serves the same user for the entire time that the user is engaged. Using sticky sessions will limit opportunities for race conditions, where saving/reading session data is not synchronized in time across instances in the cluster between requests. This is most an issue in ajax heavy applications which may fire multiple requests to the cluster at the same time.


##Session Clustering
Multiple Lucee instances can share session data by storing the data a database.

https://github.com/getrailo/railo/wiki/Using-database-for-session-data-storage

##Client Clustering

##Cluster Cache
http://stackoverflow.com/questions/31053742/railo-lucee-ehcache-sessionstorage-not-synchronizing