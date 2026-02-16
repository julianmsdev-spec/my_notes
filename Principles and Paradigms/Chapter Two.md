# Basic Python

## Variables
Variables in Python do not have a static type. They are introduced by assigning a value to a name:
```python
x = 4
```

## Basic Data Structures 
Multiple assignment is actually an example of using a *tuple*, which is an immutable compound data type.
```python
a = (3, 4)
# Individual elements of a tuple can be accessed with square brackets
a[0]
a[1]
# Negative indices access a container in reverse, with -1 corresponding to the last element:
a[-1]
a[-2]
# Lists are mutable containers, and they are constructed using square brackets around the values.
b = [5, 6]
# Unlike tuples, list elements can be modified, and new elements can be appended to the end of a list:
b[1] = 7
b.append(8)
```

The dir function can be used to inspect the full interface of the list type:
```python
dir(list)
```
Documentation of a particular method can be retrieved with the help function:
```python
>>> help(list.append)
```
A dict (short for *dictionary*) is an associative container that maps a key to a value. It is created by enclosing key-value pairs within curly braces.
```python
>>> d = { 1 : 2, 'hello' : 'world' }
>>> d[1]
>>> d['hello']
```
Strings are denoted by either single or double quotes. A common convention is to use single quotes unless the string contains a single quote as one of its characters.
```python
>>> 'hello world'
>>> "hello world"
```
Furthermore, A string can span multiple lines if it is enclosed in triple quotes. For example:
```python
>>> x = """
>>> Hello
>>> World!
>>> """
>>> x
'\nHello\nWorld!\n'
```
## Compound Statements 
In python, a sequence of statements, also called a *suite*, consists of one or more statements preceded by the same indentation.

A conditional statement is composed of an if clause, zero, or more elif clauses, and an optional else clause:
```
if <expression>:
	<suite>
elif <expression>:
	<suite>
else:
	<suite>
```
```python
if pow(2, 3) > 5:
	print('greater than')
elif pow(2, 3) == 5:
	print('equal')
else:
	print('less than')
```
While loops have similar syntax:
```
while <expression>:
	<suite>
```
For loops iterate over a sequence, similar to the range-based for loop in C++:
```
for <variable> in <sequence>:
	<suite>
```
```python
>>> for i in [3, 4, 5]:
>>> 	print(i)
```
## Function Definitions
A function is defined with def statement:
```
def <function>(<argument>):
	<suite>
```
```python
def square(x):
	return x * x
```
If a function does not explicitly return a value when it is called, then it returns the special None value:
```python
>>> def print_twice(s):
...     print(s)
...     print(s)
...
>>> x = print_twice(3)
3
3
>>> x
>>> print(x)
None
```
A def statement binds a function object to the given name. Unlike in some other languages, this name can be rebound to something else.
```python
>>> print_twice
<function print_twice at 0x7f53e16935e0>
>>> print_twice = 2
>>> print_twice
2
>>> print_twice(3)
Traceback (most recent call last):
  File "<python-input-21>", line 1, in <module>
    print_twice(3)
    ~~~~~~~~~~~^^^
TypeError: 'int' object is not callable
```
## Class Definitions 
A class is defined with class statement:
```
class <name>(<base classes>):
	<suite>
```
```python
>>> class Cat:
...     def speak(self):
...         print("meow")
...
>>> Cat().speak()
meow
```
The constructor is defined using the special __init__ method. Member variables, more properly called *attributes* in Python, are introduced using the self parameter and dot syntax.
```python
>>> class Square:
...     def __init__(self, side_length):
...         self.side = side_length
...     def perimeter(self):
...         return 4 * self.side
...     def area(self):
...         return self.side * self.side
...
>>> s = Square(3)
>>> s.perimeter()
12
>>> s.area()
9
```
## Modules 
```
import <modules>
```
```python
>>> import operator, math
>>> math.pow(operator.mul(2,3), 2)
```
Individual attributes of a module can also be introduced into the environment using another form of the import statement:
```
from <module> import <attributes>
```
```python
>>> from math import pow
>>> pow(2, 3)
8
```

Another variant imports all names from a module:
```
from <module> import *
```
```python
>>> from operator import *
>>> mul(2, 3)
6
```

It is possible to specify a piece of code that does not run when a module is imported, but runs when a module is executed directly at the command-line in:
```
python3 program.py <arguments>
```
This is accomplished by checking if the __name__ attribute is set to '__main__':
```python
if __name__ == '__main__':
	<suite>
```
## Python Reference Semantics 
A variable in Python is actually an indirect *reference* to an object, rather than holding the object directly in the variable's memory location. Pointer to the same object:
```python
>>> x = []
>>> y = x
>>> y.append(3)
>>> x
[3]
```
copy() function or the deepcopy() function from copy module. Alternatively, many types can be copied by invoking the constructor with an existing object, as in the following:
```python
>>> x = [3]
>>> y = list(x)
>>> y.append(-7)
>>> y
[3, -7]
>>> x
[3]
```