# Lifecycle Scopes

Lucee has built in Scopes which are data holders that can contain any variables and keep them around for specific durations. All of the scopes are accessible via dotted notation from anywhere that the scope is valid to access it. There are global scopes, and non-global scopes. 

To set a variable into a scope, use dotted notation:

```
application.myVar = "foo"; //sets foo into myVar in the application scope
request.myVar = "bar"; //sets bar into myVar in the request scope
```

##Global Scopes
These variable scopes are available from any script executing within an application. The global scopes are:

###Application
Accessible for the entire life of the application, which is until the applicationTimeout specified in the Application.cfc expires. Care must be used when multiple requests are writing to the same application scoped variable. In these situations, use lock {} to syncronize write access. 

###Request
Accessible for the life of a single web request. It is not necessary to lock access to this scope unless using thread {} and thus possibly accessing a request scoped variable from multiple threads. 

###Session
Accessible for the life of a user session, until the sessionTimeout specified in Application.cfc is reached from no activity. Care must be used when multiple requests could come in from the same client simultaneously. In these situations, use lock {} to syncronize write access. 

###URL
Accessible for the life of a single request, the URL scope represents any URL query parameters passed
> yourdomain.com?arg1=foo&arg2=bar

###Form
Accessible for the life of a single request, the FORM scope represents any parameter which has been sent (Posted) to the application using an HTML form or javascript Ajax with POST

###CGI
Accessible for the life of a single request, the CGI scope (which stangs for Common Gateway Interface) is all of the web server variables passed to Lucee by Tomcat, Apache or any web server running in front of Lucee.

The full list of CGI variables is available in the [CGI Variables Reference](https://rorylaitila.gitbooks.io/lucee/content/cgi_variables.html)

It is not necessary to **read** lock access to any of the global scopes, only **write** access when there can potentially be a race condition of two clients writing to a global variable at the same time.


##Localized Scopes

###Variables Scope
The Variables Scope is global to a single Component. Any variables declared in a Component without the var keyword default to the variables scope. However, you should always explicitly scope your variables for readability and to prevent mistakes.

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
    echo(variables.myVar); //same as above, outputs "foo"
  }
  
}
```
You should always explicitly state the scope of your variables, and use var for your local variables. This will prevent subtle bugs that are hard to track.

It is also possible to access local variables as a collection using the local structure. 
```
function myFunc(){
  var myVar = "foo";
  echo(local.myVar); //outputs foo
}

```

