# Mixins
Mixins are a programming feature which allow for dynamically adding methods to components during instantiation. Lucee support both type checked mixins confirming to an interface, and unchecked dynamic mixins.

Mixins are used when a component has "cross cutting" functionality that is shared with other components, and which this functionality should be exposed as functionality of the component itself. This allows for code reuse by only writing the functionality in one place, and then including it in other places.

In terms of code-reuse, this allows for more flexibility than inheritance because multiple sets of functionality can be 'mixed in', and it is less boilerplate than creating ['Decorator' classes](https://en.wikipedia.org/wiki/Decorator_pattern) which simply wrap other function calls.

##Dynamic Mixins
There are two methods of acheiving mixins with Lucee:
1. Including Functions
2. Lifting, or copying functions between components

###Including Functions

Consider this basic component without any mixins:

{% gist id="SamyPesse/6ceb8cb8d531ffab75f0",file="README.md" %}{% endgist %}

<noscript>
```
component {
  
  function init(){
    //Do something on instantiation 
    return this;
  }  

}
```
</noscript>


##Type Checked
