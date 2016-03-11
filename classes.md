# Classes (Components)

In lucee, classes are called Components and have the file extension .cfc. Lucee supports many OOP class features like interfaces, inheritance, & public and private methods. They are called Components because Lucee classes are also used for implementing framework features like ORM & REST. To see these advanced usages of Components, refer to the Developing Applications section. The rest of this section will discuss standard OOP features. 

##Component Definition

<script src="https://gist.github.com/roryl/5a127d2d99c09924b3aa.js?file=empty_component.cfc"></script>

<noscript>
```
component {

}
```
</noscript>

##Default Constructor
In lucee, you may define a default constructor for your Component by providing a function called init. There can only be one constructor and Lucee does not support method overloading

<script src="https://gist.github.com/roryl/5a127d2d99c09924b3aa.js?file=default_constructor.cfc"></script>

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
You can define additional methods in your class, and they can have the following access levels:
* Public - Accessible to all callers
* Private - Accessible to only callers within this class
* Package - Accessible to other Components in a package
* Remote - Accessible to remote callers via web services, REST or invoking your components from HTTP

To define additional methods

<script src="https://gist.github.com/roryl/5a127d2d99c09924b3aa.js?file=single_function.cfc"></script>

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

See Types for a list of [Types](https://rorylaitila.gitbooks.io/lucee/content/types.html) that you can annotate your functions with.

###Method Arguments
In Lucee, method arguments can be optionally typed, optionally required, and have default values

####Typed Arguments

<script src="https://gist.github.com/roryl/5a127d2d99c09924b3aa.js?file=typed_arguments.cfc"></script>

<noscript>
```
component {
  public function myFunc(string argumentName1, struct argumentName2){
  }
}
```
</noscript>

####Required Arguments

<script src="https://gist.github.com/roryl/5a127d2d99c09924b3aa.js?file=required_arguments.cfc"></script>

<noscript>
```
component {
  public function myFunc(required argumentName1, required argumentName2){
  }
}
```
</noscript>

####Required & Typed Arguments

<script src="https://gist.github.com/roryl/5a127d2d99c09924b3aa.js?file=required_and_typed_arguments.cfc"></script>

<noscript>
```
component {
  public function myFunc(required string argumentName1, required struct argumentName2){
  }
}
```
</noscript>

####Default Arguments

<script src="https://gist.github.com/roryl/5a127d2d99c09924b3aa.js?file=default_arguments.cfc"></script>

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

<script src="https://gist.github.com/roryl/5a127d2d99c09924b3aa.js?file=new_object.cfm"></script>

```
<cfscript>
  myObj = new default_constructor();
</cfscript>
```

###CreateObject()
The createObject function is provided to instantiate Components, but also Java, Com and Webservice Objects. It also allows instantiating components with dynamic variable names

<script src="https://gist.github.com/roryl/5a127d2d99c09924b3aa.js?file=create_object.cfm"></script>

```
<cfscript>
  myObj = createObject("myComponent");
</cfscript>
```

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

<script src="https://gist.github.com/roryl/5a127d2d99c09924b3aa.js?file=component_implicit_path.cfc"></script>

<noscript>
```
component {    
   public function init(){
     myObj = new components.subComponent();   
   }  
}
```
</noscript>

You can also import Components to find them:

<script src="https://gist.github.com/roryl/5a127d2d99c09924b3aa.js?file=component_imported_path.cfc"></script>

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

If your Components are not accessible from the webroot and are stored elsewhere in your system or outside of the webroot for security (a best practice). You need to add an Application Mapping to access them. 


