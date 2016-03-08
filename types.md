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

##Type Hinting
Lucee allows annotating functions, arguments and properties with type information which will be checked at runtime. The following types are evaluated as type hints

* any
* array
* binary
* boolean
* component: the value must be a Lucee component.
* date
* guid: the value must be a UUID or GUID of the form xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx where each x is a character that represents a hexadecimal number (0-9A-F).
* numeric
* query
* string
* struct
* uuid: the value must be a UUID of the form xxxxxxxx-xxxx-xxxx-xxxxxxxxxxxxxxxx where each x is a character that represents a hexadecimal number (0-9A-F).
* variableName: a string formatted according to variable naming conventions.
* void-  does not return a value.
* xml: allows web service functions to return XML objects and XML strings.
* A component name: If the type attribute value is not one of the preceding items, Lucee treats it as the name of a Lucee component. When the function executes, it generates an error if the argument that is passed in is not a CFC with the specified name.







