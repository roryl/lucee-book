# Syntax

There are two flavors to the Lucee Language, Tags and Script. The entire language is available in Tags or Script. Tags should (almost always) only be used for HTML templates.

* [See a detailed review of script syntax ](https://github.com/adamcameron/cfscript/blob/master/cfscript.md)
* [See a synxtax cheat sheet](https://rorylaitila.gitbooks.io/lucee/content/script_cheat_sheet.html)

## Quick Overview

### Script
The script based language resembles javascript 

<script src="https://gist.github.com/roryl/5817942eccef2bad2281.js?file=setting_a_variable.cfm"></script>

<noscript>
```
myVar = "test";
```
</noscript>

The trailing ";" denoting the end of the statement can be ommitted as long as new statements are on a new line, but convention is to keep the ";"

Lucee script supports all Tags in script by simply wrapping the code block in brackets

<script src="https://gist.github.com/roryl/5817942eccef2bad2281.js?file=script_tags.cfm"></script>

<noscript>
```
savecontent variable="myContent {
  echo("Output some test");
}
```
</noscript>

View the [script reference](script_reference.html) for all language constructs

### Tags 

The tag based language loosely resembles HTML.

<script src="https://gist.github.com/roryl/5817942eccef2bad2281.js?file=setting_a_variable.cfm"></script>

<noscript>
```
<cfset myVar = "test">
```
</noscript>

Tags can have bodies or not. Tags without bodies do not need a closing bracket, but some people prefer them stylistically 
```
<cfset myVar = "test />
```
Tags with bodies always need a closing tag
```
<cfsavecontent variable="myContent">
  Output some text
</cfsavecontent>
```

