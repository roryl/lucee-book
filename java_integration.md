# Java Integration

Lucee is built on Java and makes integrating with existing Java libraries in both directions (calling Java from Lucee, or Lucee from Java). This makes it possible to build parts of an application in Lucee which is a higher level language, and parts in Java, which has many existing libraries and may perform better for some use cases.

##Calling Java Classes
Because Lucee is a Java application, any of the Java standard library is available within Lucee scripts without any additional configuration. 

###Instantiating a Java standard library class
The first thing to do is akin to importing the java class that is to be used. In Lucee, this is done with the createObject() function.

{% gist id="https://gist.github.com/roryl/c8c5fd83bf367c70cd09",file="create_java.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
javaArray = createObject("java", "java.util.ArrayList");
</cfscript>
```
</noscript>

The above merely readies the Java class but has not called any constructors. To call the constructor use the init() method:

{% gist id="https://gist.github.com/roryl/c8c5fd83bf367c70cd09",file="initialize_java.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
javaArray = javaArray.init();
</cfscript>
```
</noscript>

This example above initialized the Java class matching a constructor whose arguments match what was passed into the init function. Now the class is fully instantiated and methods can be called on it like in the example below:

{% gist id="https://gist.github.com/roryl/c8c5fd83bf367c70cd09",file="output_java.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
javaArray = createObject("java", "java.util.ArrayList");
javaArray = javaArray.init();
echo(javaArray.size()); //outputs the size of the array
</cfscript>
```
</noscript>

The above example does not have to be so verbose, it is possible to accomplish the same all in one line:

{% gist id="https://gist.github.com/roryl/c8c5fd83bf367c70cd09",file="inline_java.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
echo(createObject("java", "java.util.ArrayList").init().size()); //outputs the size of the array
</cfscript>
```
</noscript>

