# Concurrency
Lucee applications are by default concurrent per request. Each request to Lucee runs in its own thread, with its own request scope to store data for that request. Lucee provides additional concurrency features for concurrent execution within a single request.

##Parallel Functions
Lucee has the collection methods, map(), each(), every(), reduce(), some(), filter() which can be used to operate on arrays, structs & query data in parallel, and also used to execute code asynchronously.

Parallel functions are the easiest to use when some code can be exeucted concurrently but control must be returned (execution blocked) until all of the executions are complete.

##Tasks


##Threading

