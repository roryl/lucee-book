# First Class Functions

All function declarations in Lucee are first class functions, meaning that you can pass functions around as variables to other functions, copy them, delete them, etc. Although this is not often used, this enables complex dynamic runtime behavior. 

Consider the following two Components:

a.cfc
```
component { 
  
  public function init(){
    return this;
  }
  
  public function otherFunc(){
    echo("called!");
  }

}
```

b.cfc
```
component { 
  
  public function init(){
    var a = new a(); //instantiate a
    
    this.otherFunc = a.otherFunc; //Copy otherFunc from a to b
    
    this.otherFunc(); //Outputs "called!"
    
    call(this.otherFunc);
    
    return this;
  }
  
  private function call(required function func){
    arguments.func(); //executes otherFunc, outputs "called!"
  } 

}
```

Though this is a trivial example and doesn't imply any business case, you can see that passing functions around is possible. 

###Named Functions vs. Closures
In the example above we passed around what are called named functions example: "function myName(){}" - When executing named functions, they have the scopes from *where they are called* This is in comparison to closures, whcih have the scope from *where they were created* This subtle difference is important when passing functions, depending on if you want that passed function to operate on the scopes from where it was created, vs where it is used. 