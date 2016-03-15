# Structs

Structs in Lucee are hashmaps meaning that struct members have a key to reference the member objects.

##Creating Structs

###An Empty Struct
{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_create_empty.cfm" %}{% endgist %}

###With Data
{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_create.cfm" %}{% endgist %}


###With Nested Data

Structs can infinitely next structs and complex data type (arrays can nest structs too)

{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_create_nested.cfm" %}{% endgist %}

##Inserting Items into an Existing Struct

{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_append.cfm" %}{% endgist %}

##Dumping a Struct

{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_dump.cfm" %}{% endgist %}

![](struct_dump.png)

In the preceeding example, all of the keys were uppercased when dumped. While Lucee is case insensitive, it will convert all keys to uppercase when serializing or dumping. To preseve case, make the new names quoted:

{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_dump_quoted.cfm" %}{% endgist %}

![](struct_dump_quoted.png)



