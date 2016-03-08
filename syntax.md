# Syntax

There are two flavors to the Lucee Language, Tags and Script. The entire language is available in Tags or Script. Tags should be (almost always) only used for HTML templates.

For a detailed review of script syntax see [](https://github.com/adamcameron/cfscript/blob/master/cfscript.md)

For a cheat sheet see [](https://rorylaitila.gitbooks.io/lucee/content/script_cheat_sheet.html)

## Quick Overview

### Script
The script based language loosely resembles javascript 
```
myVar = "test";
```
The trailing ";" denoting the end of the statement can be ommitted as long as new statements are on a new line, but convention is to keep the ";"

Lucee script supports all Tags in script by simply wrapping the code block in handlebar brackets

```
savecontent variable="myContent {
  echo("Output some test");
}
```

There is also an alternative style which looks more like a block function
```
savecontent(variable="myContent){
  echo("Output some test");
}
```
View the [script reference](script_reference.html) for all language constructs

### Tags 

The tag based language loosely resembles HTML.
```
<cfset myVar = "test>
```
Tags can have bodies or not. Tags without bodies do not need a closing bracket, but some people prefer them stylistically 
```
<cfset myVar = "test />
```
Tags with bodies always need a closing bracket
```
<cfsavecontent variable="myContent">
  Output some text
</cfsavecontent>
```

