# Using Lucee to Compile .Java

For major Java programming, it is recommended to use a full Java IDE, however if you are just wanting to work with a couple Java classes, Lucee with the help of a third party library can compile Java classes.

To use the examples below, you'll need a copy of JAR file for the [Eclipse IDE Java Compiler](http://mvnrepository.com/artifact/org.eclipse.jdt.core.compiler/ecj/4.2.2)

The following Application.cfc will compile any Java classes it finds in its containing folder 

{% gist id="roryl/3580c74e7749ba8bd7e7d7d07278cc66",file="Application.cfc" %}{% endgist %}

```
<noscript>
component {
  	this.javaSettings = {LoadPaths = ["./"], loadCFMLClassPath = true, reloadOnChange= true, watchInterval = 2, watchExtensions = "jar,class,xml"}

 	function onRequestStart(){ 		
 		compileClasses(); 		
 	}

	  /**
	 * compiles all .java files in /WEB-INF/lucee/classes via the ECJ BatchCompiler
	 * lucee code added to classpath via the jars in System classpath and the latest rc patch
	 */
	function CompileClasses() {
	 
	    var java = {	 
	          System        : createObject( 'java', 'java.lang.System' )
	        , PrintWriter   : createObject( 'java', 'java.io.PrintWriter' )
	        , StringWriter  : createObject( 'java', 'java.io.StringWriter' )
	        , BatchCompiler : createObject( 'java', 'org.eclipse.jdt.core.compiler.batch.BatchCompiler', 'ecj-4.2.2.jar' )
	    };
	 
	    var src = expandPath( '' );
	        
	    var rc  = arrayLast( directoryList( expandPath( '{lucee-server}/../patches' ) ) );
	    var cp = java.System.getProperty( "java.class.path" );      // all libs from System classpath        
	    cp &= Server.separator.path & rc;                           // add the lucee-Core to classpath
	 	// writeDump(cp);
	 	// abort;
	 
	    var out = java.StringWriter.init();     
	    var outWriter = java.PrintWriter.init( out, true );
	 
	    var cmd = "-cp #cp# #src#";
	 
	    outWriter.println( "Compiler Command: " & cmd );
	 
	    java.BatchCompiler.compile( cmd, outWriter, outWriter, javaCast( 'null', '' ) );
	    
	    outWriter.println( "Done." );
	    
	    var result = out.getBuffer().toString().trim();
	    writeDump(result);
	    return result;
	}
}
</noscript>
```

This method was found from: https://issues.jboss.org/browse/RAILO-2398



