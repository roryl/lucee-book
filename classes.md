# Classes (Components)

In lucee, classes are called Components and have the file extension .cfc. Lucee supports many OOP class features like interfaces, inheritance, & public and private methods. They are called Components because Lucee classes are also used for implementing framework features like ORM & REST. To see these advanced usages of Components, refer to the Developing Applications section. The rest of this section will discuss standard OOP features. 

##Component Definition
```
component {

}
```
>Save this file as myClass.cfc to create your Component



##Default Constructor
In lucee, you may define a default constructor for your Component by providing a function called init. There can only be one constructor and Lucee does not support method overloading

```
component {
  function init(){
    //Do something on instantiation 
    return this;
  }
}
```

##Methods
You can define additional methods in your class, and they can have the following access levels:
* Public - Accessible to all callers
* Private - Accessible to only callers within this class
* Package - Accessible to other Components in a package
* Remote - Accessible to remote callers via web services, REST or invoking your components from HTTP

To define additional methods
```
component {
  public void function myFunction(){
    
  }
}
```

The above declaration represents the following
```
  [access] [return type] function [function name](){
  
  }  
```

See Types for a list of Types that you can annotate your functions with.

###Method Arguments




##Instantiation

