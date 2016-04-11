# Lists
Lucee has lists which are strings with a delimiter (default is a comma). Lists can only contain strings (and they are a string themselves), so use an Array to contain complex data types. Lists are not real objects in Lucee, and are simply strings that contain a delimiter. Any string can be a list that has a delimiter other than a zero length string.

##Create a List
To create a list, create a string with a delimiter. The default delimiter for list functions is a comma, but any delimiter is possible. 



<noscript>
```
<cfscript>
	myList = "one,two,three"; //Create a comma separated list
	echo(myList.listLen() & "<br />"); //echo the length, should be 3
	myOtherList = "one|two|three"; //Create a pipe separated list
	echo(myOtherList.listLen("|") & "<br />"); //Echo the length, should be three. Pass the delimiter because we are overriding the default which was a comma
	echo(myList.listLen("t")); //Any character can be a delimiter
</cfscript>
```
</noscript>

