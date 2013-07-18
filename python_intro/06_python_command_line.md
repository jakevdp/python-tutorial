Python and the Command Line
===========================

Earlier, we heard about how to use the shell effectively, and how to run
programs and pass commands to them.

Here, briefly, we'll talk about using this from within Python.

It's pretty simple, really.  All we need is to import the ``sys`` module, and
do something like the following:

``` python
# file: command_line.py
import sys
print sys.argv
```

Create this file, and run it from the command line:

```
>$ python command_line.py arg1 arg2 -v arg3
['command_line.py', 'arg1', 'arg2', '-v', 'arg3']
```

We see that anything after the ``python`` command is stored in the list called
``sys.argv``.


Exercise
--------
write a python script ``add.py`` which adds two numbers.  For example, the
output should be

```
>$ python add.py 2 3
5
```

Note that the arguments are passed as strings, and will have to be converted
to floating point numbers with ``float()``

### Bonus

write a python script ``arithmetic.py`` which performs basic arithmetic
operations.  For example:

```
>$ python arithmetic.py add 2 3
5
>$ python arithmetic.py multiply 4 5
20
>$ python arithmetic.py subtract 5 3
2
>$ python arithmetic.py divide 5 2
2.5
```

More Complicated Arguments
--------------------------
For more complicated argument parsing, the ``argparse`` package is useful.
Here's an example of a script using ``argparse`` which sums integers from
the command-line

``` python
# file: sum.py
import argparse
import sys

parser = argparse.ArgumentParser(description = 'sum the integers at the command line')
parser.add_argument('integers', metavar='int', nargs='+', type=int,
                    help='an integer to be summed')
parser.add_argument('--log', default=sys.stdout, type=argparse.FileType('w'),
                    help='the file where the sum should be written')
args = parser.parse_args()
args.log.write('%s' % sum(args.integers))
args.log.write('\n')
args.log.close()
```

Now you can type

```
>$ python sum.py 1 2 3 4
10
```

This may seem extreme for such a simple example, but it has some nice features,
including automatically generating documentation:

```
>$ python sum.py --help
usage: sum.py [-h] [--log LOG] int [int ...]

sum the integers at the command line

positional arguments:
  int         an integer to be summed

optional arguments:
  -h, --help  show this help message and exit
  --log LOG   the file where the sum should be written
jakesmac:python_intro jakevdp$ python sum.py --help
usage: sum.py [-h] [--log LOG] int [int ...]

sum the integers at the command line

positional arguments:
  int         an integer to be summed

optional arguments:
  -h, --help  show this help message and exit
  --log LOG   the file where the sum should be written
```

Further, there are many options which can be used to easily create very
sophisticated command-line interfaces.

### Exercise
Repeat the previous arithmetic exercise, but use ``argparse`` to process the
arguments.