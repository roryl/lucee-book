# Style Guide

While each project and developer will settle on their own conventions, these are the common coding styles used in the Lucee commnuity.

##camelCase functions and components

Use camelCase for function names, whether built in, component functions or user defind functions

```
var file = fileNew();
```

A common convention is to upercase the first word of Components, but lower case any other variables

```
var MyObj = new MyObj();
var myArray = [];
```

##Tags lowercase

When using tags in templates like `<cfset>`, keep them lowercase

##Quote Attributes
Tags in Lucee can take strings or variables, for exmaple

`loop array=myArray index="i" {}` or `loop array="#myArray#" index="i" {}`

The common convention is to always quote attributes so that there is visual consistency in the attributes like in the second example above.

##Scope Non-local functions
Variables in Lucee can exist in one of many [scopes](https://rorylaitila.gitbooks.io/lucee/content/lifecycle_scopes.html), Local, Variables, This, Application, Session, etc. Lucee will look up the chain of available scopes to find a variable, but this costs performance and is unclear to other developers. The best practice is to always preface variables with the scope they are in, except for local function variables

```
<cfscript>
application.myVariable = "foo";

echo(myVariable); //outputs foo
echo(application.myVariable); //outputs foo
</cfscript>
```

Although in the proceeding example, both calls to myVariable will work (because Lucee will check all scopes for myVariable if it can't find it), the second `application.myVariable` is faster for Lucee to execute and is more clear.

Scoping variables is particularly important in the case of CFCs. The shared CFC variable state is the "variables" scope, and Lucee will put any unscoped variables into the variables scope by default. This can lead to subtle bugs and race conditions, so its always best to scope CFC variables too.

```
component {
   variables.myVariable = "foo";
   
   public function myFunc(){
     var myVariable = "bar";
     echo(myVariable); //outputs bar
     echo(variables.myVariable); //outputs foo
   }
}
```

##Var local variables
In Lucee, variables scopes to a local function are declared with the var keyword

```
function myFunc(){
  var myVariable = "foo";
}
```



It is also possible to use the "local" scope:
```
function myFunc(){
  local.myVariable = "foo";
}
```

Best practice is to use var for all local variables, and instantiate all variables at the top of the function, where possible. Although the var keyword can be used anywhere within the function if need be.

```
function myFunc(){
  var myVariable = "foo";
  var myOtherVariable = "bar";
  
  echo(myVariable);
}
```

Because Lucee always looks in the local scope first, convention is to not scope local variables `local.myVariable` and instead reference them directly. However take care to always `var` declare them first, otherwise they will be in the variables scope:

```
component {
   variables.myVariable = "foo";
   
   public function myFunc(){
     myVariable = "bar";
     echo(variables.myVariable); //outputs bar, because we did not declare a local variable it overwrote the `variables.myVariable`
     
   }
}
```




