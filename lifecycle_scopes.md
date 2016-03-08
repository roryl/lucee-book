# Lifecycle Scopes

Lucee has built in Scopes which are data holders that you can put your variables into and keep them around for specific durations. All of the scopes are accessible via dotted notation from anywhere that the scope is valid to access it. There are global scopes, and non-global scopes. 

To set a variable into a scope, you use dotted notation:

```
application.myVar = "foo"; //sets foo into myVar in the application scope
request.myVar = "bar"; //sets bar into myVar in the request scope
```

##Global Scopes
These variable scopes are available from any script executing within your application. The global scopes are:

###Application
Accessible for the entire life of your application until the applicationTimeout specified in the Application.cfc for your application. Care must be used when multiple requests are writing to the same application scoped variable. In these situations, use lock {} to syncronize write access. 

###Request
Accessible for the life of a single web request. You do not need to lock access to this scope unless you are using thread {} and possibly accessing a request scoped variable from multiple threads. 

###Session
Accessible for the life of a user session, until the sessionTimeout specified in Application.cfc is reached from no activity. Care must be used when multiple requests could come in from the same client simultaneously. In these situations, use lock {} to syncronize write access. 


##Localized Scopes

###Variables Scope
The Variables Scope is global to a single Component. Any variables declared in a Component without the var keyword default to this scope

###Local Scope
Any veriable instantiated within a function with the var keyword, lives in the local scope of that function and is not accessible to other functions in the Component or elsewhere. 
```
component {

  function myFunc(){
    var myVar = "foo";
    echo(myVar); //outputs "foo"
  }
  
  function otherFunc(){
    echo(myVar); //errors for undefined variable
  }
  
}
```
This this example above, only the myFunc has access to myVar. If you wanted all functions to access myVar, you should declare it in the variables scope. That would change the example to the following:

```
component {

  function myFunc(){
    variables.myVar = "foo";
    echo(myVar); //outputs "foo"
  }
  
  function otherFunc(){
    echo(myVar); //outputs "foo";
  }
  
}
```


