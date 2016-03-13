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

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=if.cfm"></script>
```
if(condition){
  doSomething();
}
```

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=if_else.cfm"></script>

## If/else
```
if(condition){
  doSomething();
} else {
  doSomethingElse();
}
```

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=if_elseif_if.cfm"></script>

## If/else if
```
if(condition){
  doSomething();
} else if(condition2) {
  doSomethingElse();
} else {
  doSomethingMore();
}
```

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=for.cfm"></script>

##For Loop
```
for(var i = 1; i <= 5; i=i+1){
  echo('my text');
}
```

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=for_in_array.cfm"></script>

##For IN Loop Array
```
for(var i IN myArray){
  //Outputs the value of the array element
  echo(i);
}
```

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=for_in_struct.cfm"></script>

##For IN loop struct
```
for(var key IN myStruct){
  //Outputs the value of the struct key
  echo(myStruct[key]);
}
```

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=for_in_query.cfm"></script>

#For IN loop Query
```
for(row IN query){
  echo(row.columnName);
}
```
<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=array_loop.cfm"></script>

##Array Loop
Usefull for maintaining a reference to the index and the array element
```
loop index="i" array="#myArray#" item="item" {   
   echo(i) //Outputs the index we are on in the loop
   echo(item) //outputs the value of the array element we are on  
}
```

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=while_loop.cfm"></script>

##While Loop
```
x = 0;
while(x <= 10){
  x = x + 1;
  echo(x);
}
```

##Closure
Implements a closure, which passing this function around keeps a reference to the scopes from where it was created

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=closure.cfm"></script>

```
myClosure = function(){
  //do something
}
```

##User Defined Function
User defined functions can be called from anywhere within the script but when they are passed around they do not contain a reference to where they were created

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=user_defined_function.cfm"></script>

```
function myFunc(){

}
```

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=do_while_loop.cfm"></script>

##Do While Loop
```
x = 0;
do {
  x = x+1;
  echo(x);
} while(x <= 10)
```

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=try_catch_finally.cfm"></script>

##Try Catch Finally
```
 try {
   //Trys code and watches for an exception
 } catch(any e){
   //Runs if an exception was encountered in the try block
 } finally {
   //Runs always whether there was an exception or not
 }
```

##Tags In Script

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=tags_in_script.cfm"></script>

```
tagname arg=1 arg=2 {
  //tag body
}
```

##Single Line Comment

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=single_comment.cfm"></script>

```
//this is a comment
```

##Multi Line Comment

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=multi_comment.cfm"></script>

```
/*

This is a multi line commit

*/

```

##Struct Literal

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=struct_literal.cfm"></script>

```
myStruct = {key:"value", key2:"value2"}
```

##Array Literal

<script src="https://gist.github.com/roryl/11c5a5ab8cf061ab1621.js?file=array_literal.cfm"></script>

```
myArray = ["value1", "value2"];
```




