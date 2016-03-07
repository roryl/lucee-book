# Operators


## Mathematical Operators

| Operator | Title | Description |
| -- | -- | -- |
|+|add| -- 
|-|subtract|--
|/|divide|--
|*|multiply|--
|^|exponentiate|Raises one number to the power of another, e.g. 2 ^ 2 is 4
|%|modulus|Returns the remainder of a number, e.g. 5 % 2 is 1
|MOD|modulus|Returns the remainder of a number, e.g. 5 mod 2 is 1
|\|integer divide|Divides giving an integer result, e.g. 7 \ 2 is 3
|++|increment|Increments a number. Can be used before or after an assignment, e.g. a = b++ would assign the value of b to a, then increment b. a = ++b would increment b, then assign the new value to a. In both cases, b would be incremented.
|--|decrement|Decrements a number. Can be used before or after an assignment, e.g. a = b-- would assign the value of b to a, then decrement b. a = --b would decrement b, then assign the new value to a. In both cases, b would be decremented.
|+=|Compound add|A shorthand operator for adding to a value, e.g. a += b is equivalent to writing a = a + b
|-=|Compound subtract|A shorthand operator for subtracting from a value, e.g. a -= b is equivalent to writing a = a - b
|*=|Compound multiply|A shorthand operator for multiplying a value, e.g. a *= b is equivalent to writing a = a * b
|/=|Compound divide|A shorthand operator for dividing a value, e.g. a /= b is equivalent to writing a = a / b
| 0:2 | 1:2 | 2:2 |

## Logical Operators
| 0:0 | 1:0 | 2:0 |
| -- | -- | -- |
|!|logical inversion|! true is false|
|NOT|logical inversion|not true is false|
|AND|logical and|Returns true if both operands are true, e.g. 1 eq 1 and 2 eq 2 is true|
|&&|logical and|Returns true if both operands are true, e.g. 1 == 1 && 2 == 2 is true|
|OR|logical or|Returns true if either or both operands are true, e.g. 1 eq 1 or 2 eq 3 is true|
|&#124;&#124;|logical or|Returns true if either or both operand are true, e.g. 1 == 1 &#124;&#124; 2 == 3 is true|
|XOR|logical exclusive or|Returns true if either operand is true, but not both, e.g. 1 == 1 XOR 2 == 3 is true, but 1 == 1 XOR 2 == 2 is false|
| 0:2 | 1:2 | 2:2 |

##Comparison Operators
| 0:0 | 1:0 | 2:0 |
| -- | -- | -- |
|EQ|equals|Returns true if operands are equal, e.g. "A" EQ "A" is true|
|==|equals|Returns true if operands are equal, e.g. "A" == "A" is true|
|===|identical|Returns true if operands are equal in value, and are of the same type, e.g. 1 === "1" is false, but 1 === 1 is true|
|NEQ|does not equal|Returns true if operands are not equal, e.g. "A" NEQ "B" is true|
|<>|does not equal|Returns true if operands are not equal, e.g. "A" <> "B" is true|
|!=|does not equal|Returns true if operands are not equal, e.g. "A" != "B" is true|
|!==|is not identical|Returns true if operands are not equal or not of the same type, e.g. 1 !== "1" is true, but 1 !== 1 is false|
|GT|greater than|Returns true if the operand on the left is has a higher value than the operand on the right, e.g. 1 GT 2 is false|
|>|greater than|Returns true if the operand on the left is has a higher value than the operand on the right, e.g. 1 > 2 is false|
|LT|less than|Returns true if the operand on the left has a lower value than the operand on the right, e.g. 1 LT 2 is true|
|<|less than|Returns true if the operand on the left has a lower value than the operand on the right, e.g. 1 < 2 is true|
|GTE|greater than or equal to|Returns true if the operand on the left has a value higher than or equal to the operand on the right, e.g. 2 GTE 2 is true|
|>=|greater than or equal to|Returns true if the operand on the left has a value higher than or equal to the operand on the right, e.g. 2 >= 2 is true|
|LTE|less than or equal to|Returns true if the operand on the left has a value lower than or equal to the operand on the right, e.g. 2 LTE 2 is true|
|<=|less than or equal to|Returns true if the operand on the left has a value lower than or equal to the operand on the right, e.g. 2 <= 2 is true|
|CONTAINS|contains|Returns true if the left operand contains the right operand, e.g. "SMILES" CONTAINS "MILE" is true|
|CT|contains|Returns true if the left operand contains the right operand, e.g. "SMILES" CT "MILE" is true|
|DOES NOT CONTAIN|does not contain|Returns true if the left operand does not contain the right operand, e.g. "SMILES" DOES NOT CONTAIN "RHUBARB" is true|
|NCT|does not contain|Returns true if the left operand does not contain the right operand, e.g. "SMILES" NCT "RHUBARB" is true|
| 0:2 | 1:2 | 2:2 |

##String Operators
| 0:0 | 1:0 | 2:0 |
| -- | -- | -- |
|&|concatenation|Joins two strings, e.g. The result of "Hello" & "World" is "HelloWorld"|
|&=|compound concatenation|A shorthand operator that joins two strings, e.g. a &= b would be equivalent to writing a = a & b|
| 0:2 | 1:2 | 2:2 |





