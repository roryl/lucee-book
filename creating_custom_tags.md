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
When executing a custom tag, Lucee looks for a function in the component called onStartTag() and it calls it.

Here is an example of a minimal custom tag:

{% gist id="roryl/f7fcd0fc09be6a207adba91b495c55b7",file="basicTag.cfc" %}{% endgist %}

To execute this tag, use:

{% gist id="roryl/f7fcd0fc09be6a207adba91b495c55b7",file="use_basic.cfm" %}{% endgist %}

It will output: `Hello there!`

###onStartTag arguments
Then Lucee calls the onStartTag, it provides the arguments specified in the example above. Your onStartTag should handle all of these arguments.

####Attributes
Lucee will pass to onStartTag, a struct containing all of the attributes in the start tag area. The onStartTag() function can use these attributes to perform actions, looking data or do anything the custom tag should be allowed to do. 

####Caller
Lucee will pass a *reference* to the variables scope of the .cfm template which is calling the custom tag. This allows the custom tag to inject data into the script which is using the custom tag, that the script may use. 

###onStartTag return value (boolean)
onStartTag() should return a true or false, which controls if the body of the tag should be executed. This is useful for tags which do not have bodies `<cf_nobody>`, or for when the custom tag needs to skip the body based on the values of the attributes or some other need.

##Handling the End Tag
Lucee handles the end tag by calling the function onEndTag() in the Component. Lucee does this for normal full closing tags, and self closing tags. 

>#### A note about Self Closing Tags
A self closing tag is when the custom tag does not have a tag body, but has a closing slash (/) for example: `<cf_basicTag />`. In a self closing tag, Lucee will call onEndTag() just as if the tag had a body like `<cf_basicTag>body</cf_basicTag>`. If the tag does not close like <cf_basicTag> then Lucee will not call onEndTag()


Consider this example of a custom tag we created to output the invite to a party:

{% gist id="roryl/f7fcd0fc09be6a207adba91b495c55b7",file="use_invite.cfm" %}{% endgist %}

What this tag is going to do is take an invitee supplied as an attribute, create a salutation for them and then output the paragraph for the invitation. The example would output: 

```
Hello Jimmy,

I'd like to let you know that you are invited to our party!
```

To implement this custom tag, we used the following:

{% gist id="roryl/f7fcd0fc09be6a207adba91b495c55b7",file="invite.cfc" %}{% endgist %}

###onEndTag Arguments
The arguments passed to the onEndTag allow for controlling what happens to the content between the start and end tags

####Attributes
Just like the onStartTag, the onEndTag gets the attributes from the start tag. This is often used to control or change the content of the text between the tags.

####Caller
Just like the onStartTag, the onEndTag also gets a reference to the variables scope of the calling template. 

####GeneratedContent

