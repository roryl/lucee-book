# Types

Lucee supports simple and complex types, type hinting and type coercion

##Simple Types
* String
* Boolean
* Numeric

##Complex Types
* Lists (string lists, like a CSV)
* Array
* Struct
* Component
* Object
* Date
* Query

##Type Coercion
Lucee will  automatically convert Numerics, Strings and Booleans (simple types) in comparison operators and when passing to Typed functions. For example, the following will all be coericed numeric when checked:

```
isNumeric("1"); //returns true
isNumeric(1); //returns true
1 == "1"; //returns true
```







