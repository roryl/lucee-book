# Lifecycle Scopes

Lucee has built in Scopes which are data holders that can contain any variables and keep them around for a specific duration. All of the scopes are accessible via dotted notation from anywhere that the scope has valid to access it. 

There are three primary categorizations of scopes:

* [Global Scopes](#global-scopes)
* [Request Scopes](#request-scopes)
* [Localized Scopes](#localized-scopes)

It is also important to understand the [Scope Lookup/Cascading](#scope-lookup-cascading) rules. 

###Setting any variable into a scope
To set a variable into a scope, use dotted notation:

```
application.myVar = "foo"; //sets foo into myVar in the application scope
request.myVar = "bar"; //sets bar into myVar in the request scope
```

##Global Scopes
These variable scopes are available from any script executing within an application. The global scopes are:

###Application
Accessible for the entire life of the application, which is until the applicationTimeout specified in the Application.cfc expires. Care must be used when multiple requests are writing to the same application scoped variable. In these situations, use lock {} to syncronize write access.

###Session
Accessible for the life of a user session, until the sessionTimeout specified in Application.cfc is reached from no activity. Care must be used when multiple requests could come in from the same client simultaneously. In these situations, use lock {} to syncronize write access. 

###Cookie
Accessible for the life of a single request, the Cookie scope is created by Lucee based on the cookies provided by the user's browser. It contains the same data as is in the cgi.http_cookie variable, but it is parsed into  a structure for you like below

![](cookie_example.png)

###Client
Contains variables that should be persistent for a particular browser client. By default, client variables are stored as cookies, and so are synonymous with the cookie scope. However, client variables can also be stored is a database where a cookie ID is used to loop up the database entry and populate the client scope.

###Server
Server scoped variables exist for the life of a running Lucee instance.

###Cluster

##Request Scopes
These are scopes created and available for the live of a single web request. Once the request ends, any data set into these scopes is deleted.

###Request
Accessible for the life of a single web request.

###URL
Accessible for the life of a single request, the URL scope represents any URL query parameters passed
> yourdomain.com?arg1=foo&arg2=bar

###Form
Accessible for the life of a single request, the FORM scope represents any parameter which has been sent (Posted) to the application using an HTML form or javascript Ajax with POST

###CGI
Accessible for the life of a single request, the CGI scope (which stangs for Common Gateway Interface) is all of the web server variables passed to Lucee by Tomcat, Apache or any web server running in front of Lucee.

The full list of CGI variables is available in the [CGI Variables Reference](https://rorylaitila.gitbooks.io/lucee/content/cgi_variables.html)

It is not necessary to **read** lock access to any of the global scopes, only **write** access when there can potentially be a race condition of two clients writing to a global variable at the same time where use of that write could conflict.

##Localized Scopes

###Variables
The Variables Scope is global to a single Component. Any variables declared in a Component without the var keyword default to the variables scope. However, variables should always be explicitly scoped for readability and to prevent mistakes, and also slightly improves performance.

###Local
Any variable instantiated within a function with the var keyword, lives in the local scope of that function and is not accessible to other functions in the Component or elsewhere. 

{% gist id="roryl/08a89aa59430b797cdb4",file="component_local.cfc" %}{% endgist %}

<noscript>
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
</noscript>

In the example above, only the myFunc() function has access to myVar. If multiple functions need to access myVar, it should be declared it in the variables scope. That would change the example to the following:

{% gist id="roryl/08a89aa59430b797cdb4",file="component_variables.cfc" %}{% endgist %}

<noscript>
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
</noscript>

Variables should always be explicitly assigned to a scope, and use var for local variables. This will prevent subtle bugs that are hard to track if accidentally overriding a more global scope when it should have been a  local variable.

It is also possible to access local variables as a collection using the local structure. 

{% gist id="roryl/08a89aa59430b797cdb4",file="component_local_struct.cfc" %}{% endgist %}

<noscript>
```
component {
	function myFunc(){
	  var myVar = "foo";
	  echo(local.myVar); //outputs foo
	}	
}
```
</noscript>

###Arguments
The arguments scope is available inside any function

###This
The This scope is the public interface of a Component. Any variables set to this, will be accessible from outside the component. 

###Attributes
The attributes scope is a special scope used only in custom tags

###Caller
The caller scope is a special scope used only in custom tags

###Thread
The thread scope is created when creating a new thread{} in Lucee. Any variables passed to the thread at put in the thread scope, and exist until the thread finishes.

##Scope Lookup / Cascading
Lucee looks for variables starting from the most specific all the way up to the most global. If a variable is not scoped, Lucee will search all scopes for it. This can be a performance penalty if doing a lot of lookups, therefore follow the [style guide for scoping variables](https://rorylaitila.gitbooks.io/lucee/content/style_guide.html#scope-nonlocal-variables)

The order in which Lucee looks up scopes is:


