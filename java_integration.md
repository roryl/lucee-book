# Java Integration

Lucee is built on Java and makes integrating with existing Java libraries in both directions (calling Java from Lucee, or Lucee from Java). This makes it possible to build parts of your application in Lucee which is a higher level language, and parts in Java, which has many existing libraries and may perform better for some use cases.

##Calling Java Classes
Because Lucee is a Java application, any of the Java standard library is available within your Lucee scripts. 

###Instantiating a Java class
The first thing you need to do is akin to importing the java class that you want to use. In Lucee, we use the createObject() function to do this.

```
javaArray = createObject("java", "java.util.ArrayList");
```
The above merely readies the Java class but has not called any constructors. To call the constructor we use the init() method:

```
javaArray = javaArray.init();
```
This will initialize the Java class matching a constructor whose arguments match what was passed into the init function. Now the class is fully instantiated and we can call methods on it:

```
echo(javaArray.size()); //outputs the size of the array
```