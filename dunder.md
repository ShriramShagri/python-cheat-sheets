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
|<        |         object.\_\_lt__(self, other)  |
|<=       |         object.\_\_le__(self, other)  |
|==       |         object.\_\_eq__(self, other)  |
|!=       |         object.\_\_ne__(self, other)  |
|>=       |         object.\_\_ge__(self, other)  |
|>        |         object.\_\_gt__(self, other)  |

## \_\_eq__ :

The `a == b` expression invokes `A.\_\_eq__`, since it exists. Its code includes `self.value == other`. Since int's don't know how to compare themselves to B's, Python tries invoking `B.\_\_eq__` to see if it knows how to compare itself to an int.

```python
class A(object):
    def __eq__(self, other):
        print("A __eq__ called: %r == %r ?" % (self, other))
        return self.value == other
class B(object):
    def __eq__(self, other):
        print("B __eq__ called: %r == %r ?" % (self, other))
        return self.value == other

a = A()
a.value = 3
b = B()
b.value = 4
a == b
```

Output:

```
A __eq__ called: <__main__.A object at 0x013BA070> == <__main__.B object at 0x013BA090> ?
B __eq__ called: <__main__.B object at 0x013BA090> == 3 ?
```


## \_\_enter__ and \_\_exit__ :

Using these magic methods (`__enter__`, `__exit__`) allows you to implement objects which can be used easily with the `with` statement.

The idea is that it makes it easy to build code which needs some 'cleandown' code executed (think of it as a try-finally block). 

A useful example could be a database connection object (which then automagically closes the connection once the corresponding 'with'-statement goes out of scope):

```python
class DatabaseConnection(object):

    def __enter__(self):
        # make a database connection and return it
        ...
        return self.dbconn

    def __exit__(self, exc_type, exc_val, exc_tb):
        # make sure the dbconnection gets closed
        self.dbconn.close()
        ...
```

As explained above, use this object with the `with` statement (you may need to do `from __future__ import with_statement` at the top of the file if you're on Python 2.5).

```python
with DatabaseConnection() as mydbconn:
    # do stuff
```

# \_\_setstate__ and \_\_getstate__ :

Whatever comes out of `getstate`, goes into `setstate`. It does not need to be a dict.

Whatever comes out of `getstate` must be pickeable, e.g. made up of basic built-ins like `int`, `str`, `list`.

Find more on pickle [here](https://docs.python.org/3/library/pickle.html#pickle-protocol)

```python
class C(object):
    def __init__(self, i):
        self.i = i
    def __getstate__(self):
        return self.i
    def __setstate__(self, i):
        self.i = i
assert pickle.loads(pickle.dumps(C(1), -1)).i == 1
```

Default `__setstate__`

The default `__setstate__` takes a dict.

`self.__dict__` is a good choice, but we can construct one ourselves to better see what is going on:

```python
class C(object):
    def __init__(self, i):
        self.i = i
    def __getstate__(self):
        return {'i': self.i}
assert pickle.loads(pickle.dumps(C(1), -1)).i == 1
```

Default `__getstate__`

Analogous to `__setstate__`.

```python
class C(object):
    def __init__(self, i):
        self.i = i
    def __setstate__(self, d):
        self.i = d['i']
assert pickle.loads(pickle.dumps(C(1), -1)).i == 1
```
Original answers

* [\_\_getstate__ and \_\_setstate__](https://stackoverflow.com/questions/1939058/simple-example-of-use-of-setstate-and-getstate)
* [\_\_enter__ and \_\_exit__](https://stackoverflow.com/questions/1984325/explaining-pythons-enter-and-exit)
* [\_\_eq__](https://stackoverflow.com/questions/3588776/how-is-eq-handled-in-python-and-in-what-order)