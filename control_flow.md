# Control Flow

##Decisions

* if
* if/else
* if/elsif/else
* switch

##Branching

* break;
* continue;
* return;

##Looping
* for
* for in loop
* do while
* while do
* Loop
* Looping Labels

---

###if

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="if.cfm" %}{% endgist %}

###if else

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="if_else.cfm" %}{% endgist %}

###if else if else

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="if_elseif_else.cfm" %}{% endgist %}

###switch

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="switch.cfm" %}{% endgist %}

###break
Use the break statement to exit a loop and resume the execution of the parent block. Break can be combined with a label to go to a specific loop.

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="loop_break.cfm" %}{% endgist %}

###continue
Use continue to skip an iteration of a loop and resume at the next iteration

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="loop_continue.cfm" %}{% endgist %}

###return
Functions in Lucee can have multiple return values which can exit a function early for controlling flow.

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="return.cfm" %}{% endgist %}

###for loop

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for_loop.cfm" %}{% endgist %}

###for in loop

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for_in_loop.cfm" %}{% endgist %}

###Do While loop

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="do_while_loop.cfm" %}{% endgist %}

###While Loop
{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="while_loop.cfm" %}{% endgist %}

###Loop Tag
The loop tag is an alternative style which has additional features for [arrays](https://rorylaitila.gitbooks.io/lucee/content/arrays.html), [structs](https://rorylaitila.gitbooks.io/lucee/content/structs.html), [queries](https://rorylaitila.gitbooks.io/lucee/content/queries.html) and lists

See:
* [Looping Arrays](https://rorylaitila.gitbooks.io/lucee/content/arrays.html#looping-arrays)
* [Looping Structs](https://rorylaitila.gitbooks.io/lucee/content/structs.html#looping-structs) TODO
* [Looping Queries](https://rorylaitila.gitbooks.io/lucee/content/queries.html#loop)

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="loop.cfm" %}{% endgist %}

###Looping Labels
It is possible to break out of loops and resume execution at particular lables. This is particularly useful when executing nested loops, and when breaking out of a child loop, wanting to continue execution at a parent.

####For Loop with Label;
{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for_loop_label.cfm" %}{% endgist %}

####Nested For Loops with Labels
{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for_loop_label_nested.cfm" %}{% endgist %}

####Nested Loop tags with Label

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="loop_label.cfm" %}{% endgist %}

