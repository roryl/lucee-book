# Style Guide

While each project and developer will settle on their own conventions, these are the common coding styles used in the Lucee commnuity.

##camelCase functions and components

Use camelCase for function names, whether built in, component functions or user defind functions

```
var file = fileNew();
```

A common convention is to upercase the first work of Components, but lower case any other variables

```
var MyObj = new MyObj();
var myArray = [];
```

##Tags lowercase

When using tags in templates like `<cfset>`, keep them lowercase

##Quote Attributes
Tags in Lucee can take strings or variables, for exmaple

`loop array=myArray index="i" {}` or `loop array="#myArray#" index="i" {}`

The common convention is to always quote attributes so that there is visual consistency in the attributes like in the second example above.



