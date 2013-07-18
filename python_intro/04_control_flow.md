Python 4: Control Flow
======================

Here we will discuss ways to control the flow of a program, including
conditional statements and loop statements.

*Adapted from* http://scipy-lectures.github.com

Conditionals
------------

```python
>>> if 2**2 == 4:
...     print 'Obvious!'
...
Obvious!
```

Note: Blocks are delimited by **indentation**
   
Type the following lines in your Python interpreter, and be careful
to **respect the indentation depth**. The Ipython shell automatically
increases the indentation depth after a column ``:`` sign; to
decrease the indentation depth, go four spaces to the left with the
Backspace key. Press the Enter key twice to leave the logical block.

```
In [1]: a = 10

In [2]: if a == 1:
   ...:     print(1)
   ...: elif a == 2:
   ...:     print(2)
   ...: else:
   ...:     print('A lot')
   ...:
A lot

Indentation is compulsory in scripts as well.

### Exercise: running a script from IPython
As a practice with this, open a file ``condition.py`` and re-type the above
statements.  Previously, we ran this file with ``$> python conditional.py``.
We can also run it from the IPython terminal, using

```
In [1]: %run condition.py
```

Try this out!


For loops and range
-------------------
Another important piece of coding is doing the same thing (or similar things)
multiple times.  We can do this with ``for`` loops and ``while`` loops.  We'll
focus on ``for`` loops here.

A typical for loop is an iteration over an index

```
>>> for i in range(4):
...     print(i)
0
1
2
3
```

But most often, it is more readable to iterate over values.  This is one feature
Python has that many languages don't:

```
>>> for word in ('cool', 'powerful', 'readable'):
...     print('Python is %s' % word)
Python is cool
Python is powerful
Python is readable
```


while looks and break/continue
------------------------------
``while`` loops are in some ways more general.  They can easily be used to
create infinite loops that will go on forever:

```
>>> while True:
...     pass # do nothing
```

To stop this, press ``Ctrl C``.

A typical C-style while loop is this, which solves the Mandelbrot problem:

```
>>> z = 1 + 1j
>>> while abs(z) < 100:
...     z = z**2 + 1
>>> z
(-134+352j)
```

### More advanced while-loops

``break`` out of enclosing for/while loop::

```
>>> z = 1 + 1j

>>> while abs(z) < 100:
...     if z.imag == 0:
...         break
...     z = z**2 + 1
```

``continue`` the next iteration of a loop.::

```
>>> a = [1, 0, 2, 4]
>>> for element in a:
...     if element == 0:
...         continue
...     print 1. / element
1.0
0.5
0.25
```


Conditional Expressions
-----------------------

- ``if <OBJECT>``

  Evaluates to False:
    * any number equal to zero (0, 0.0, 0+0j)
    * an empty container (list, tuple, set, dictionary, ...)
    * ``False``, ``None``

  Evaluates to True:
    * everything else

- ``a == b``:

  Tests equality, with logics::

    >>> 1 == 1.
    True

- ``a is b``:

  Tests identity: both sides are the same object::

    >>> 1 is 1.
    False

    >>> a = 1
    >>> b = 1
    >>> a is b
    True

- ``a in b``:

  For any collection ``b``: ``b`` contains ``a`` ::

    >>> b = [1, 2, 3]
    >>> 2 in b
    True
    >>> 5 in b
    False


  If ``b`` is a dictionary, this tests that ``a`` is a key of ``b``.

Advanced iteration
------------------

### Iterate over any *sequence*

You can iterate over any sequence (string, list, keys in a dictionary, lines in
a file, ...):

``` python
>>> vowels = 'aeiouy'

>>> for i in 'powerful':
...     if i in vowels:
...         print(i),
o e u
```

``` python
>>> message = "Hello how are you?"
>>> message.split() # returns a list
['Hello', 'how', 'are', 'you?']
>>> for word in message.split():
...     print word
...
Hello
how
are
you?
```

**Tip**
Few languages (in particular, languages for scientific computing) allow to
loop over anything but integers/indices. With Python it is possible to
loop exactly over the objects of interest without bothering with indices
you often don't care about. This feature can often be used to make
code more readable.


**warning**: It's not safe to modify the sequence you are iterating over!


### Keeping track of enumeration number

Common task is to iterate over a sequence while keeping track of the
item number.

* Could use while loop with a counter as above. Or a for loop::

  ``` python
  >>> words = ('cool', 'powerful', 'readable')
  >>> for i in range(0, len(words)):
  ...     print i, words[i]
  0 cool
  1 powerful
  2 readable
  ```

* But, Python provides ``enumerate`` keyword for this::

  ``` python
  >>> for index, item in enumerate(words):
  ...     print index, item
  0 cool
  1 powerful
  2 readable
  ```


### Looping over a dictionary

Use **iteritems**:

``` python
>>> d = {'a': 1, 'b':1.2, 'c':1j}

>>> for key, val in d.iteritems():
...     print('Key: %s has value: %s' % (key, val))
Key: a has value: 1
Key: c has value: 1j
Key: b has value: 1.2
```

Advanced: List Comprehensions
-----------------------------
List comprehensions are a way to condense for loops into a single statement.
They can be really fun!

``` python
>>> [i**2 for i in range(4)]
[0, 1, 4, 9]
```

They can be very useful and concise, but it's easy to misuse these and make
code very difficult to read.  For example:

``` python
def S(p):i=p.find('0');return[(s for v in
set(`5**18`)-{(i-j)%9*(i/9^j/9)*(i/27^j/27|i%9/3^j%9/3)or
p[j]for j in range(81)}for s in S(p[:i]+v+p[i+1:])),[p]][i<0]
```

This is a piece of python code I wrote that can solve any sudoku puzzle
(see http://jakevdp.github.io/blog/2013/04/15/code-golf-in-python-sudoku/
for a discussion).  But, you should **never** write real code as obscured
as this.


Exercise
--------
Compute the decimals of Pi using the Wallis formula:

![\pi = 2 \prod_{i=1}^{\infty} \frac{4i^2}{4i^2 - 1}](formula.png)
