# Meta Programming

Meta Programming in Lucee referes to the concept where method calls are not known in advance and are dynamically resolved. Lucee provides meta programming capabilities by allowing components to resolve method calls at runtime.

##A Meta Programming Use Case
An often useful programming pattern is the [Decorator Pattern](https://en.wikipedia.org/wiki/Decorator_pattern) wherein one class wraps another class in order to add additional functionality. For example, one could create a decorator to log all method calls.

Consider this component which implements some math functions- add, multiply and subtract:

{% gist id="roryl/1209cf05ae342beeecda87dd879b0150",file="math.cfc" %}{% endgist %}

If the use case was that every time we called one of the math methods we wanted to output some text, we could solve it by creating a decorator which reproduces and wraps the math object. Consider this decorator which simply re-implements the functions of math.cfc, adds the new functionality, and forwards the calls to match.cfc: 

{% gist id="roryl/1209cf05ae342beeecda87dd879b0150",file="mathDecoratorBasic.cfc" %}{% endgist %}

To execute this decorator run:

{% gist id="roryl/1209cf05ae342beeecda87dd879b0150",file="use_math_basic.cfm" %}{% endgist %}

Which outputs:

```
You are trying to add 5 and 7 
The result was 12 
You are trying to multiply 2 and 10 
The result was 12 
You are trying to subtract 20 and 6 
The result was 26 
```

This works as expected but in this decorator there is a lot of similar code in each wrapper function. Also each and every function has to be wrapped, which is easy if there are only a few functions, but if there were dozens it could be a lot of tedious coding. 

Lucee has a metaprogramming feature called onMissingMethod which allows implementing a decorator pattern like the above in a lot less code. If an `onMissingMethod()` function is defined, Lucee will call this whenever a method invocation is made on the component and the method does not exist. With onMissingMethod, the decorator can be written dynamically as follows:

{% gist id="roryl/1209cf05ae342beeecda87dd879b0150",file="mathDecorator.cfc" %}{% endgist %}

**onMissingMethod takes the following arguments:**

| Name | Type | Description |
| -- | -- | -- |
| missingMethodName | string |  The name of the method that was being called |
| missingMethodArguments | struct | A structure of the arguments passed to the function call |

**Walking through each line of the implementation:**

1. First we use the missing method name to output what method was being called, and the value of the arguments passed:
```
echo("You are trying to #missingMethodName# #missingMethodArguments[1]# and #missingMethodArguments[2]# <br />");
```

2. Then we instantiate the math component
```
var math = new math();
```

3. Then making use of the [dynamic evaluation](https://rorylaitila.gitbooks.io/lucee/content/dynamic_evaluation.html#evaluate) function, we call the method that was originally intended, passing in all of the arguments using Lucee's dynamic argumentCollection feature
```
var result = evaluate("math.#missingMethodName#(argumentCollection=missingMethodArguments)");
```

4. Lastly we echo the result:
```
echo("The result was #result#");
```

Now we can use this new mathDecorator:

{% gist id="roryl/1209cf05ae342beeecda87dd879b0150",file="use_math.cfm" %}{% endgist %}

And it outputs the following:

```
You are trying to add 5 and 7 
The result was 12You are trying to multiply 2 and 10 
The result was 20You are trying to subtract 20 and 6 
The result was 14
```
		
		
		


