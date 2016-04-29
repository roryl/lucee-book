# Nested Custom Tags

In the previous article [Creating Custom Tags](https://rorylaitila.gitbooks.io/lucee/content/creating_custom_tags.html), it used an example of a single tag. Single use tags can be powerful but even moreso, Lucee can nest custom tags which can communicate with eachother and enabled complex behavior.

Consider this view template which generates an article and a Table of Contents for each section:

{% gist id="roryl/f7fcd0fc09be6a207adba91b495c55b7",file="use_article.cfm" %}{% endgist %}

Although there is nothing in the markup that produces a table of contents, when the script executes, a table of contents is produced by the custom tags:

![](article.png)

