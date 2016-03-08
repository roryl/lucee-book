# Caching
Simple applications usually do not need caching but as your application grows more complex, you may need to employ caching strategies to speed up execution. You should always try to avoid caching until it is necessary. Caching data can add complexity to your application, and that complexity has to be worth it. If you are not seeing any slowness in your application yet, then don't bother caching.

Lucee has one of the most robust caching solutions on the market and caching is available at every level, even in the language syntax itself. The right type of caching you need to use depends on the performance constraints of your particular application and the structure of your code. Typically, go for the easiest thing that works!

This section gives an overview of the available caching features.

##Template Caching
Lucee can cache whole Lucee HTML templates so that they are only generated once, and then subsequent requests are from the cache

##Query Caching
Lucee can cache your SQL queries by reading the content of your SQL Statements and saving the results. It know when you make the same query again, and it serves the data from the cache. This is like caching in your SQL server, but gives you control from within Lucee.

##Object Caching
Lucee can cache any object or variable that you create into a cache, and you can retrieve it as needed.

##Function Caching
Lucee has language level support for caching the results of functions based on the arguments supplied. This makes quick work of speeding up complex functions.

##Template Fragment Caching
If you need only part of a Lucee template to be cached, but the remainingh part to stay dynamic, you can acheive this with Template Fragment caching

##Persistent Scope Caching
Lucee implements a number of persistent variable scopes, Application, Session, Client & cluster, which can be used for simple caching scenarios

##ORM Caching
The Lucee ORM supports caching ORM Entities to reduce load on the underlying datasource and speed up large number of entities

##RAM Disk Caching
Lucee can load files (images, CSVs, videos, etc) into RAM disk and operat on those files in RAM which is significantly faster than the local file system in many cases





