# Types

Lucee supports simple and complex types, type hinting and type coercion

##Simple Types
* String
* Boolean
* Numeric

> Note: You can check if a variable resolves to a simple type with the function isSimpleValue()

###Numeric Type
The numeric type supports Integers and Real Numbers. 

###Pass by Value
The simple types of String, Boolean and Numeric are passed by value, meaning that assigning a variable of a simple type to another variable, duplicates the value.

##Complex Types
* Lists (string lists, like a CSV)
* Array
* Struct
* Component
* Object
* Date
* Query
* XML

###Pass by Reference
The complex types are passed by reference, meaning that when assigning a complex variable to another variable, both variables will contain reference to the same underlying data object. Changing the data will impact both variable references. To create a copy of a value and not pass by reference, use the `duplicate()` function

##Type Coercion
Lucee will  automatically convert Numerics, Strings and Booleans (simple types) in comparison operators and when passing to Typed functions. For example, the following will all be coerced numeric when checked:

```
isNumeric("1"); //returns true
isNumeric(1); //returns true
1 == "1"; //returns true
```

##Type Hinting
Lucee allows annotating functions, arguments and properties with type information which will be checked at runtime. The following types are evaluated as type hints. Because Lucee is dynamically interpreted, Types are not statically enforced by the compiler. Add types to your functions and components to make them self documenting for other programmers and to catch type errors closer to the source of the problem.

You can make use of [CFLint](https://github.com/cflint/CFLint) to statically analyize your code, though this does not check that variables are of the correct Type. 

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
* A interface name: Specifify an interface that a component must implement







