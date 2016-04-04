# Clustering

Clustering allows sharing Lucee session or client data among multiple Lucee server instances for load balancing and failover. Currently the only variable scopes that can be shared across the cluster are Session and Client variables. To share other types of data across instances, store the data in a database or cache that both instances have access to.

##Session Clustering
https://github.com/getrailo/railo/wiki/Using-database-for-session-data-storage

##Client Clustering
