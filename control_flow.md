# Control Flow

##Decisions

* [if](#if)
* [if/else](#if-else)
* [if/elsif/else](#if-else-if-else)
* [switch](#switch)

##Branching

* [break;](#break)
* [continue;](#continue)
* [return;](#return)

##Looping
* [for loop](#for-loop)
* [for in loop](#for-in-loop)
* [do while loop](#do-while-loop)
* [while loop](#while-loop)
* [Loop Tag](#loop-tag)
* [Looping with Labels](#looping-labels)

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

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for.cfm" %}{% endgist %}

###for in loop
The for in construct can be used with for [arrays](https://rorylaitila.gitbooks.io/lucee/content/arrays.html), [structs](https://rorylaitila.gitbooks.io/lucee/content/structs.html), and [queries](https://rorylaitila.gitbooks.io/lucee/content/queries.html). Below is an example for arrays. For other examples, see:

* [Looping Arrays](https://rorylaitila.gitbooks.io/lucee/content/arrays.html#looping-arrays)
* [Looping Structs](https://rorylaitila.gitbooks.io/lucee/content/structs.html#looping-structs) TODO
* [Looping Queries](https://rorylaitila.gitbooks.io/lucee/content/queries.html#loop)

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for_in_array.cfm" %}{% endgist %}

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

###Looping with Labels
It is possible to `break;` out of loop and `continue;` loops and resume execution at particular lables. This is particularly useful when executing nested loops, and when breaking out of a child loop, wanting to continue execution at a parent, or after a parent.

####For Loop with Label;
{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for_loop_label.cfm" %}{% endgist %}

####Nested For Loops with Labels
This exits out of the child loop and continues after the parent loop
{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for_loop_label_nested.cfm" %}{% endgist %}

####Nested Loop tags with Label
Labels are also possible with loop tags using the label attribute
{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="loop_label.cfm" %}{% endgist %}

####Nested Loop using Continue
While the previous examples used `break;` to exit the loop and resume after the label, its also possible to use continue, which results the next iteration of the loop, at the label:

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for_loop_label_nested_continue.cfm" %}{% endgist %}

The above sample would produce: 

inner loop with 1 <br>
inner loop with 2 <br>
Top of loop with 2 <br>
inner loop with 1<br>
inner loop with 2<br>
Top of loop with 3<br>
inner loop with 1<br>
inner loop with 2<br>
Top of loop with 4<br>
inner loop with 1<br>
inner loop with 2<br>
Top of loop with 5<br>
inner loop with 1<br>
inner loop with 2<br>
After loop<br>

The sample example but with a break

{% gist id="https://gist.github.com/roryl/11c5a5ab8cf061ab1621",file="for_loop_label_nested_break.cfm" %}{% endgist %}

, produces:

Top of loop with 1<br>
inner loop with 1<br>
inner loop with 2<br>
After loop<br>
