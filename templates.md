# Templates

Lucee allows creating server side templates which can house HTML and Javascript to be rendered and delivered to the web browser. These templates allow access to all Lucee Built in Functions and Tags. Combining these functions and tags with HTML allow you to build complex interfaces, or other kinds of output like XML, JSON, or PDFs. 

>Note: The file extension of Lucee templates is .cfm

Here is an example of a Lucee Template which outputs the time for a webpage


>Save this code as mytemplate.cfm
```
<cfoutput>
<div>
  #now()#
</div>
</cfoutput>
```

With Lucee templates, you can mingle HTML and Lucee code. In this example above, we output the time using the Lucee function now(). It is wrapped in ## to tell Lucee to evaluate now() instead of sending it to the browser.

