# Serialization

Serialization allows turning any complex objects (Components, Arrays, Structs, Queries) into a string representation that can be transferred or stored. The two common scenarios for serialization are 1) Persisting complex Lucee objects to a database or file system, or transfering them between systems, and 2) Turning objects into Json for an API or client use.

* Persisting Complex Objects
* Serializing to Json

##Persisting & Transferring Complex Objects
There are sometimes use cases for saving objects to persistent storage directly, and loading them back, without saving the object's data into a structured data store like a SQL database. There are also times when say a Component might want to be transfered between systems, but creating a formal API is overfill. As long as the system both writing and reading the serialized objects is Lucee, any object in Lucee can be saved and recreated.

> To serialize (turn it into text) any Lucee object, use the `serialize()` function

> To deserialize (get back a real object) any Lucee object, use the `evaluate()` function

###Serialization Example
This example serializes a simple structure with a nested query structure with a row of data.

<noscript>
```
<cfscript>
<cfscript>
myStruct = {foo:"bar", baz:queryNew("test","varchar",[{test:"my data"}])};
structText = serialize(myStruct);
echo(structText);
</cfscript>
```
</noscript>

The output of the echo is:

`{'BAZ':query('test':['my data']),'FOO':'bar'}`

When Lucee serializes complex objects, notice how it is very similar to Json, but there are differences. For exmaple, the query is turned into a function `query()` which when deserialized, will create the query again. This is something not possible in Json.

To get the structure back, use the `evaluate()` function:

<noscript>
```
<cfscript>
structText = "{'BAZ':query('test':['my data']),'FOO':'bar'}";
myStruct = evaluate(structText);
writeDump(myStruct);
</cfscript>
```
</noscript>

Which the above example outputs:

![](serialize_struct_dump.png)


Here is an example of serializing a Component:

First, a basic component:

<noscript>
```
component {
  this.foo = "bar";
  function init(){
    //Do something on instantiation 
    return this;
  }
}
```
</noscript>

Then serialize the component:

<noscript>
```
<cfscript>
myComponent = new basicComponent();
componentText = serialize(myComponent);
echo(componentText);
</cfscript>
```
</noscript>

It results in the output:

`evaluateComponent('examples.serialization.basicComponent','c31d231165a410c67a9a8c57da575e88',{'FOO':'bar'},{})`

Which this can be deserialized back into the original component


<noscript>
```
<cfscript>
componentText = "evaluateComponent('examples.serialization.basicComponent','c31d231165a410c67a9a8c57da575e88',{},{})";
myComponent = evaluate(componentText);
writeDump(myComponent);
</cfscript>
```
</noscript>



