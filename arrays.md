# Arrays Examples

Lucee Array indexes start at 1

##Creating Arrays

Arrays can be created with elements or empty and elements added later.

###Create an Array with some elements
{% gist id="https://gist.github.com/roryl/cc95907c4837ca032b45",file="create_array.cfm" %}{% endgist %}

###Create an Empty Array

{% gist id="https://gist.github.com/roryl/cc95907c4837ca032b45",file="empty_array.cfm" %}{% endgist %}

###Appending Elements to an Array

{% gist id="https://gist.github.com/roryl/cc95907c4837ca032b45",file="array_append.cfm" %}{% endgist %}


##Referencing Arrays

{% gist id="https://gist.github.com/roryl/cc95907c4837ca032b45",file="referencing_arrays.cfm" %}{% endgist %}

##Looping Arrays

###For Loop

{% gist id="https://gist.github.com/roryl/cc95907c4837ca032b45",file="array_for_loop.cfm" %}{% endgist %}

###For In Loop

{% gist id="https://gist.github.com/roryl/cc95907c4837ca032b45",file="array_for_in_loop.cfm" %}{% endgist %}

###Loop Tag

{% gist id="https://gist.github.com/roryl/cc95907c4837ca032b45",file="array_loop_tag.cfm" %}{% endgist %}

###Loop Tag with with Index

{% gist id="https://gist.github.com/roryl/cc95907c4837ca032b45",file="array_loop_tag_index.cfm" %}{% endgist %}

###Each

{% gist id="https://gist.github.com/roryl/cc95907c4837ca032b45",file="array_each.cfm" %}{% endgist %}

##Advanced Array Usage

Arrays have many functions, see all uses here: http://luceedocs.herokuapp.com/objects

>Note: The member functions available on the Array object like .sort() duplicate the older "Built in Function" (BIF) style (like arraySort()). Modern convention is to use the new style, but the old BIFs are still provided for compatibility with older version of Lucee.

