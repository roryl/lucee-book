# Futures
Lucee has a number of [concurrency features](https://rorylaitila.gitbooks.io/lucee/content/concurrency.html) to aid in creating high performance applications. A modern approach to concurrency in Lucee is with the use of Futures, as provided via a [community extension](https://github.com/roryl/future.lucee/blob/master/README.md). See the [developing applications concurrency section](https://rorylaitila.gitbooks.io/lucee/content/concurrency.html) for a thorough review of Lucee's concurrency features.

>Note: The Futures library is an open source extension which can be obtained [its repository](https://github.com/roryl/future.lucee/blob/master/README.md)


Futures are used for executing code asynchronously from the currently executing request and providing a handle that can be passed to obtain the result of the asynchronous code when it completes. Lucee futures also have the additional capabilities in its future implementation:

* Asynchronous Callbacks
* Chaining Futures
* Yielding between Futures


##Creating a basic Future
Futures in Lucee are created with the futures component:

```
<cfscript>
future = new future(function(){
	sleep(2000);
	return "some value"
});

/*
//Code area running in the main thread
*/

//Blocks the currently executing thread and waits for the result to finish
echo(future.get());
</cfscript>
```

The future takes a closure, which the closure returns `some value` after a delay of 2000 milliseconds. The closure will be executed in a thread which will allow the main page thread to continue executing. When the main thread gets to `echo(future.get());`, the future blocks the page thread while waiting for the future to finish its execution.




