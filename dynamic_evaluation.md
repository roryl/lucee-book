# Dynamic Evaluation
Sometimes it can be useful to run Lucee code which has been dynamically generated, or access variables which are dynamically generated. This can enable meta programming when you do not know the names of variables in advance.

##Dynamic Variables
The following code sets a dynamic variable "test" 

```
myVar = "test";
"#myVar#" = "foo";
echo(test); //outputs foo
```

##Evaluate
When doing more complex dynamic evaluations, you can make use of the evalute() function which will execute the Lucee code as if it was normally executed. This example below produces the same output as above. 
```
myVar = "test";
evaluate("#myVar# = 'foo'");
echo(test); //outputs foo
```
