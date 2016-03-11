# Templates

Lucee allows creating server side templates which can house HTML to be rendered and delivered to the web browser. These templates allow access to all Lucee "Built in Functions" (Lucee's standard function library) and block Tags like query, loop and savecontent. Combining these functions and tags with HTML allow you to build complex interfaces, or other kinds of output like XML, JSON, or PDFs. 

>Note: The file extension of Lucee templates is .cfm

Here is an example of a Lucee Template which outputs the time for a webpage:


>Save this code as mytemplate.cfm
```
<cfoutput>
<div>
  #now()#
</div>
</cfoutput>
```

Lucee templates can combine HTML and Lucee code. In this example above, it outputs the time using the Lucee function now(). It is wrapped in ## to tell Lucee to evaluate now() instead of sending it to the browser.

The &lt;cfoutput&gt;&lt;/cfoutput&gt; tags tell Lucee to look for any variables wrapped in # signs and evaluate them. A common convention is to wrap all content &lt;cfoutput&gt;&lt;/cfoutput&gt; 

Because Lucee's language control flow is completely available as HTML style tags, it lends itself naturally to HTML output. The example below uses the IF and ELSE tag to change what is displayed.

```
<cfset pets = ["dogs","cats","pigs"]>
<cfoutput>
<h1>Sounds a Pet Makes</h1>
<cfloop array="#pets#" item="#beedName#">
  <cfif breedName IS "dogs">
    Woof!
  </elseif breedNAme IS "cats">
    meow!
  </cfelse>
    Thats an odd pet
  </cfif>  
</cfloop>
</cfoutput>
```

