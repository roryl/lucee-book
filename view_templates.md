# View Templates
Creating HTML views and fragments in Lucee is typically implemented using [Templates](https://rorylaitila.gitbooks.io/lucee/content/templates.html). Although techically, any script (template or Component) can output to the output buffer, convention for developer clarity is that HTML goes into templates only.

This article assumes that you are not using a Framework. If you are using a framework, follow the templating conventions of that framework.

##Classic Lucee Templates

The Classic Lucee Templates section describes how to make HTML output by combining Lucee standard library tags and HTML. This is the "classic" approach, because it is the original method of building templates, but it is by no means antiquated!

##Lucee Template Custom Tags
For complex views or for when building a view library that others may use, Lucee custom tags allow creating custom view tags that can output HTML and perform custom logic. These are similar to Java JSP tags. 

##Lucee Handlebars.js
For those following a logic-less template philosophy, or for building isomorphic javascript apps, the Lucee community has implemented a popular templating language called [Handlebars.js](http://handlebarsjs.com/), and it is called Handlebars.lucee

```
<h1>Comments</h1>

<div id="comments">
  {{#each comments}}
  <h2><a href="/posts/{{../permalink}}#{{id}}">{{title}}</a></h2>
  <div>{{body}}</div>
  {{/each}}
</div>
```