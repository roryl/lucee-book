# Implicit Accessor Methods

Implicit Accessor Methods in Lucee allows treating getters and setter methods on a component as if they were public variables. To enable this feature, it requires an override in the Application.cfc

{% gist id="roryl/c8c33b03651b5c4641a4a711799db735",file="Application.cfc" %}{% endgist %}

<noscript>
```
component {
	this.triggerDataMember=true;
}
```
</noscript>

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

However, it is possible to access the variables in the public `this` scope, and Lucee will look for any setters & getters and call them instead, if they exist:

{% gist id="roryl/c8c33b03651b5c4641a4a711799db735",file="implicit.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
myObj = new basicComponent();
myObj.MyValue = "foo";
echo(myObj.MyValue);
</cfscript>
```
</noscript>