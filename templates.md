##Templates

Lucee allows creating server side templates which can house HTML to be rendered and delivered to the web browser. These templates allow access to all Lucee "Built in Functions" (Lucee's standard function library) and block Tags like query, loop and savecontent. Combining these functions and tags with HTML allow building complex interfaces, or other kinds of output like XML, JSON, or PDFs. 

Lucee implements the ColdFusion Markup Language (CFML) as its default templating language, but supports other popular templating languages like [Handlebars](https://github.com/roryl/handlebars.lucee) as well [Custom Tags](https://rorylaitila.gitbooks.io/lucee/content/custom_tags.html) for creating reusable template elements. 

The examples below utilize CFML templates for basic usage.

>Note: The file extension of the default Lucee templates is .cfm


##Basic Example
Here is an example of a Lucee Template which outputs the time for a webpage:

{% gist id="roryl/708a488afcf4a86f1931",file="basic_template.cfm" %}{% endgist %}

<noscript>
```
<cfoutput>
<div>
  #now()#
</div>
</cfoutput>
```
</noscript>

Lucee templates can combine HTML and Lucee code. In this example above, it outputs the time using the Lucee function now(). It is wrapped in ## to tell Lucee to evaluate now() instead of sending it to the browser.

The `<cfoutput></cfoutput>` tags tell Lucee to look for any variables wrapped in # signs and evaluate them. A common convention is to wrap all content &lt;cfoutput&gt;&lt;/cfoutput&gt; when using CFML templates.

##Conditional Logic
Because Lucee's language control flow is completely available as HTML style tags, it lends itself naturally to HTML output. The example below uses the LOOP, IF, ELSEIF and ELSE tag to change what is displayed.

{% gist id="roryl/708a488afcf4a86f1931",file="conditional_logic.cfm" %}{% endgist %}

<noscript>
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
</noscript>

All Lucee tags, IF, IFELSE, ELSE, SWITCH, TRY, and more are available for use in templates.

##Escaping Output
When Lucee is exeucting code inside cfoutput tags, it is looking for any variables wrapped in #'s. If the template should output an actual # character, then two # together will do so, like ##

{% gist id="roryl/708a488afcf4a86f1931",file="escaping_output.cfm" %}{% endgist %}

<noscript>
```
<cfoutput>
<div>
  ##now()##
</div>
</cfoutput>
```
</noscript>

This template would output:

> &#35;now()#

Notice here that the output *was not* the time. The double ##s were ignored, so Lucee processed now() as text and sent it straight to the browser.

##Including Templates
Sometimes content on a website is repeated on many pages, like the header navigation, and it can be useful to include one template in others so that you are not repeating your efforts. Lucee supports including one template within another using the include tag. 

Here is an example of a three page website, made up of a Home page, an About Us page, and a Services page. There is a template for each page, an a template called navigation.cfm which each page includes.

{% gist id="roryl/708a488afcf4a86f1931",file="home.cfm" %}{% endgist %}


<noscript>
```
<h1>Home</h1>
<cfinclude template="navigation.cfm" />
<p>
Page content about home
</p>
```
</noscript>

{% gist id="roryl/708a488afcf4a86f1931",file="about_us.cfm" %}{% endgist %}

<noscript>
```
<h1>About Us</h1>
<cfinclude template="navigation.cfm" />
<p>
Page content about us
</p>
```
</noscript>

{% gist id="roryl/708a488afcf4a86f1931",file="services.cfm" %}{% endgist %}

<noscript>
```
<h1>Servicess</h1>
<cfinclude template="navigation.cfm" />
<p>
Page content about services
</p>
```
</noscript>

{% gist id="roryl/708a488afcf4a86f1931",file="navigation.cfm" %}{% endgist %}

<noscript>
```
<ul>
  <li>Home</li>
  <li>Services</li>
  <li>About Us</li>
</ul>
```
</noscript>

When each of the websites pages is run, they will all use the common navigation.cfm and be combined to product the result, for example on the homepage:

>####Home
>* Home
>* Services
>* About Us
>
>Page Content about home

>Note: The include tag finds templates via their path from the webroot, or a mapping configured in Application.cfc

##Best Practices
Lucee's entire tag library, including complex functionality like making HTTP requests, sending email, and querying databases, are available as tags. For example, the query tag can select from a database.

{% gist id="roryl/708a488afcf4a86f1931",file="cars_select.cfm" %}{% endgist %}

<noscript>
```
<cfquery name="myQuery">
  SELECT carModel
  FROM myTable
</cfquery>
```
</noscript>

And this tag can be used in a template to output the data:

{% gist id="roryl/708a488afcf4a86f1931",file="cars_output.cfm" %}{% endgist %}

<noscript>
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
</noscript>

However except for one off scripts, it is best to only use conditional or display logic (If,Else,Loop) in templates for outputting HTML, and avoid complex tags. Templates do not have any class structure to help you organize your code, and so complex code written in templates can be hard to organize. Complex code like database access, security and validation is best handled in Components.


