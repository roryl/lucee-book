# Numeric (DRFAT)
Lucee has a built in number type called Numeric. This type supports numbers with up to 16 digits of precision. Lucee will use [type coercion](https://rorylaitila.gitbooks.io/lucee/content/types.html#type-coercion) and automatically convert numeric types to string and visa versa, depending on use.  

##Creating a Number
Creating a number in Lucee is accomplished by setting a number to a variable:

{% gist id="roryl/6edb0b617f29447556e515e4b7597281",file="numeric.cfm" %}{% endgist %}

When dumping the variable, it will be of the numeric type:

![](numeric_dump.png)

##Using a Number
Any variable which is numeric can be used with [mathematical operators](https://gist.github.com/roryl/6edb0b617f29447556e515e4b7597281) (addition, subtraction, etc). 

{% gist id="roryl/6edb0b617f29447556e515e4b7597281",file="operators.cfm" %}{% endgist %}

![](operators_dump.cfm.png)

##Numeric Type Coercion
Lucee will also automatically convert strings to numbers when they are used in mathematical operations. In this example, a Lucee string is created by enclosing the number in quotes:

{% gist id="roryl/6edb0b617f29447556e515e4b7597281",file="numeric_string.cfm" %}{% endgist %}

In the dump of the variable it is a string type and not a numeric type:

![](numeric_string.png)

However, if this string is used in mathematical operations, Lucee will try to convert it to a numeric and will return a numeric type after the operation:

{% gist id="roryl/6edb0b617f29447556e515e4b7597281",file="operate_string.cfm" %}{% endgist %}

![](operate_string.png)

If Lucee cannot convert a string to a valid number, it will throw an error like `can't cast string to a number value` as in this example:

{% gist id="roryl/6edb0b617f29447556e515e4b7597281",file="operate_string_error.cfm" %}{% endgist %}

![](operate_string_error.png)

##Working with Big Integers
Numbers in Lucee are a floating point number with 16 digits of precision (Lucee uses the java.lang.Double type). For most use cases, this is a sufficiently performant way for Lucee to store numbers. However for really big numbers (greater than 16 digits), this will cause Lucee to round the number to the nearest place.

http://www.barneyb.com/barneyblog/2009/07/15/beware-coldfusion-floating-point-integers/