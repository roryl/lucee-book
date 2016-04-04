# Clustering

Clustering allows sharing data among multiple Lucee server instances for load balancing and failover. Currently the only *variable scopes* that can be shared across the cluster are Session and Client variables. To share other types of data across instances, store the data in a database, or configure a distributed cache.

##Clustering Considerations
Sharing data across a cluster has drawbacks and is not a universal solution to all performance and data sharing needs. Implementing the following recommendations will make clustering easier to achieve.

###Stateless Applications
Avoid storing application and user state in global variables (application, session, client) if this data needs to be available and synchronized across the cluster. Every bit of data that needs to be shared opens up opportunity to race conditions or forgetting to synchronize the data. Instead, keep the application *stateless* Load all of the data necessary for each request on every request, and then naturally a request can be served by any Lucee instance in the cluster. 



##Session Clustering

https://github.com/getrailo/railo/wiki/Using-database-for-session-data-storage

##Client Clustering

##Cluster Cache
http://stackoverflow.com/questions/31053742/railo-lucee-ehcache-sessionstorage-not-synchronizing