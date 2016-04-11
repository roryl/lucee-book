# Script Quick Reference

###Table of Contents
- [If](#if)
- [If/Else](#ifelse)
- [If/Else if](#ifelse-if)
- [For Loop](#forloop)
- [For IN Loop Array](#for-in-loop-array)
- [For IN loop Struct](#for-in-loop-struct)
- [For In Loop Query](#for-in-loop-query)
- [Array Loop](#array-loop)
- [While Loop](#while-loop)
- [Closure](#closure)
- [User Defined Function](#user-defined-function)
- [Do While Loop](#do-while-loop)
- [Try Catch Throw Finally](#try-catch-throw-finally)
- [Tags in Script](#tags-in-script)
- [Single Line Comment](#single-line-comment)
- [Multi Line Comment](#multi-line-comment)
- [Struct Literal](#struct-literal)
- [Array Literal](#array-literal)

## If

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="if.cfm" %}{% endgist %}


## If/else

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="if_else.cfm" %}{% endgist %}



## If/else if/else

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="if_elseif_else.cfm" %}{% endgist %}



##For Loop

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for.cfm" %}{% endgist %}



##For IN Loop Array

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for_in_array.cfm" %}{% endgist %}




##For IN loop struct

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for_in_struct.cfm" %}{% endgist %}




#For IN loop Query

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for_in_query.cfm" %}{% endgist %}

#For IN loop List
The for in construct works with any [List](https://rorylaitila.gitbooks.io/lucee/content/lists.html) that is comma delimited. To change a list to comma delimited, use the ['listChangeDelims()'](http://luceedocs.herokuapp.com/object/string/listChangeDelims) function.

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for_in_list.cfm" %}{% endgist %}


##Array Loop
Usefull for maintaining a reference to the index and the array element

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="array_loop.cfm" %}{% endgist %}



##While Loop
{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="while_loop.cfm" %}{% endgist %}


##Closure
Implements a closure, which passing this function around keeps a reference to the scopes from where it was created

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="closure.cfm" %}{% endgist %}


##User Defined Function
User defined functions can be called from anywhere within the script but when they are passed around they do not contain a reference to where they were created

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="user_defined_function.cfm" %}{% endgist %}




##Do While Loop
{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="do_while_loop.cfm" %}{% endgist %}




##Try Catch Finally

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="try_catch_finally.cfm" %}{% endgist %}


##Tags In Script

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="tags_in_script.cfm" %}{% endgist %}


##Single Line Comment

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="single_comment.cfm" %}{% endgist %}


##Multi Line Comment

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="multi_comment.cfm" %}{% endgist %}


##Struct Literal

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="struct_literal.cfm" %}{% endgist %}


##Array Literal

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="array_literal.cfm" %}{% endgist %}





