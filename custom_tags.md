# Custom Tags

Lucee allows extending the language with custom tags to add functionality to your views. Custom tags are typically used for view logic. You create cutom tags with CFCs and then import them into your page.

##Example View with a Custom Tag

Consider the following HTML template which uses a custom tag, called greeting.

{% gist id="roryl/f7fcd0fc09be6a207adba91b495c55b7",file="view.cfm" %}{% endgist %}

<noscript>
```
<html>
<head>
	<meta charset="UTF-8">
	<title>A Basic Custom Tag Example</title>
</head>
<body>
	<div>
		<cf_greeting firstName="Jim" lastName="Smith" />
	</div>
</body>
</html>
```
</noscript>

When running this script, it will output:

```
Hello Jim Smith,

The time is 06:43 AM
```

What happened here is we created a custom tag called greeting, passed a firstname & lastname to it, and the greeting tag generated the text for output. 

Here is what the greeting.cfc custom tag looks like. Further on in this articule it will be explained.

{% gist id="roryl/f7fcd0fc09be6a207adba91b495c55b7",file="greeting.cfc" %}{% endgist %}

<noscript>
```
component {

	/**
	 * Invoked during the start of the custom tag
	 * @param  {struct} required struct        attributes The attributes passed to the custom tag
	 * @param  {struct} required struct        caller     A reference to the variables scope from the location that calls the custom tag
	 * @return {boolean}          To control whether to execute the body of the custom tag
	 */
	public boolean function onStartTag(required struct attributes, required struct caller){

		param name="attributes.firstName";
		param name="attributes.lastName";
		writeOutput("<p>Hello #attributes.FirstName# #attributes.lastName#, </p>");
		writeOutput("<p>The time is #timeFormat(now(), "hh:mm tt")#</p>");
		return false;
	}

	/**
	 * Invoked after the completion of the closing tag
	 * @param  {struct} required struct        attributes The attributes passed to the custom tag
	 * @param  {struct} required struct        caller     A reference to the variables scope from the location that calls the custom tag
	 * @param  {string} string        output     The output generated between the start and end tags at the caller
	 * @return {boolean}          To control whether to execute the body of the custom tag
	 */
	public boolean function onEndTag(required struct attributes, required struct caller, string output){
		return false;
	}

}
```
</noscript>

##Calling Custom Tags
Before getting into how to build custom tags, its important to first know where Lucee looks for custom tags and how to call them. There are a few lookup rules:

1. Custom Tags in the same directory as the executing script
2. Custom Tags defined in a custom tag path
3. Custom Tags imported into the view

###Custom Tags in the Same Directory
If the custom tag is in the same directory as the view template executing the tag, Lucee can find the tag with the cf prefix. Consider the following directory structure (which is the structure of this example).

greeting.cfc
view.cfm
