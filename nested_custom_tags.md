# Nested Custom Tags

In the previous article [Creating Custom Tags](https://rorylaitila.gitbooks.io/lucee/content/creating_custom_tags.html), it used an example of a single tag. Single use tags can be powerful but even moreso, Lucee can nest custom tags which can communicate with eachother and enabled complex behavior.

Consider this view template which generates an article and a Table of Contents for each section. It has a `<cf_article>` tag which contains multiple `<cf_section>` tags. And these two tags will worth together to produce the output.

{% gist id="roryl/f7fcd0fc09be6a207adba91b495c55b7",file="use_article.cfm" %}{% endgist %}

Although there is nothing in the markup that produces a table of contents, when the script executes, a table of contents is produced by the custom tags:

![](article.png)

What makes nested custom tags powerful is it can enable writing complex view code which can take a few tags and options, but generate complex output.

##How Nested Tags Work
Because custom tags are simply .CFC components, they can do anything a Component can do. But in order for a nested tag to be aware of its parent, Lucee tells nested tags who their parents are.

Lets start with the implementation of the nested tag `<cf_section>`: 

{% gist id="roryl/f7fcd0fc09be6a207adba91b495c55b7",file="section.cfc" %}{% endgist %}

The new feature of this section tag that was not used in any previous examples is the `init()` function. Focus on just the function signature to start:

```
public void function init(component parent, required boolean hasEndTag){
    //ommitted 
}
```

When Lucee encounters a custom tag and instantiates it, it will pass two parameters to the init() function, first is a reference to the parent cfc, and second a true/false for `hasEndTag`. Notice that hasEndTag is required, but parent is not. This means that a parent is not always present. If a custom tag does not have any parent tags (which the `<cf_article>` in the example does not) then this value will be null.

Looking at the full implementation: 

```
public void function init(component parent, required boolean hasEndTag){
    if(!isNull(parent)){
        parent.addChild(this);
    } else {
        throw("Cannot have sections without a parent <cf_article>");
    }
}
```

We see that it does two things: First, it checks if the parent exists, and then calls `parent.addChild(this)` (more on this later), or else it throws an error that sections must have a parent article.

Moving on to the <cf_section> onEndTag() function, it is implemented: 

```
public boolean function onEndTag(required struct attributes, required struct caller, string generatedContent){
      param name="attributes.title";
      variables.title = attributes.title;
      variables.body = generatedContent;
      return false;
  }
```

Instead of outputting the tag content or title, instead it is setting the content into the variables scope. This is for later use by the `<cf_article>` parent. Also see that <cf_section> implements two getter methods for variables.title and variables.body:

```
public function getTitle(){
    return variables.title;
}

public function getBody(){
    return variables.body;
}
```

The purpose of these getter methods is so that <cf_article> can get to the data of <cf_section>. Now that we have the implementation of <cf_section>, lets see the implementation of <cf_article>:

{% gist id="roryl/f7fcd0fc09be6a207adba91b495c55b7",file="article.cfc" %}{% endgist %}




