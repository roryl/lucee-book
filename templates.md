#Templates

Lucee allows creating server side templates which can house HTML to be rendered and delivered to the web browser. These templates allow access to all Lucee "Built in Functions" (Lucee's standard function library) and block Tags like query, loop and savecontent. Combining these functions and tags with HTML allow you to build complex interfaces, or other kinds of output like XML, JSON, or PDFs. 

>Note: The file extension of Lucee templates is .cfm

##Basic Example
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


##Conditional Logic
Because Lucee's language control flow is completely available as HTML style tags, it lends itself naturally to HTML output. The example below uses the LOOP, IF, ELSEIF and ELSE tag to change what is displayed.

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

All Lucee tags, IF, IFELSE, ELSE, SWITCH, TRY, and more are available for use in templates.

##Escaping Output
When Lucee is exeucting code inside cfoutput tags, it is looking for any variables wrapped in #'s. If the template should output an actual # character, then two # together will do so, like ##

```
<cfoutput>
<div>
  ##now()##
</div>
</cfoutput>
```

This template would output:

> &#35;now()#

Notice here that the output *was not* the time. The double ##s were ignored, so Lucee processed now() as text and sent it straight to the browser.

##Including Templates
Sometimes content on a website is repeated on many pages, like the header navigation, and it can be useful to include one template in others so that you are not repeating your efforts. Lucee supports including one template within another using the include tag. 

Here is an example of a three page website, made up of a Home page, an About Us page, and a Services page. There is a template for each page, an a template called navigation.cfm which each page includes. 

>home.cfm


```
<h1>Home</h1>
<cfinclude template="navigation.cfm" />
<p>
Page content about home
</p>
```

>about_us.cfm


```
<h1>About Us</h1>
<cfinclude template="navigation.cfm" />
<p>
Page content about us
</p>
```

>services.cfm


```
<h1>Servicess</h1>
<cfinclude template="navigation.cfm" />
<p>
Page content about services
</p>
```



>navigation.cfm

```
<ul>
  <li>Home</li>
  <li>Services</li>
  <li>About Us</li>
</ul>
```

When each of the websites pages is run, they will all use the common navigation.cfm and be combined to product the result, for example on the homepage:

>####Home
>* Home
>* Services
>* About Us
>
>Page Content about home

##Best Practices
Lucee's entire tag library, including complex functionality like making HTTP requests, sending email, and querying databases, are available as tags. For example, the query tag can select from a database

```
<cfquery name="myQuery">
  SELECT *
  FROM myTable
</cfquery>
```

And this tag can be used in a template to output the data:

>query_test.cfm

```
<cfquery name="myQuery">
  SELECT carModel
  FROM cars
</cfquery>
<cfoutput>
<cfloop query="#myQuery#">
  #carModel#
</cfloop>
<cfoutput>
```

However except for one off scripts, it is best to only use conditional or display logic (IF,Else,LOOP) in templates for outputting HTML, and avoid complex tags. Templates do not have any class structure to help you organize your code, and so complex code written in templates can be hard to organize. Complex code like database access, security and validation is best handled in Components.


