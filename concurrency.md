# Concurrency
Lucee applications are by default concurrent per request. Each request to Lucee runs in its own thread, with its own request scope to store data for that request. Lucee provides additional concurrency features for concurrent execution within a single request.

##Parallel Functions
Lucee has the collection methods, map(), each(), every(), reduce(), some(), filter() which can be used to operate on arrays, structs & query data in parallel, and also used to execute code asynchronously.

Parallel functions are the easiest to use when some code can be exeucted concurrently but control must be returned (execution blocked) until all of the executions are complete.

##Futures
Using the community developed [Lucee Future library](https://github.com/roryl/future.lucee/blob/master/README.md), you can asynchronously execute code and retrieve the result at a later time. This is a syntax sugar over the native threading capabilities.

##Tasks
Tasks are a method to fire off additional processing which runs independent of the current request, and the response of the task is not used in the request. This is the method to use when the executing code needs to run in its own full HTTP request thread and not share the current request. This makes use of Lucee's Scheduled tasks functionality. 

##Threading
Lucee provides access to directly create Java threads to asynchronously execute blocks of code. This type of concurrency provides primitives to create, block and terminate threads. It is a more manual approach, but can provide for more complex scenarios like running a background task at the beginning of a request, continuing with the request, and then blocking and retrieving the background value at the end. As this is more involved, use of the preceding methods is recommended for most cases.
