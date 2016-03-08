# Lifecycle Scopes

Lucee has built in Scopes which are data holders that you can put your variables into and keep them around for specific durations. All of the scopes are accessible via dotted notation from anywhere that the scope is valid to access it. There are global scopes, and non-global scopes. 

To set a variable into a scope, you use dotted notation:

```
application.myVar = "foo"; //sets foo into myVar in the application scope
request.myVar = "bar"; //sets bar into myVar in the request scope
```

##Global Scopes
These variable scopes are available from any script executing within your application. The global scopes are:

Application
Request
Session
Cluster

##localized Scopes

###Variables Scope
The Variables Scope is global to a single Component. Any variables declared in a Component without the var keyword default to this scope

###Local Scope
Any veriable instantiated within a function with the var keyword, lives in the local scope of that function and is not accessible to other functions in the Component or elsewhere. 
```
function myFunc(){
  var myVar = "foo";
}
```

