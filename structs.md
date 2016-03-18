# Structs

Structs in Lucee are containers for data where there is a 'key' that references a 'value'. When dumping a struct it looks like:

![](struct_dump.png)

The default type of structure created with the notation below is unordered, such that when looping over the keys in the struct, or dumping the struct, the data may appear in any order. To mainain the order of keys when adding, the structNew() function must be used.

##Creating Structs

###An Empty Struct
{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_create_empty.cfm" %}{% endgist %}

When dumped an empty struct has no data:

![](struct_empty.png)

###With Data
{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_create.cfm" %}{% endgist %}


Struct Dump:

![](struct_dump.png)

###With Nested Data

Structs can infinitely next structs and complex data type (arrays can nest structs too)

{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_create_nested.cfm" %}{% endgist %}

Nested Struct Dump:

![](struct_nested.png)

##Creating an Ordered Struct

Use the structNew() function to create an ordered struct which maintains the order of the keys when looping, dumping or serializing.

{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_create_ordered.cfm" %}{% endgist %}

Dump of an Ordered Struct:

![](sturct_ordered.png)

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

###For in Loop
{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_looping.cfm" %}{% endgist %}

###Each Loop
{% gist id="https://gist.github.com/roryl/19296468d648117f1fb2",file="struct_each.cfm" %}{% endgist %}


##Advanced Struct Usage

Structs have many functions, see all uses here: http://luceedocs.herokuapp.com/objects

>Note: The member functions available on the struct object like .insert() duplicate the older "Built in Function" (BIF) style (like structInsert()). Modern convention is to use the new style, but the old BIFs are still provided for compatibility with older versions of Lucee.