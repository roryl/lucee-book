# Java Integration

Lucee is built on Java and makes integrating with existing Java libraries in both directions (calling Java from Lucee, or Lucee from Java). This makes it possible to build parts of an application in Lucee which is a higher level language, and parts in Java, which has many existing libraries and may perform better for some use cases.

##Calling Java Classes
Because Lucee is a Java application, any of the Java library is available within Lucee scripts without any additional configuration. 

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

###Instantiating third party Java libraries
In order to use third party java libraries, Lucee must be able to find them. Like any Java application, Lucee will load any java libraries on the  classpath, but Lucee also supports dynamically loading libraries at runtime.

####Defining Java libraries in the Application.cfc
The Application.cfc can have a setting to tell Lucee where to find additional java libraries

`this.javaSettings = {LoadPaths = [".\java_lib\",".\java\myjar.jar"], loadColdFusionClassPath = true, reloadOnChange= true, watchInterval = 100, watchExtensions = "jar,class,xml"}`

| Paremeter | Description | Required? | Default Value |
| -- | -- | -- | -- |
| LoadPaths | An array of directories containing jar files or an array of paths to jar files. It will also accept a single directory or path to a Jar file| yes | |
| loadCFMLClassPath | Whether to load the underlying Lucee classes. This is only for advanced use cases and should be rare as functionality may change | yes | false |
| reloadOnChange | Instructs Lucee to reload the java libraries when they have changed without needing to restart the Lucee server | no | false |
| watchInterval | How many seconds to wait between checking for changes to the java libraries. This only applies if reloadOnChange is true | no | 60 |
| watchExtensions | Specifies which file extensions to watch for changes. By default only .class and .jar files are monitored | no | false

[Support for this.javasettings was added in Lucee version 4](https://issues.jboss.org/browse/RAILO-1971)


####Defining Java libraries during instantiation
For one off instatniations, its possible to define the jar files to load with the createObject function. 

`createObject('java',String className,String paths, String delimiter )`

| Parameter | Required | Default | Description |
| -- | -- | -- | -- |
| Type | yes |  | Must be 'java' to tell Lucee it is instantiating a Java object |
| Classname | yes |  | The Java class being instantiated, must be the full package and class name |
| Path | yes |  | An array or list of jar files or directories containing jar files |
| Delimiter | | , | The delimiter for the list of jar files, defaults to a comma  |

This example below shows loading the Handlebars.java library to use the Handlebars templating language inside Lucee.

{% gist id="https://gist.github.com/roryl/c8c5fd83bf367c70cd09",file="java_load_jar.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
//Load a comma separated list of jar files
Handlebars = createObject('java','com.github.jknack.handlebars.Handlebars','handlebars-4.0.3.jar,commons-lang3-3.1.jar,antlr4-runtime-4.5.1-1.jar').init();

//Load an array of jar files
Handlebars = createObject('java','com.github.jknack.handlebars.Handlebars',['handlebars-4.0.3.jar','commons-lang3-3.1.jar','antlr4-runtime-4.5.1-1.jar']).init();

//Dump the created java object
writeDump(Handlebars);
</cfscript>
```
</noscript>


Further Resources: 
https://github.com/getrailo/railo/wiki/Tutorial--Using-Java-in-Railo
