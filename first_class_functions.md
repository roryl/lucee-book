# First Class Functions

All function declarations in Lucee are first class functions, meaning that functions can be passed around as variables to other functions, copy them, delete them, etc. Although this is not often used, this enables complex dynamic runtime behavior. 

Consider the following two Components:

<script src="https://gist.github.com/roryl/468f346631ec9afa3cf9.js?file=component_a.cfc"></script>

<noscript>
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
</noscript>

<script src="https://gist.github.com/roryl/468f346631ec9afa3cf9.js?file=component_b.cfc"></script>

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

Though this is a trivial example and doesn't imply any business case, complex passing of functions around is possible. 

###User Defined Functions vs. Closures
In the example above it passed around what are called User Defined Functions (UDFs) example: "function myName(){}" - When executing UDFs, they have the scopes from *where they are called* This is in comparison to closures, whcih have the scope from *where they were created* This subtle difference is important when passing functions, depending on if you want that passed function to operate on the scopes from where it was created, vs where it is used. 