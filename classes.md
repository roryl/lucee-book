# Classes (Components)

In lucee, classes are called Components and have the file extension .cfc. Lucee supports many OOP class features like interfaces, inheritance, & public and private methods. They are called Components because Lucee classes are also used for implementing framework features like ORM & REST. To see these advanced usages of Components, refer to the Developing Applications section. The rest of this section will discuss standard OOP features. 

##Component Definition
```
component {

}
```
>Save this file as myClass.cfc to create your Component



##Default Constructor
In lucee, you may define a default constructor for your Component. There can only be one constructor and Lucee does not support method overloading

```
component {
  function init(){
    return this;
  }
}
```

##Methods

##Invocation

