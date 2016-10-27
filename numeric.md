# Numeric (DRFAT)
Lucee has a built in number type called Numeric. This type supports numbers with up to 16 digits of precision. Lucee will use [type coercion](https://rorylaitila.gitbooks.io/lucee/content/types.html#type-coercion) and automatically convert numeric types to string and visa versa, depending on use.  

##Creating a Number
Creating a number in Lucee is accomplished by setting a number to a variable:

{% gist id="roryl/6edb0b617f29447556e515e4b7597281",file="numeric.cfm" %}{% endgist %}



##Working with Big Integers


http://www.barneyb.com/barneyblog/2009/07/15/beware-coldfusion-floating-point-integers/