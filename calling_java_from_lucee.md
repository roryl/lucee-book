# Calling Java from Lucee

Because Lucee is a Java application, any Java library can be used within Lucee. This article describes using Java libraries from within Lucee code. Java libraries you'll use in Lucee are typically of the following types:

* [Java Standard Library](#instantiating-a-java-standard-library-class)
* [Third Party Java Libraries](#instantiating-third-party-java-libraries)
* [Custom Java code](#compiling-and-running-java-source-files)

###Instantiating a Java standard library class
The entire Java standard library that ships with the JVM is available to Lucee code without any additional configuration.

To utilize a Java standard library class, it first must brought into Lucee, which is kind of like a class import. In Lucee, this is done with the createObject() function.

{% gist id="https://gist.github.com/roryl/c8c5fd83bf367c70cd09",file="create_java.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
javaArray = createObject("java", "java.util.ArrayList");
</cfscript>
```
</noscript>

The above merely readies the Java class but has not called any constructors. To call a constructor use the init() method:

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

`this.javaSettings = {LoadPaths = [".\java_lib\",".\java\myjar.jar"], loadCFMLClassPath = true, reloadOnChange= true, watchInterval = 100, watchExtensions = "jar,class,xml"}`

| Parameter | Required? | Default Value |  Description |
| -- | -- | -- | -- |
| LoadPaths | yes | | An array of directories containing jar files or an array of paths to jar files. It will also accept a single directory or path to a Jar file|
| loadCFMLClassPath | yes | false | Whether to load the underlying Lucee classes. This is only for advanced use cases and should be rare as functionality may change |
| reloadOnChange | no | false | Instructs Lucee to reload the java libraries when they have changed without needing to restart the Lucee server |
| watchInterval | no | 60 | How many seconds to wait between checking for changes to the java libraries. This only applies if reloadOnChange is true |
| watchExtensions | no | false |  Specifies which file extensions to watch for changes. By default only .class and .jar files are monitored |

[Support for this.javasettings was added in Lucee version 4](https://issues.jboss.org/browse/RAILO-1971)
> Note, there appears to be an issue with watchinterval and detecting changed classes https://luceeserver.atlassian.net/browse/LDEV-800 as a workaround, use the admin tag to restart the Lucee instance and pick up Java library changes:

```
<cfscript>
//Set the password to the password of your server administrator
admin action="restart" type="server" password="";
</cfscript>
```


####Defining Java libraries during instantiation
For one off instantiations, its possible to define the jar files to load with the createObject function. 

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
* https://github.com/getrailo/railo/wiki/Tutorial--Using-Java-in-Railo
* https://github.com/getrailo/railo/wiki/using_Railo_in_Java
* https://issues.jboss.org/browse/RAILO-1817
* Compiling Java in line: https://issues.jboss.org/browse/RAILO-2398

###Custom Java Code
Developing Lucee code (in .CFCs and .CFMs) does not require compiling, but Java source code files (.java file extension) do need to be compiled before instantiating. When working on a codebase where both the Java and Lucee code is being written, having to compile changes to Java classes and then test in Lucee can be tedious. It is possible to have Lucee compile .java files so that the normal save-file and browser refresh workflow is possible.

To have Lucee compile Java classes makes use of a function to compile the Java source code, described below, and the this.javasettings watchInterval as described above.