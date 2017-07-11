## Index
1. [Basics](https://github.com/obitech/python_cheatsheet#1-basics--)
2. [Strings](https://github.com/obitech/python_cheatsheet#2-strings--)
3. [Lists](https://github.com/obitech/python_cheatsheet#3-lists--)
4. [Control flow](https://github.com/obitech/python_cheatsheet#4-control-flow--)
5. [Functions](https://github.com/obitech/python_cheatsheet#5-functions--)
6. [Tuples](https://github.com/obitech/python_cheatsheet#6-tuples--)
7. [Sets](https://github.com/obitech/python_cheatsheet#7-sets--)
8. [Dictionaries](https://github.com/obitech/python_cheatsheet#8-dictionaries--)
9. [Modules](https://github.com/obitech/python_cheatsheet#9-modules--)
10. [I/O](https://github.com/obitech/python_cheatsheet#10-io--)
11. [Error Handling](https://github.com/obitech/python_cheatsheet#11-error-handling)
* [Sources](https://github.com/obitech/python_cheatsheet#sources)

## 1. Basics
### Arithmetics
Operator | Operation | Example | Evaluates to
--- | --- | --- | --- 
``**`` | Exponent | ``2 ** 3`` | 8
``%`` | Modulus/Remainder | ``22 % 8`` | 6
``//`` | Integer division | ``22 // 8`` | 2
``/`` | Division | ``22 / 8`` | 2.75
``*`` | Multiplication | ``2 * 5`` | 10
``-`` | Substraction | ``5 - 2 `` | 3
``+`` | Addition | ``5 + 2`` | 7

### Variables
Valid name | Invalid name | Rule
--- | --- | ---
``balance`` | ``current-balance`` | __no hyphen allowed__
``currentBalance`` | ``current balance`` | __no space allowed__
``current_balance`` | ``4current_balance`` | __can't begin with number__
``_balance`` | ``4`` | __can't begin with number__
``BALANCE`` | ``$balance`` | __no special characters__
``current_balance_4`` | ``'current_balance'``| __no special characters__

#### Assignments
```python
# Multiple assignments
>>> a, b = 0, 1
>>> a
0
>>> b
1
```

### Comparisons

Operator | Explanation
--- | ---
``>, >=`` | Less than, less than or equal
``<, <=`` | Greater than, greater than or equal
``==`` | Equal
``!=`` | Not equal
``is`` | __Object/type identity__
``is not `` | negated object identity
``a and b``| a & b
``a or b`` | a \| b
``not a`` | !a

## 2. Strings ([->](https://docs.python.org/3/tutorial/introduction.html#strings "Python 3.6 - Strings"))
### Basic printing
```python
>>> 'A string'
'A string'
>>> "A 2nd string"
'A 2nd string'
>>> print("Print a string")
Print a string

#  Removes \n
>>> print('Hello', end='')

# Separator
>>> print('cats', 'dogs', 'mice', sep=',')
cats,dogs,mice

# Multi line '\' prevents auto-add \n
print("""\
Multi line

strings.
""")

# Printing with arguments
>>> i = 42
>>> print("The value of i is", i)
The value of i is 42
```

### Concatination
```python
# Repetition + concat
>>> 3 * "ha" + "yes"
'hahahayes'

# Auto concat of string literals, need to be next to each other!
>>> 'test' 'case'
'testcase'

# Concat with variable
>>> prefix = "py"
>>> prefix + 'thon'
'python'

# Breaking down long strings
>>> string = ('Hello' 'World')
>>> string
'HelloWorld'

# Treat a string like a list/array. Note that there are no chars like in C, Just a string with size 1
>>> string
'HelloWorld'
>>> string = "Hello World"
>>> string[0]
'H'
>>> string[6]
'W'
>>> string[-1] # last character
'd'
>>> string [-2] # second-last character
'l'
```

### Slicing strings
Slicing will obtain a substring. __The start is always included, the end is always excluded__: ``s[:i] + s[i:] == s``. Default indices are 0 and length.
```python
>>> string[0:2] # Characters from pos 0 (incl) to pos 2 (excl)
'He'
>>> string[2:5] # Characters from pos 2 (incl) to pos 5 (excl)
'llo'
>>> string[:2] # Pos 0 - Pos 2
'He'
>>> string[2:] # Pos 2 - End
'llo World'
>>> string[:2] + string[2:]
'Hello World'
```
It's a good way to think of indices as marking the __borders__ of a position:
```python
 +---+---+---+---+---+---+
 | P | y | t | h | o | n |
 +---+---+---+---+---+---+
 0   1   2   3   4   5   6
-6  -5  -4  -3  -2  -1
```

### Behaviour
Strings are __immutable__.
```python
>>> string
'Hello World'

# Can't change a string
>>> string[0] = "c"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment

# Need to create a new string!
>>> "Bye" + string[5:]
'Bye World'

# Returns length
>>> len(string)
11
```

### Formatting
```python
# Python 3.x f-strings
>>> a = "Hello"
>>> b = 42
>>> c = [3.14, "World]"
>>> f"{a}, {b}, {c}"
"Hello, 42, [3.14, 'World']"

# Padding & alignment
>>> "{:>10}".format("test")
'      test'
>>> "{:<10}".format("test")
'test      '
>>> "{:^10}".format("test")
'   test   '
>>> "{:.^10}".format("test")
'...test...'

# Numbers
>>> "{:f}".format(3.141592653589793)
'3.141593'
>>> "{:.2f}".format(3.141592653589793)
'3.14'
>>> "{:06.2f}".format(3.141592653589793)
'003.14'
>>> "{:+2f}".format(3.141592653589793)
'+3.141593'
>>> "{:=+6.2f}".format(3.141592653589793)
'+ 3.14'

# Nested data structures
>>> arr = [13, 42, "test"]
>>> "{a[0]}, {a[1]}, {a[2]}".format(a = arr)
'13, 42, test'

# Parameters
>>> "{:{fill}{align}{width}}".format(string, fill="!", align="^", width="16")
'!!!HelloWorld!!!'
```
For more info on string formatting see [pyformat.info](https://pyformat.info/).

For more built-in string methods see [official doc](https://docs.python.org/3/library/stdtypes.html#string-methods "Python 3.6 - String Methods").

## 3. Lists ([->](https://docs.python.org/3/tutorial/introduction.html#lists "Python 3.6 - Lists"))
A list is an unordered, comma-seperated, [sequence](https://docs.python.org/3/glossary.html#term-sequence "Python 3.6 - Gloassary") of values of either the same of different types. The first index is zero. __Lists are mutable__.
```python
# Standard list
>>> numbers = [1, 2, 3, 4, 5, 6]
>>> numbers
[1, 2, 3, 4, 5, 6]

# Create a list from a range
>>> numbers = list(range(5))
>>> numbers
[0, 1, 2, 3, 4]

# List comprehension
>>> squares = [x**2 for x in range(10)]
>>> squares
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# Conditional list comprehension
[x for x in range(...) if (...)]
[x if (...) else (...) for x in ls]


# Lists can be nested too
>>> letters = ['a', 'b', 'c']
>>> list = [numbers, letters]
>>> list
[[1, 2, 3, 4, 5, 6], ['a', 'b', 'c']]
>>> list [0][2]
3
>>> list [1][2]
'c'
```
For more list comprehension see [docs](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions).

### Manipulation
All manipulation returns a new list.
```python
>>> numbers
[1, 2, 3, 4, 5, 6]

# Return value at index
>>> numbers[0]
1
>>> numbers[-2]
5

# Slicing
>>> numbers[3:]
[4, 5, 6]

>>> numbers [:-2]
[1, 2, 3, 4]

# Copy
>>> numbers[:]
[1, 2, 3, 4, 5, 6]

# Concat
>>> numbers + [1, 2, 4, 8]
[1, 2, 3, 4, 5, 6, 1, 2, 4, 8]

# Replace
>>> numbers[3] = 42
>>> numbers
[1, 2, 3, 42, 5, 6]

# Remove
>>> numbers[2:4] = []
>>> numbers
[1, 2, 5, 6]

>>> numbers[:] = []
>>> numbers
[]

>>> numbers[2:4] = [42, 23]
>>> numbers
[1, 2, 42, 23, 5, 6]

# Methods
>>> len(numbers)
6

>>> numbers.append(5 ** 2)
>>> numbers
[1, 2, 3, 42, 5, 6, 25]
```
For built-in list methods see [official doc](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists "Python 3.6 - More on Lists").

### Looping
```python
>>> array = ['a', 'b', 'c'] 

# .. in range()
>>> for i in range(len(array)):
...     print(i, array[i])
... 
0 a
1 b
2 c

# .. in enumerate()
>>> for i, v in enumerate(array):
...     print(i, v)
... 
0 a
1 b
2 c

# Using zip() to pair up two sequences
pass
```

### Common operations
Common __sequence__ operations (this is also applicable to strings):
Operation | Result
--- | ---
``x in s`` | ``True`` if ``x`` is part of ``s``
``s + t`` | Append ``t``to ``s``



## 4. Control flow ([->](https://docs.python.org/3/tutorial/controlflow.html))
### If/Else
```python
x = int(input("Please input integer: "))
if x < 0:
   print("x < 0")
elif x > 0:
   print("x > 0")
else:
   print("x = 0")

# Output
Please input integer: 42
x > 0   
```
### For-loop
This loops over every item in a sequence:
```python
animals = ["cats", "dogs", "birds", "fish"]

for i in animals:
   print("String:", i, "\t\nLength:", len(i))
```
For modifications, use a copy:
```python
animals = ["cats", "dogs", "mammals", "birds", "fish", "reptiles"]
for i in animals[:]:
   if len(i) > 6:
      # Adds HUMANS at beginning of array if one item is longer than 6
      animals.insert(0, "HUMANS")
print(animals)
['HUMANS', 'HUMANS', 'cats', 'dogs', 'mammals', 'birds', 'fish', 'reptiles']
```
### For..in..range()-loop
This loops over a range of numbers:
```python
# loops from 0 - 9
for x in range(10):
   print(x)

# 0, 3, 6, 9
range(0, 10, 3)

# -10, -40, -70
range(-10, -100, -30):
```

### pass-statement
The ``pass`` statement does nothing but can function as a placeholder.

## 5. Functions ([->](https://docs.python.org/3/tutorial/controlflow.html#defining-functions))
### Docstring
String literal at the beginning of function. Make sure to include this for doctumentation:
```python
def test():
    """This is a test function"""
    print("test")
    
# can be called by print(test.__doc__)
```

### Execution
From the [docs](https://docs.python.org/3/tutorial/controlflow.html#defining-functions "Python 3.6 - Defining Functions"), emphasis by me:
> The execution of a function introduces a new symbol table used for the local variables of the function. More precisely, all variable assignments in a function store the value in the local symbol table; whereas variable references first look in the local symbol table, then in the local symbol tables of enclosing functions, then in the global symbol table, and finally in the table of built-in names. Thus, __global variables cannot be directly assigned a value within a function__ (unless named in a global statement), although they may be referenced.

And:
>The actual parameters (arguments) to a function call are introduced in the local symbol table of the called function when it is called; thus, arguments are passed using __call by value__ (where the value is always an object reference, not the value of the object). (Actually, call by object reference would be a better description, since if a mutable object is passed, the caller will see any changes the callee makes to it (items inserted into a list.) When a function calls another function, a new local symbol table is created for that call

### Arguments
For default arguments, keyword arguments, argument lists, see [doc](https://docs.python.org/3/tutorial/controlflow.html#more-on-defining-functions).

### Returning values
Functions either returns a value or ``None``.
```python
numbers = [42]

def add_numbers(temp):
    for i in range(3):
        temp.append(i)
    # add_numbers(numbers) returns [42, 0, 1, 2]
    return temp
```

### Lambdas
Lambdas are small, anonymous, one-line functions
```python
>>> add = lambda n1, n2: n1+n2
>>> add(2,3)
5
```

## 6. Tuples ([->](https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences))
A Tuple is an __immutable__ list of values seperated by a comma and enclosed in parentheses:
```python
# Tuple packing
>>> tuple = 1, 2, 'test', 3
>>> tuple
(1, 2, 'test', 3)

# Tuple unpacking
>>> a, b, c, d = tuple
>>> c
'test'

# Immutability
>>> tuple[2] = 42
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment

# Empty tuple:
>>> tuple = ()
>>> tuple
()

# Tuple with single item, add trailing comma
>>> tuple = 42,
>>> tuple
(42,)
```

## 7. Sets ([->](https://docs.python.org/3/tutorial/datastructures.html#sets))
Unordered collection of items with no duplicates.
```python
>>> fruits = {'apple', 'banana', 'apple', 'plum', 'pear', 'plum'}
>>> fruits
{'pear', 'banana', 'apple', 'plum'}

# Create with set() method
>>> letters1 = set('aaaadsdasddsasdgfgfsdfasd')
>>> letters1
{'g', 's', 'f', 'd', 'a'}

>>> letters2 = set('kofkgskokdoasow')
>>> letters2
{'g', 's', 'k', 'f', 'o', 'd', 'w', 'a'}

# Returns items in a but _not_ b
>>> letters1 - letters2
set()

# Returns items in a _or_ b
>>> letters1 | letters2
{'g', 's', 'k', 'f', 'o', 'd', 'w', 'a'}

# Returns items in a _and_ b
>>> letters1 & letters2
{'g', 's', 'f', 'd', 'a'}

# Returns items in a _xor_ b
>>> letters1 ^ letters2
{'k', 'o', 'w'}
```

## 8. Dictionaries ([->](https://docs.python.org/3/tutorial/datastructures.html#dictionaries))
Array of key-value pairs. Key is immutable.
```python
# Creating a dictionary
>>> students = {'jack': 32, 'john': 25, 'james': 19}
>>> students
{'jack': 32, 'john': 25, 'james': 19}

# Create with dict() if keys are strings
>>> students = dict(jim=40, alex=19, nicole=23)
>>> students
{'jim': 40, 'alex': 19, 'nicole': 23}

# Adding a pair
>>> students['felix'] = 22
>>> students
{'jack': 32, 'john': 25, 'james': 19, 'felix': 22}

# Deleting a pair
>>> del students['felix']
>>> students
{'jack': 32, 'john': 25, 'james': 19}

# Displaying keys, returns view-object
>>> list(students.keys())
['jack', 'john', 'james', 'felix']
>>> sorted(students.keys())
['felix', 'jack', 'james', 'john']

# Checking if key is in dict
>>> 'james' in students
True
>>> 'nick' in students
False
```

### Looping
```python
>>> for key, value in students.items():
...     print(key, value)
... 
jim 40
alex 19
nicole 23
```

## 9. Modules ([->](https://docs.python.org/3/tutorial/modules.html))
Create ``arithm.py``, save in same folder:
```python
def add(a, b):
    return a + b

def sub(a, b):
    return a - b

def mult(a, b):
    return a * b
```
Using it:
```python
# 1)
import arithm
print(arithm.add(23, 4))

# 2)
import arithm as a
print(a.add(23, 4))

# 3)
from arithm import add, sub
print(add(23, 4))
print(sub(23, 4))
```
Use from command line:
```python
from arithm import add, sub

# This checks if called from command line
if __name__ == "__main__":
    import sys
    if len(sys.argv) != 3:
        sys.exit("Invalid # of arguments")
    print(add(sys.argv[1], sys.argv[2]))
```
## 10. I/O ([->](https://docs.python.org/3/tutorial/inputoutput.html#input-and-output))
### Advanced output formatting 
Code | Function | Example
--- | --- | ---
``str()``| Converts value to human-readable string | ``str("test\n\n"``
``repr()`` | Converts to interpreter-readable string | ``repr("test\n\n")``
``str.rjust(int)`` | Align right, ``int`` width | ``"test".rjust(10)``
``str.zfill(int)`` | Fill left side of expression with zeros, `int` width | ``"300".zfill(10)``

* See [docs](https://docs.python.org/3/library/string.html#format-specification-mini-language) for more information on format specifier commands
* See [docs](https://docs.python.org/3/library/string.html#formatexamples) for more format examples.

### Files
Flag | Explanation
--- | ---
``'r'`` | Read only, __default__
``'w'`` | Write only
``'a'`` | Append
``'r+'`` | Read/Write

#### Read/Write
```python
with open("workfile", "r") as f:
  for line in f:
    print(line)

# Write to file, returns characters written
>>> value = ('the answer', 42)
>>> s = str(value)  # convert the tuple to string
>>> s
"('the answer', 42)"
>>> f.write(s)
18
```

#### JSON
```python
# Read from JSON and save in dict
>>> import json
>>> with open("birthdays.json", "r") as f:
...     test_dict = json.load(f)
...
>>> test_dict
{'albert_einstein': '14.03.1879', 'benjamin_franklin': '17.01.1706', 'ada_lovelace': '10.12.1815'}

# Write  dict to JSON
>>> with open("birthdays.json", "w") as f:
...   json.dump(test_dict, f)
...
```

* See [docs](https://docs.python.org/3/tutorial/inputoutput.html#methods-of-file-objects) for basic file operations.
* See [docs](https://docs.python.org/3/tutorial/inputoutput.html#saving-structured-data-with-json) for __JSON__ conversion.

## 11. Error Handling
```python
>>> def divide(n):
...     try:
...             return 42 / n
...     except:
...             print('Invalid number')
...             return None
... 
>>> divide(5)
8.4
>>> divide(0)
Invalid number
```
## Sources
* [docs.python.org](https://docs.python.org/3/)
* [automatetheboringstuff.com](https://automatetheboringstuff.com)