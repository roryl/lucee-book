# Dynamic Evaluation
Sometimes it can be useful to run Lucee code which has been dynamically generated, or access variables which are dynamically generated. This can enable meta programming when the code or variable names cannot be known at compile time.

##Dynamic Variables
The following code sets a dynamic variable "test" 

{% gist id="https://gist.github.com/roryl/95f6bd166627abb425a4",file="dynamic_variable.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
myVar = "test";
"#myVar#" = "foo"; //set test = "foo" by evaluating myVar
echo(test); //outputs foo
</cfscript>
```
</noscript>

Its also possible to use the `getVariable()` function to dynamically evaluate a variable name:

{% gist id="https://gist.github.com/roryl/95f6bd166627abb425a4",file="get_variable.cfm" %}{% endgist %}


##Evaluate
When doing more complex dynamic evaluations, you can make use of the evalute() function which will execute any Lucee *expression* as if it was normally executed. This example below produces the same output as above. 

{% gist id="https://gist.github.com/roryl/95f6bd166627abb425a4",file="evaluate.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
myVar = "test";
evaluate("#myVar# = 'foo'"); //set test = "foo" by evaluating myVar
echo(test); //outputs foo
</cfscript>
```
</noscript>

##Dynamic Struct Array Notation
It is also possibly to dynamically access the members of a structure using array notation

{% gist id="https://gist.github.com/roryl/95f6bd166627abb425a4",file="dynamic_struct_keys.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
myVar = "test";
myStruct = {test:"foo"; test2:"bar"}
echo(myStruct[myVar]); //outputs "foo"
echo(myStruct["test2"]; //outputs "bar" 
</cfscript>
```
</noscript>

##Dynamic Lucee Code
Dynamically running Lucee tags or script that is more complex than simple expressions is usually not possible with evaluate(). In these situations, we can make use of Lucee's virtual filesystem to write and include dynamic code.

First it is necessary to create a mapping to the virtual file system. The mapping can be named anything, in this example it is named `temp`

{% gist id="https://gist.github.com/roryl/95f6bd166627abb425a4",file="Application.cfc" %}{% endgist %}

Then it is possible to dynamically create .cfm templates and include them. This example below compiles a template that outputs the time with a 50 milisecond delay, based on the number of iterations specified. 

{% gist id="https://gist.github.com/roryl/95f6bd166627abb425a4",file="dynamic_compilation.cfm" %}{% endgist %}

##ArgumentCollection
It is possible to pass to functions a dynamic set of arguments

