# Closures

Closures are a name given to a kind of [First Class Function](https://rorylaitila.gitbooks.io/lucee/content/first_class_functions.html) but when created,keep reference to the scopes from *where they were created*. This is useful because it allows you to pass the Closure around, just like passing a variable. But whereas a variable is simply a holder of a data element, a Closure is a function which containsreferences to its creation. In Lucee, Closures can be assigned or they can be anonymous. Many of the functional features of Lucee require the use of Closures.

##Define a Closure via Function Expression

When setting a variable equal to a function, this creates a Closure. Any variables references inside the function have the scope from where they were created.

{% gist id="https://gist.github.com/roryl/d14806856b35baeffc5e" %}{% endgist %}

<noscript>
```
myClosure = function(){

}
```
</noscript>


##Define a Closure via Anonymous Function
Many functions in Lucee like array.map() take a Closure as an argument, and these closures are defined inline without names
```
var myArray = ["one","two","three"];
var newArray = myArray.map(function(value){
  return ucase(value);
});
dump(newArray); //outputs ONE, TWO, TREE
```

Here we passed an anonymous function (it had no name) to the map function.





