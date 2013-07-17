Hello World x4
==============
In this section, we'll learn the "hello world" of python, four different ways.
We'll discuss these ways of using Python, including their advantages and
disadvantages.  We'll make use of all of these throughout the tutorial.

As we go, we'll look at several basic building blocks of Python: print
statements, variables, and basic operations.



Basic command-line
------------------
The basic command-line interface for Python is how many people get started
experimenting with the language.  Open a *terminal* and you'll get a terminal
prompt.  Depending on your system, this prompt might have your username or
directory information.  Mine looks like this:

```
jakesmac:jakevdp$
```

Yours might look different. As a shortcut, we'll use the symbol ``>$`` to
indicate a terminal prompt.

At your terminal prompt, type the command ``python``, and you should see
something like the following:

```
>$ python
Python 2.7.3 |Anaconda 1.4.0 (x86_64)| (default, Feb 25 2013, 18:45:56) 
[GCC 4.0.1 (Apple Inc. build 5493)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

It shows some information about your Python installation, and then gives you
the standard python command-line interpreter prompt: ``>>>``.  You can type
things at this prompt -- for example,

```
>>> print("hello world")
hello world
```

This is a very simple Python script: printing any string.  This also can be
very convenient as a quick calculator, using the symbols ``+``, ``-``, ``*``,
and ``/``.  Try this out with a few examples, and note here that white space
doesn't matter.

```
>>> 1 + 1
2
>>> 2 * 16
32
>>> 6 / 3
2
>>> 10 - 5
5
```

*Did you see any unexpected behavior with the division operator?
We'll discuss this a bit later.*




IPython command-line
--------------------
The basic command line lacks a few features that we'd like for an IDE
(that's **I**nteractive **D**evelopment **E**nvironment), so fortunately
there are other options out there.  If you've set up your python 
installation correctly ([Anaconda](https://store.continuum.io/) is a
good option) then you can use the IPython (Interactive Python) interpreter
instead.

Press ``Ctrl d`` to exit out of the Python interpreter, and then at your
command prompt type:

```
>$ ipython
Python 2.7.3 |Anaconda 1.4.0 (x86_64)| (default, Feb 25 2013, 18:45:56) 
Type "copyright", "credits" or "license" for more information.

IPython 0.13.1 -- An enhanced Interactive Python.
?         -> Introduction and overview of IPython's features.
%quickref -> Quick reference.
help      -> Python's own help system.
object?   -> Details about 'object', use 'object??' for extra details.

In [1]:
```

Here we see the standart IPython prompt: an input with a line number.  Let's
do our hello world example again:

```
In [1]: print("hello world")
hello world
```

You'll notice that the next prompt is ``In [2]``.  The IPython interpreter
keeps track of commands in a way that allows you to reference them in following
commands.  We'll explore that more later, but for now, just notice that the
special character ``_`` stores the result of the last computation.
For example:

```
In [2]: 1 + 1
Out[2]: 2

In [3]: _ * 4
Out[3]: 8
```

You can also refer to results from their particular line numbers:

```
In [4]: _2 + _3
Out[4]: 10
```

This added the output of command 2 to the output of command 3.  Note that
these tricks only work within the IPython interpreter, not within the standard
Python interpreter.

IPython has a lot more interesting features we'll see, but we won't cover them
all right now.



Using a .py File
----------------
For simple tasks like adding a few numbers, a command-line interface can be
useful.  But for more substantial tasks, it can be more useful to write the
code in a file and execute it all at once.

To do this, you'll need a good plain-text editor.  A word processor or other
program with fancy formatting will not work well for this.  I'd recommend
something along the lines of gedit or emacs.

Use your text editor to open a file in the current directory
(name the file "hello_world.py": the '.py' is a standard extention which
marks it as a python file), and write the following code:

``` python
# file: hello_world.py
print("hello world")

# add some numbers
print("I'm going to add 2 and 2")
print(2 + 2)
```

Now to execute this file, return to the command-line and type the following:

```
>$ python hello_world.py
```

You should see the following output:

```
hello world
I'm going to add 2 and 2
4
```

You'll notice that the lines starting with ``#`` didn't do anything.  In
Python, the pound sign is used as an indicator of comments.  Anything after
the ``#`` will be ignored by the interpreter.

###Making Things Interactive
We can use these tools to make a quick interactive script.  Type the following
into your ``hello_world.py`` file:

``` python
# hello_world.py
name = raw_input("enter your name: ")
print("hello " + name)
```

Run the file, and see how it behaves.  What we've done here is to use the
*function* ``raw_input`` to get input from the user, and stored that input
in a *variable* called ``name``.  We then print the name and the greeting
together to get a customized salutation.

#### Exercise
Create a script that uses multiple ``raw_input`` calls to ask for a name,
a title, and a saluation.  The interaction should look something like this:

```
What is your name? Jake
What is your title? Dr.
What is your preferred greeting? Whazzup

Whazzup Dr. Jake
```

Take a few moments to create this script. You should use a different variable
to store each response.  A variable name can be (nearly) any string
consisting of capital and lowercase letters, underscores, and digits, as
long as the first character is not a digit.



Using IPython notebook
----------------------
The fourth method we will use to interact with Python is the IPython notebook.
This is very similar to the IPython command prompt we saw above, but it
runs within a web browser.  Assuming you have all the dependencies installed,
you can type at the terminal prompt

```
>$ ipython notebook
```

and the notebook dashboard should appear in your web browser.  The remainder
of this tutorial section will take place in the notebook
``notebook_intro.ipynb``, which you can find in the current git repository.
To open it, you'll have to run the ``ipython notebook`` command from within
the directory that contains this file.