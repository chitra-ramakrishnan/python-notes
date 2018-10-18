# 19-oct-2018

### 8 - pytest benchmark

- nice function performance benchmarking

```bash
pip3 install pytest pytest-benchmark
```

```python
import re
import string
import random

# Python ZIP version
def count_doubles(val):
    total = 0
    for c1, c2 in zip(val, val[1:]):
        if c1 == c2:
            total += 1
    return total


# Python REGEXP version
double_re = re.compile(r'(?=(.)\1)')

def count_doubles_regex(val):
    return len(double_re.findall(val))


# Benchmark it
# generate 1M of random letters to test it
val = ''.join(random.choice(string.ascii_letters) for i in range(1000000))

def test_pure_python(benchmark):
    benchmark(count_doubles, val)

def test_regex(benchmark):
    benchmark(count_doubles_regex, val)
```

### 7 - input(): disaster

- [ ] TODO find out why this is designed like this: to evaluate the input string
- Also, notice the dunder import

```python
>>> input()
dir()
['__builtins__', '__doc__', '__name__', '__package__']
>>> input()
__import__('sys').exit()
```

### 6 - public, private , secret simple example

```python
class Foo(object):
    def __init__(self):
        self.public = 'public'
        self._private = 'public'
        self.__secret = 'secret'

>>> foo = Foo()
>>> foo.public
'public'
>>> foo._private
'public'
>>> foo.__secret
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Foo' object has no attribute '__secret'
>>> foo._Foo__secret
'secret'
```

### 5 - list comprehension for flattening

```python
words = ['her', 'name', 'is', 'rio']
letters = [letter for word in words for letter in word]
```    

### 4 - yield syntax in python3

```python
yield from gen()
```

### 3 - LEGB scoping rules of Python

LEGB Rule.

L, Local — Names assigned in any way within a function (def or lambda), and not declared global in that function.

E, Enclosing-function locals — Name in the local scope of any and all statically enclosing functions (def or lambda), from inner to outer.

G, Global (module) — Names assigned at the top-level of a module file, or by executing a global statement in a def within the file.

B, Built-in (Python) — Names preassigned in the built-in names module : open,range,SyntaxError,...


### 2 - Naming list slices

```python
>>> a = [0, 1, 2, 3, 4, 5]
>>> LASTTHREE = slice(-3, None)
>>> LASTTHREE
slice(-3, None, None)
>>> a[LASTTHREE]
[3, 4, 5]
```

### 1 - get python config information

```bash
$ python -m sysconfig
```