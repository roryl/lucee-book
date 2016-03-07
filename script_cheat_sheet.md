# Script Quick Reference

## If
```
if(condition){
  doSomething();
}
```

## If/else
```
if(condition){
  doSomething();
} else {
  doSomethingElse();
}
```

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
##For Loop
```
for(var i = 1; i <= 5; i=i+1){
  echo('my text');
}
```

##For IN Loop Array
```
for(var i IN myArray){
  //Outputs the value of the array element
  echo(i);
}
```

##For IN loop struct
```
for(var key IN myStruct){
  //Outputs the value of the struct key
  echo(myStruct[key]);
}
```

##Array Loop
Usefull for maintaining a reference to the index and the array element
```
loop index="i" array="#myArray#" item="item" {   
   echo(i) //Outputs the index we are on in the loop
   echo(item) //outputs the value of the array element we are on  
}
```





