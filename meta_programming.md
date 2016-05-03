# Meta Programming

Meta Programming in Lucee referes to the concept where method calls are not known in advance and are dynamically resolved. Lucee provides meta programming capabilities by allowing components to resolve method calls at runtime.

##A Meta Programming Use Case
An often useful programming pattern is the [Decorator Pattern](https://en.wikipedia.org/wiki/Decorator_pattern) wherein one class wraps another class in order to add additional functionality. For example, one could create a decorator to log all method calls.

Consider this component which implements some math functions:

{% gist id="roryl/1209cf05ae342beeecda87dd879b0150",file="README.md" %}{% endgist %}