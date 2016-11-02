# Syntax

There are two flavors to the Lucee Language, Tags and Script. The entire language is available in Tags or Script. Tags are intended to mix well with HTML and should (almost always) only be used in HTML templates.

* [See a detailed review of script syntax ](https://github.com/adamcameron/cfscript/blob/master/cfscript.md)
* [See a synxtax cheat sheet](https://rorylaitila.gitbooks.io/lucee/content/script_cheat_sheet.html)

## Quick Overview

### Script
The script based language resembles javascript 

{% gist id="roryl/5817942eccef2bad2281",file="setting_a_variable.cfm" %}{% endgist %}

<noscript>
```
myVar = "test";
```
</noscript>

The trailing ";" denoting the end of the statement can be ommitted as long as new statements are on a new line, but convention is to keep the ";"

Lucee script supports all Tags in script by simply wrapping the code block in brackets

{% gist id="roryl/5817942eccef2bad2281",file="script_tags.cfm" %}{% endgist %}

<noscript>
```
savecontent variable="myContent {
  echo("Output some test");
}
```
</noscript>

View the [script reference](https://rorylaitila.gitbooks.io/lucee/content/script_cheat_sheet.html) for all language constructs

### Tags 

The tag based language loosely resembles HTML.

{% gist id="roryl/5817942eccef2bad2281",file="setting_a_variable_tag.cfm" %}{% endgist %}

<noscript>
```
<cfset myVar = "test">
```
</noscript>

Tags can have bodies or not. Tags without bodies do not need a closing bracket, but some people prefer them stylistically 

{% gist id="roryl/5817942eccef2bad2281",file="optional_closing.cfm" %}{% endgist %}

<noscript>
```
<cfset myVar = "test" />
```
</noscript>

Tags with bodies always need a closing tag

{% gist id="roryl/5817942eccef2bad2281",file="closing_tag_bodies.cfm" %}{% endgist %}

<noscript>
```
<cfsavecontent variable="myContent">
  Output some text
</cfsavecontent>
```
</noscript>

