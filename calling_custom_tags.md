#Calling Custom Tags
Before getting into how to build custom tags, its important to first know where Lucee looks for custom tags and how to call them. There are a few lookup rules:

1. Custom Tags in the same directory as the executing script
2. Custom Tags defined in a customtag path
4. Custom Tags loaded at Lucee startup

###Custom Tags in the Same Directory
If the custom tag is in the same directory as the view template executing the tag, Lucee can find the tag with the cf prefix. Consider the following directory structure (which is the structure of the above example).

- /
  - greeting.cfc
  - view.cfm

When executing the view.cfm template, and encountering the `<cf_greeting>` tag, Lucee looked for any matching tags in the same directory as view.cfm.

This basic lookup mechanism is useful when custom tags are only used by one view. But when used by multiple views, not all views would necessarily be in the same directory, so there are additional methods to find the tags.

###Custom Tags defined in a custom tag path
The Application.cfc can direct Lucee where to find custom tags with the setting: `this.customTagPaths`;

Consider this directory structure:

- /
  - /custom_tag
    - view_custom_tag.cfm
    - Application.cfc
  - /custom_tag_import
    - greeting2.cfc

Here was an additional custom tag, "greeting2" which will say "Good Day" instead of "Hello":

{% gist id="roryl/e310ceab4866e75ae923861f5381d8b9",file="greeting2.cfc" %}{% endgist %}

> Note: This is from a different github gist repository because gists do not support subdirectories

If view_custom_tag.cfm is looking for `<cf_greeting2>` custom tag, it wont find it in the same directory as itself and will error with something like this:

![](not_found.png)

So the Application.cfc needs to tell Lucee where to look:

{% gist id="roryl/f7fcd0fc09be6a207adba91b495c55b7",file="Application.cfc" %}{% endgist %}

<noscript>
```
component {
	this.customTagPaths = ["../custom_tag_import"];
}
```
</noscript>

Then when the view is executed, Lucee can find the custom tag and will output:

```
Good Day Jim Smith,

The time is 07:04 AM
```

###Custom Tags loaded at Lucee startup
Any custom tags placed into the Lucee server context, or Web context, custom tag directory. Server context tags will be available to all web contexts, while web context tags will only be available to that specific web context.

The easiest way to find these directories is with the system directory placeholders:

{% gist id="roryl/f7fcd0fc09be6a207adba91b495c55b7",file="system.cfm" %}{% endgist %}

<noscript>
```
<cfscript>
writeDump(expandPath("{lucee-server}/library/tag"));
writeDump(expandPath("{lucee-web}/library/tag"));
</cfscript>
```
</noscript>

Place any custom tags into the library/tag directory of the server or web context, and Lucee can find them.