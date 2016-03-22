# Classes (Components)

In lucee, classes are called Components and have the file extension .cfc. Lucee supports many OOP class features like interfaces, inheritance, & public and private methods. They are called Components because Lucee classes are also used for implementing framework features like ORM & REST. To see these advanced usages of Components, refer to the Developing Applications section. The rest of this section will discuss standard OOP features. 

##Component Definition

{% gist id="https://gist.github.com/roryl/5a127d2d99c09924b3aa",file="empty_component.cfc" %}{% endgist %}

<noscript>
```
component {

}
```
</noscript>

##Implicit Constructor
Any code within the body of the component before any functions are defined is known as the "implicit constructor". This code will be executed on each instantiation of the CFC no matter the instantiation method. This can be used for code which must always be run. This was the original constructor strategy for Lucee, but most applications today use the Default Constructor described below.

##Default Constructor
In lucee, components may have a default constructor method by providing a function called init. There can only be one constructor and Lucee does not support method overloading

{% gist id="https://gist.github.com/roryl/5a127d2d99c09924b3aa",file="default_constructor.cfc" %}{% endgist %}


<noscript>
```
component {
  function init(){
    //Do something on instantiation 
    return this;
  }
}
```
</noscript>

##Methods
Components can define additional methods and they can have the following access levels:
* Public - Accessible to all callers
* Private - Accessible to only callers within this class
* Package - Accessible to other Components in a package
* Remote - Accessible to remote callers via web services, REST or invoking components from HTTP

To define additional methods

{% gist id="https://gist.github.com/roryl/5a127d2d99c09924b3aa",file="single_function.cf" %}{% endgist %}


<noscript>
```
component {
  public void function myFunction(){
    
  }
}
```
</noscript>

The above declaration represents the following
```
  [access] [return type] function [function name](){
  
  }  
```

See Types for a list of [Types](https://rorylaitila.gitbooks.io/lucee/content/types.html) that functions can be annotated with.

###Method Arguments
In Lucee, method arguments can be optionally typed, optionally required, and have default values

####Typed Arguments

{% gist id="https://gist.github.com/roryl/5a127d2d99c09924b3aa",file="typed_arguments.cfc" %}{% endgist %}


<noscript>
```
component {
  public function myFunc(string argumentName1, struct argumentName2){
  }
}
```
</noscript>

####Required Arguments

{% gist id="https://gist.github.com/roryl/5a127d2d99c09924b3aa",file="required_arguments.cfc" %}{% endgist %}


<noscript>
```
component {
  public function myFunc(required argumentName1, required argumentName2){
  }
}
```
</noscript>

####Required & Typed Arguments

{% gist id="https://gist.github.com/roryl/5a127d2d99c09924b3aa",file="required_and_typed_arguments.cfc" %}{% endgist %}

<noscript>
```
component {
  public function myFunc(required string argumentName1, required struct argumentName2){
  }
}
```
</noscript>

####Default Arguments

{% gist id="https://gist.github.com/roryl/5a127d2d99c09924b3aa",file="default_arguments.cfc" %}{% endgist %}

<noscript>
```
component {
  public function myFunc(required string argumentName1="test", required struct argumentName2={key:"value"}){
  }
}
```
</noscript>


##Instantiation
###New Operator
Using the New Operator, Lucee will instantiate the class and call the default constructor (if it exists)

{% gist id="https://gist.github.com/roryl/5a127d2d99c09924b3aa",file="new_object.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
  myObj = new default_constructor();
</cfscript>
```
</noscript>

###CreateObject()
The createObject function is provided to instantiate Components, but also Java, Com and Webservice Objects. It also allows instantiating components with dynamic variable names.

{% gist id="https://gist.github.com/roryl/5a127d2d99c09924b3aa",file="create_object.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
  myObj = createObject("myComponent");
</cfscript>
```
</noscript>

##Component Lookup Rules
When instantiating components they are found in the following ways
* Any Components that are in the same directory as the script instantiating the component
* Any Components imported into the script using the import keyword
* Any Components pathed to using dotted notation, starting from the webroot
* Any Components pathed to using dotted notation, that can be found from a mapping in Application.cfc

For Example, consider the following structure

- /MyWebApp
  - /components
    - subComponent.cfc
  - Application.cfc
  - rootComponent.cfc
  - index.cfm

We're going to instantiate subComponent.cfc from within rootComponent.cfc and index.cfm runs our application. 

rootComponent.cfc:
This will find the subComponent because it can be pathed from the webroot (/components/subComponent)

{% gist id="https://gist.github.com/roryl/5a127d2d99c09924b3aa",file="component_implicit_path.cfc" %}{% endgist %}

<noscript>
```
component {    
   public function init(){
     myObj = new components.subComponent();   
   }  
}
```
</noscript>

Components can also be imported:

{% gist id="https://gist.github.com/roryl/5a127d2d99c09924b3aa",file="component_imported_path.cfc" %}{% endgist %}

<noscript>
```
import components.subComponent;
component {    
   public function init(){
     myObj = new subComponent();   
   }  
}
```
</noscript>

Notice that the import pathed from the webroot, but then we instantiated the component directly. 

If Components are not accessible from the webroot and are stored elsewhere in on the file system system or outside of the webroot for security (a best practice), then they need an [Application Mapping](https://rorylaitila.gitbooks.io/lucee/content/mappings_class_paths.html) to access them. 


