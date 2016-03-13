# Dynamic Evaluation
Sometimes it can be useful to run Lucee code which has been dynamically generated, or access variables which are dynamically generated. This can enable meta programming when you do not know the names of variables in advance.

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
When doing more complex dynamic evaluations, you can make use of the evalute() function which will execute the Lucee code as if it was normally executed. This example below produces the same output as above. 

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
