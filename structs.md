# Structs

Structs in Lucee are hashmaps meaning that struct members have a key to reference the member.

The default type of structure created with the notation below is unordered, such that when looping over the keys in the struct, or dumping the struct, they may appear in any order. To mainain the order of keys when adding, the structNew() function must be used.

##Creating Structs

###An Empty Struct
{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_create_empty.cfm" %}{% endgist %}

###With Data
{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_create.cfm" %}{% endgist %}


###With Nested Data

Structs can infinitely next structs and complex data type (arrays can nest structs too)

{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_create_nested.cfm" %}{% endgist %}

##Creating an Ordered Struct

Use the structNew() function to create an ordered struct which maintains the order of the keys when looping, dumping or serializing.

{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_create_ordered.cfm" %}{% endgist %}

##Inserting Items into an Existing Struct

{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_append.cfm" %}{% endgist %}

##Dumping a Struct

{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_dump.cfm" %}{% endgist %}

![](struct_dump.png)

In the preceeding example, all of the keys were uppercased when dumped. While Lucee is case insensitive, it will convert all keys to uppercase when serializing or dumping. To preseve case, make the new names quoted:

{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_dump_quoted.cfm" %}{% endgist %}

![](struct_dump_quoted.png)

##Referencing Struct Keys
{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_referencing.cfm" %}{% endgist %}


##Dynamically Referencing Keys
{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_dynamic.cfm" %}{% endgist %}

##Looping Structs

{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_looping.cfm" %}{% endgist %}


##Advanced Struct Usage

Structs have many functions, see all uses here: http://luceedocs.herokuapp.com/objects
Note: The member functions available on the struct object like .insert() duplicate the older "Built in Function" (BIF) style (like structInsert()). Modern convention is to use the new style, but the old BIFs are still provided for compatibility with older versions of Lucee.