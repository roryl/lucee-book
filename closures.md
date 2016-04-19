# Closures

Closures are a name given to a type of [First Class Function](https://rorylaitila.gitbooks.io/lucee/content/first_class_functions.html) that when created, keep reference to the scopes from *where they were created*. This is useful because it allows passing the Closure around, just like passing a variable. But whereas a variable is simply a holder of a data element, a Closure is a function which contains references to the variables available during its creation. In Lucee, Closures can be assigned or they can be anonymous. Many of the functional features of Lucee require the use of Closures.

##Define a Closure via Function Expression

When setting a variable equal to a function, this creates a Closure. Any variables references inside the function have acess to the parent scopes from where they were created. This includes any local variables of parent functions, Components, and global scopes like application, session and request.

{% gist id="roryl/d14806856b35baeffc5e",file="basic_closure.cfm" %}{% endgist %}

<noscript>
```
myClosure = function(){

}
```
</noscript>


##Define a Closure via Anonymous Function
Many functions in Lucee like array.map() take a Closure as an argument, and these closures are defined inline without names

{% gist id="roryl/d14806856b35baeffc5e",file="anonymous_closure.cfm" %}{% endgist %}

<noscript>
```
var myArray = ["one","two","three"];
var newArray = myArray.map(function(value){
  return ucase(value);
});
dump(newArray); //outputs ONE, TWO, TREE
```
</noscript>

Here we passed an anonymous function (it had no name) to the map function.  For each element in the array, map called the closure and passed in the element.

##Closure Scopes Example
When creating closures, each closure contains references to its parents scopes, but parents do not have reference to the childs local scope. 

{% gist id="roryl/d14806856b35baeffc5e",file="closure_scopes_example.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
outerClosure = function(){
  var outer = "foo";
  
  innerClosure = function(){
    var inner = "bar";
    writeDump(outer); //dumps foo, shows that the inner can access the local scope of its parent
  }  

  writeDump(inner); //Errors for inner being undefined  	  
  
}

outerClosure(); //Call outer closure

otherClosure = function(){
  writeDump(outer); //Errors for being undefined
  writeDump(inner); //Errors for being undefined
}

otherClosure(); //Call the other closure showing that none of the interal variables can be accessed
</cfscript>
```
</noscript>





