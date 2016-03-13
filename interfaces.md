# Interfaces

Lucee supports Interfaces which Components can implment multiple interfaces. Combined with the use of Mixins, Lucee Interfaces can help type check and document concise code.

##Creating an Interface

Interfaces in Lucee are Components (files with the .cfc extension) but instead of defining a component, they define an interface:

{% gist id="https://gist.github.com/roryl/8b646c334f8d5658e9fe",file="IMyInterface.cfc" %}{% endgist %}

Function definitions are placed within the interface just like in components, except the function bodies are not implemented. 

<noscript>
```
interface {
  
  public function myFunc(required string myString){
  
  }
  
  public function myOtherFunc(required array myArray){
  
  }

}
```
</noscript>

##Implementing an Interface

Once an interface is created, a normal Component can be created that implements the interface

{% gist id="https://gist.github.com/roryl/8b646c334f8d5658e9fe",file="IMyInterfaceImpl.cfc" %}{% endgist %}

<noscript>
```
component implements="IMyInterface" {

  public function myFunc(required string myString){
    return arguments.myString;
  }
  
  public function myOtherFunc(required array myArray){
    return myArray;
  }
  
}
```
</noscript>

###Multiple Interfaces
Components can implement multiple interfaces by supplying a comma separated list for the implements attribute

{% gist id="https://gist.github.com/roryl/8b646c334f8d5658e9fe",file="implementsMultiple.cfc" %}{% endgist %}

<noscript>
```
component implements="IMyInterface,IOtherInterface" {

	public function myFunc(required string myString){
    	return arguments.myString;
  	}
  
  	public function myOtherFunc(required array myArray){
    	return myArray;
  	}

  	public function someOtherFunc(){
		
	}
}
```
</noscript>

> Note: If implementing multiple interfaces, all function definitions must be identical. Lucee does not currently support method overloading. 

##Using Interface Type Checking

###In Function Arguments
Function arguments can have a type annotation which checks that the object being passed in the argument conforms to the given interface. 

{% gist id="https://gist.github.com/roryl/8b646c334f8d5658e9fe",file="usesInterface.cfc" %}{% endgist %}

<noscript>
```
component {

	public function init(required IMyInterface object){
      //Will error if the object passed in did not implement IMyInterface
	}

}
```
</noscript>


###As a Return Type
Functions can have an Interface as a return type to ensure that the value returned from the function call implements the interface.

The following example shows a function getObject() which will ensure that the return value implements IMyInterface

{% gist id="https://gist.github.com/roryl/8b646c334f8d5658e9fe",file="returnsInterface.cfc" %}{% endgist %}

```
component {

	public function init(){
		return this;
	}

	public IMyInterface function getObject(){
		return new MyInterfaceImpl();
	}	

}
```

