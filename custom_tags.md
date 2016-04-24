# Custom Tags

Lucee allows extending the language with custom tags to add functionality to view templates. Custom tags are typically used for view logic. Custom tags are created with CFCs and then imported into a view, or Application.cfc

This article shows a brief example, then read these additional articles:

1. Calling Custom Tags
2. Creating Custom Tags

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

Here is what the greeting.cfc custom tag looks like. The article on Creating Custom Tags explains in depth.

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




