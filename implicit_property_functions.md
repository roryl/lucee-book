# Implicit Methods

Implicit Methods in Lucee allows treating getters and setter methods on a class as if they were public variables.

Consider the following component: 

{% gist id="roryl/c8c33b03651b5c4641a4a711799db735",file="basicComponent.cfc" %}{% endgist %}

<noscript>
```
component {
  
  public function setMyValue(string){
  	this.myValue = ucase(arguments.string);
  }

  public function getMyValue(){
  	return this.myValue;
  }
  
}
```
</noscript>

Normally, one would call the setter & getter methods, `setMyValue()` and `getMyValue()`, like the following:

{% gist id="roryl/c8c33b03651b5c4641a4a711799db735",file="default.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
myObj = new basicComponent();
myObj.setMyValue("foo");
echo(myObj.getMyValue());
</cfscript>
```
</noscript>

