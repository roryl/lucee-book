# Creating Custom Tags

Lucee custom tags are created with Components that follow a particular convention. The Compoenent can contain any code, but as long as it contains the functions Lucee is looking for as a custom tag, it can be used as a custom tag.

The special conventions that make a component a custom tag are:

* Handling the start tag
* Handling Attributes
* Handling the end tag
* Handling output

When describing a custom tag, these conventions above map to areas in the code when using a custom tag. Consider this custom tag below:

```
<cf_myCustomTag attribute1="foo" attribute2="bar">

</cf_myCustomTag>
```

The important execution areas to be aware of are as follows:

![](tag_map.fw.png)

Handling all of these execution areas is done in a single Component.

##Handling the Start Tag
When executing a custom tag, Lucee looks for a function in the component called onStartTag().

Here is an example of a minimal custom tag:

{% gist id="roryl/e310ceab4866e75ae923861f5381d8b9",file="basicTag.cfc" %}{% endgist %}

To execute this tag, use:

{% gist id="roryl/e310ceab4866e75ae923861f5381d8b9",file="use_basic.cfm" %}{% endgist %}
