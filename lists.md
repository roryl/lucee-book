# Lists
Lucee has lists which are strings with a delimiter (default is a comma). Lists can only contain strings (and they are a string themselves), so use an Array to contain complex data types. Lists are not real objects in Lucee, and are simply strings that contain a delimiter. As such, any string can be a list that has a delimiter other than a zero length string.

All of the list functions precide with "list" in their name. This is to differentiate from them string functions, because lists are also strings. So `"my,list".len();` returns 7, while `"my,list".listLen()` returns 2

See the available List functions under the [string methods](http://luceedocs.herokuapp.com/objects)

##Create a List
To create a list, create a string with a delimiter. The default delimiter for list functions is a comma, but any delimiter is possible. 

{% gist id="roryl/2433bba8846d72eabda7db04ad4147a0",file="create_list.cfm" %}{% endgist %}

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

##Looping over Lists
If the list is comma separated (which is the default delimiter) it is possible to use a for loop:

{% gist id="roryl/2433bba8846d72eabda7db04ad4147a0",file="for_loop.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
	myList = "one,two,three";
	for(val in myList){
		echo(val & "<br />");
	}
</cfscript>
```
</noscript>

If the list is not comma separated, convert to commas first with the [`listChangeDelims()`](http://luceedocs.herokuapp.com/object/string/listChangeDelims) function:

<noscript>
```
<cfscript>
	myList = "one|two|three";
	for(val in myList.listChangeDelims("," , "|")){
		echo(val & "<br />");
	}
</cfscript>
```
</noscript>

##List to Array
Though it is possible to loop over lists and perform operations on lists, it can sometimes be cleaner code to convert to an array first.

{% gist id="roryl/2433bba8846d72eabda7db04ad4147a0",file="list_to_array.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
	myList = "one,two,three";
	myArray = myList.listToArray();
	for(val in myArray){
		echo(val & "<br />");
	}
</cfscript>
```
</noscript>

