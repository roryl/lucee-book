# Types

Lucee supports simple and complex types, type hinting and type coercion

##Basic Types
String
Boolean
Numeric
Lists (string lists, like a CSV)
Array
Struct
Component
Object
DateTime


##Type Coercion
Lucee will  automatically convert Numerics, Strings and Booleans in comparison operators and when passing to Typed functions. For example, the following will all be coericed numeric when checked:

isNumeric("1"); //returns true
isNumeric(1); //returns true
1 == "1"; //returns true







