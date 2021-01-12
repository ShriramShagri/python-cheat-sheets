# Dunder or Magic functions

> Find full documentation [here](https://docs.python.org/3/reference/datamodel.html).

## Binary Operators
|   Operator 	|  Method 	|
|---	|---	|
|   + 	|   object.\_\_add__(self, other)	|
|   - 	|   object.\_\_sub__(self, other)	|
|   //	|   object.\_\_floordiv__(self, other)	|
|   /	|   object.\_\_div__(self, other)	|
|   %	|   object.\_\_mod__(self, other)	|
|   **	|   object.\_\_pow__(self, other[, modulo])	|
|   <<	|   object.\_\_lshift__(self, other)	|
|   >>	|   object.\_\_rshift__(self, other)	|
|   &	|   object.\_\_and__(self, other)	|
|   ^	|   object.\_\_xor__(self, other)	|
|   \|	|   object.\_\_or__(self, other)	|

## Assignment Operators:

|   Operator 	|  Method 	|
|---	|---	|
|   += 	|   object.\_\_iadd__(self, other)	|
|   -= 	|   object.\_\_isub__(self, other)	|
|   *= 	|   object.\_\_imul__(self, other)	|
|   /= 	|   object.\_\_idiv__(self, other)	|
|   //= |   object.\_\_ifloordiv__(self, other)	|
|   %= 	|   object.\_\_imod__(self, other)	|
|   **= |   object.\_\_ipow__(self, other[, modulo])	|
|   <<= |   object.\_\_ilshift__(self, other)	|
|   >>= |   object.\_\_irshift__(self, other)	|
|   &= 	|   object.\_\_iand__(self, other)	|
|   ^= 	|   object.\_\_ixor__(self, other)	|
|   \|= 	|   object.\_\_ior__(self, other)	|


## Unary Operators:

|   Operator 	|  Method 	|
|---	|---	|
| -          |       object.\_\_neg__(self)   |
| +          |       object.\_\_pos__(self)   |
| abs()      |       object.\_\_abs__(self)   |
| ~          |       object.\_\_invert__(self)    |
| complex()  |       object.\_\_complex__(self)   |
| int()      |       object.\_\_int__(self)   |
| long()     |       object.\_\_long__(self)  |
| float()    |       object.\_\_float__(self)     |
| oct()      |       object.\_\_oct__(self)   |
| hex()      |       object.\_\_hex__(self)   |

## Comparison Operators

|   Operator 	|  Method 	|
|---	|---	|
|<        |         object._\_lt__(self, other)  |
|<=       |         object._\_le__(self, other)  |
|==       |         object._\_eq__(self, other)  |
|!=       |         object._\_ne__(self, other)  |
|>=       |         object._\_ge__(self, other)  |
|>        |         object._\_gt__(self, other)  |