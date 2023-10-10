introduction to python using jupyterlab
========================================

.. note::

    This is a **non-interactive** version of the exercise. If you want to run through the steps yourself and see the
    outputs, you'll need to do one of the following:

    - follow the setup steps and work through the notebook on your own computer
    - open the workshop materials on `binder <https://mybinder.org/v2/gh/iamdonovan/intro-to-python/HEAD>`__ and work
      through them online
    - open a python console, copy the lines of code here, and paste them into the console to run them

overview
--------

Programming is a powerful tool that allows us to do complicated
calculations and analysis, visualize data, and automate workflows to
ensure consistency, accuracy, and reproducibility in our research.

In this exercise, you will get a basic introduction to the python
programming language, including variables and objects, data types, and
how to control the flow of our programs. Over the next few sessions, we
will build on these ideas, using some real example data, to get more of
an idea of how to use python in our research.

This is an interactive notebook - in between bits of text, there are
interactive cells which you can use to execute snippets of python code.
To run these cells, highlight them by clicking on them, then press CTRL
and ENTER (or SHIFT and ENTER, or by pressing the “play” button at the
top of this tab).

objectives
----------

After finishing this exercise, you will:

-  learn and gain experience with some of the basic elements of python
   and programming
-  learn how to use the python command line interface

objects and assignment
----------------------

We’ll start by creating a new object, foo, and assigning it a value of
``hello, world!``:

.. code:: python


       foo = "hello, world!" # assign an object using =

In the text above (and the cell below), you should notice that the color
of different parts of the text is different. We’ll discuss different
aspects of this as we go, but pay attention to the greenish text that
comes after the ``#`` - this indicates a *comment*, meaning text that is
intended for humans to read, but that is ignored by the python
interpreter. We’ll discuss comments more when we start looking at
writing scripts, but as you work through the exercises, make sure to
read the comments - they’re there to help you understand what each line
of code actually does.

After creating the ``foo`` **object**, we use the built-in ``print()``
(`documentation <https://docs.python.org/3/library/functions.html#print>`__)
function (more on these later) to see the *value* of that object.

Go ahead and run the cell to get started:

.. code:: ipython3

    foo = "hello, world!" # assign an object using =
    print(foo) # print the value of the object to the screen

You should notice that the cell has changed. First, the square brackets
(``[ ]``) have a number inside of them (``[1]``), and you can also see
the output below the cell.

Often, you will want to know how to use a particular function. To get
help, we can use the built-in ``help()`` function
(`documentation <https://docs.python.org/3/library/functions.html#help>`__).
For example, to get more information on how to use the ``print()``
function:

.. code:: ipython3

    help(print) # use the help() function to find out more about particular functions

Alternatively, in a jupyter notebook (or IPython terminal), we can use
``?`` (the question mark operator) to do the same:

.. code:: ipython3

    ?print

variable names
--------------

We have already seen one example of a variable, ``foo``, above. Remember
that in programming, a variable is name that represents or refers to a
value. Variables store temporary information that can be manipulated or
changed as we type commands or run scripts.

One important thing to remember is that the *name* of an **object** is
*case-sensitive* (meaning that ``foo`` is different from ``Foo``):

.. code:: ipython3

    print(Foo) # this won't work, because we haven't created an object called Foo yet

We’ll see more examples of error messages later (and how to interpret
them), but hopefully the message:

.. code:: pytb

       NameError: name 'Foo' is not defined

is clear enough. Because we were expecting this error message, we can
ignore it and move on for now.

In python, variable names can consist of letters, digits, or
underscores, but they cannot begin with a digit. If you try to name a
variable using an illegal name, you will get a ``SyntaxError``:

.. code:: pytb


   >>> 3var = "this won't work"
     Cell In[5], line 1
       3var = 'this won't work'
        ^
   SyntaxError: invalid decimal literal

To confirm this, try it for yourself below:

.. code:: ipython3

    3var = "this won't work"

Here, we see a ``SyntaxError`` raised - this means that the code we have
written violates the *syntax* (grammar) of the language. We’ll look more
at different error types in the debugging exercise later on.

data types
----------

So, we’ve created our first **object**, ``foo``. But what kind of object
is ``foo``? To find out, we can use the ``type()`` function
(`documentation <https://docs.python.org/3/library/functions.html#type>`__):

.. code:: ipython3

    type(foo) # use the type() function to find the type of an object

So ``foo`` is an object of type **str**, (“string”), meaning that it is
*text*.

In general, python has the following basic data types:

In practice, variables can refer to almost anything. Variables can also
be **int**\ egers, **float**\ ing point numbers (decimal numbers),
**list**\ s, **tuple**, **dict**\ ionaries, entire files, and many more
possibilities.

numeric operations
------------------

A large part of what we will use python for is the manipulation of
numeric data. Thus, it is a good idea for us to understand how python
treats numeric data. In the cell below, we first define two variables,
``x`` and ``y``, and assign them values of 2 and 3, respectively.

Before you run the cell, look at the print statements - these will show
which operators are being used (``+``, ``-``, ``*``, etc.), along with
the output of the operation using the variables ``x`` and ``y``. Think
about what you exect the results to be - when you run the cell, do the
outputs match your expectation? Why or why not?

.. code:: ipython3

    x = 2
    y = 3

    print(f"x + y = {(x+y)}") # print the value of x + y (addition)
    print(f"x - y = {(x-y)}") # print the value of x - y (subtraction)
    print(f"x * y = {(x*y)}") # print the value of x * y (multiplication)
    print(f"x / y = {(x/y)}") # print the value of x / y (division)
    print(f"x // y = {(x//y)}") # print the value of x // y (floor division)
    print(f"x ** y = {(x**y)}") # print the value of x ** y (exponentiation)
    print(f"x % y = {(x%y)}") # print the value of x % y (modular division)
    print(f"x ^ y = {(x^y)}") # print the value of x ^ y (bitwise XOR)

Most of these should be fairly straightforward, except perhaps for the
last two (``%`` and ``^``). The ``%`` (“modular” operator) returns the
remainder of dividing two numbers. The ``^`` (“bitwise XOR” or “bitwise
exclusive or”) does something a little more involved - for more
information about bitwise operators in general, see this `Wikipedia
article <https://en.wikipedia.org/wiki/Bitwise_operation#Bitwise_operators>`__.

Note also how we’re using ``print()`` here, with a “`formatted string
literal <https://docs.python.org/3/tutorial/inputoutput.html#tut-f-strings>`__”
(or “**f-String**”, ``f"{}"``). By prefixing the string with the letter
``f``, we can include the value of an expression inside the string,
using the ``{ }`` operators. We’ll look at more examples of how to use
these later on, including how we can format numbers inside of strings.

string variables and operations
-------------------------------

We have already worked with one example of a **str** (string) variable,
``foo``. We can easily access parts of a string by using the desired
index inside square brackets ``[ ]``. Remember that the index starts
from 0, and it has to be an **int**\ eger value:

.. code:: ipython3

    foo[0] # get the first element of foo, 'h'

If we use a **float**\ ing point value, it raises a ``TypeError``:

.. code:: ipython3

    foo[0.0] # slice indices have to be integers, not floats!

To access the last element of a **str** (or any sequence), we could
count up all of the elements of the **str** and subtract one (remember
that we start counting at 0, not 1), but python gives us an easier way:
*negative indexing*.

Thus, to get the last element of ``foo``, we can type ``foo[-1]``. To
get the second-to-last element, we could type ``foo[-2]``, and so on:

.. code:: ipython3

    foo[-1] # get the last character in foo

If we want to access more than one element of the string, we can use
multiple indices, with the basic form of:

.. code:: python

   sliced = foo[first:last]

This will select the letters of the string starting at index ``first``
up to, **but not including**, ``last``.

This is also called **slicing**. Before running the cell below, think
about what the result should be:

.. code:: ipython3

    foo[1:5] # get the characters from index 1 to 4

If we want to find an element in a string, we can use the
helpfully-named built-in function (or method) ``.find()``. For example,
typing ``foo.find('W')`` will return the index of the first occurrence
of the character ``'w'``:

.. code:: ipython3

    foo.find('w') # return the first index of the letter w

What happens if the given character (or substring) isn’t found in the
string? Write a line of code in the cell below to check.

.. code:: ipython3

    # write a line of code to try to find a character that isn't in 'hello, world!'

Finally, although we can’t subtract or divide strings, we do have two
operators at our disposal: ``+`` (concatenation) and ``*`` (repeated
concatenation).

Before running the cell below, what do you expect will be stored in each
variable below? Does the result match what you expected?

.. code:: ipython3

    new_string = "Hello" + "World!" # use string concatenation
    rep_string = "Hello" * 5 # use repeated concatenation

    print(f'newString is: {new_string}')
    print(f'repString is: {rep_string}')

lists
-----

**list**\ s are an incredibly powerful and versatile data type we can
use in python to store a sequence of values.

Any other data type can be inserted into a **list**, including other
**list**\ s. Run the following cell to see how we can create a new
**list** object:

.. code:: ipython3

    fruits = ["Apple", "Banana", "Melon", "Grapes", "Raspberries"] # create a list of fruits
    print(fruits) # print the value of the list

Like with **str** objects, we can access and manipulate **list** objects
using indexing and slicing techniques, in much the same way.

Can you write a command below to ``print()`` ‘Grapes’ by using the
corresponding index from the **list**?

.. code:: ipython3

    print() #insert the correct command inside the ()

If we want to access more than one element of a list, we can slice the
list, using the same syntax as with the ``foo`` examples above.

What do you think will print if you run the cell below?

.. code:: ipython3

    fruits[2:-1] # think about what this output will look like

What about this cell?

.. code:: ipython3

    fruits[2:-1][0] # what will this show?

and finally, what about this?

.. code:: ipython3

    fruits[2:-1][0][-1]

As you can see from the examples above, while indexing a **list**
returns the value of a single element, a **list** slice is itself a
**list**. This difference is subtle, but important to remember.

classes, functions and methods
------------------------------

In programming, a **function** is essentially a short program that we
can use to perform a specific action. Functions take in **parameters**
in the form of **arguments**, and (often, but not always) return a
result, or otherwise perform an action. Parameters can be **positional**
(in other words, the order they are given matters), or they can be
**keyword** (i.e., you specify the argument with the parameter name, in
the form ``parameter=value``).

Python has a number of built-in functions for us to use. For example,
instead of typing ``2 ** 8`` to raise 2 to the power of 8, we could
instead have typed ``pow(2,8)``:

.. code:: ipython3

    print(f'using the ** operator: {2**8}')
    print(f'using the pow() function: {pow(2, 8)}')

Here, we are calling the function ``pow()`` and supplying the
**positional** arguments ``2`` and ``8``. The result returned is the
same, ``256`` (or 28), but the approach used is different.

To see a list of the built-in functions, have a look at the python
`documentation <https://docs.python.org/3/library/functions.html>`__.
Alternatively, you can type ``print(dir(__builtins__))`` (note the two
underscores on either side of **builtins**):

.. code:: ipython3

    print(dir(__builtins__)) # show a list of all of the builtin functions

While it may not be completely clear at first what each of these things
are, remember that we can use the ``help()`` **function** to get more
information.

For example, one very useful built-in **class** is ``range``
(`documentation <https://docs.python.org/3/library/stdtypes.html#range>`__).

To create a new **range** object, we call it like we would a function:

.. code:: python

   range(stop)
   range([start,] stop [,step])

“Under the hood”, so to speak, remember that this is actually calling
the **\__init\_\_()** method of the **class**, which is the **function**
that python uses to *initalize*, or create, a new object.

Note that ``range()`` takes between one and three arguments:

-  ``range(stop)`` creates a **range** object that will “count” from 0
   up to (but not including) ``stop``, incrementing by 1.
-  ``range(start, stop)`` creates a **range** object that will “count”
   from ``start`` up to (but not including) ``stop``, incrementing by 1.
-  ``range(start, stop, step)`` creates a **range** object that will
   “count” from ``start`` to (but not including) ``stop``, incrementing
   by ``step``.

To pass multiple parameters to a function, we separate each parameter by
a comma. In the cell below, write a statement that returns a list of
numbers counting from a ``start`` of 10 to 0 (inclusive).

.. code:: ipython3

    for ii in range(start, stop, step): # modify this to print out a list of numbers 10, 9, 8, ... 0.
        print(ii)

A **method** is a type of **function** that acts directly on an object.

In general, methods are called just like functions - the general syntax
is ``object.method(arguments)``.

For example, **str** objects have a **method**, ``.count()``
`documentation <https://docs.python.org/3/library/stdtypes.html#str.count>`__,
which counts the number of times a character (or substring) occurs in
the **str**. The cell below should output the number of times the
character ``l`` occurs in ``foo`` (3):

.. code:: ipython3

    foo.count('l')

Another powerful **str** method is ``.split()``
`documentation <https://docs.python.org/3/library/stdtypes.html#str.split>`__,
which returns a **list** of the given **str**, split into substrings
based on the delimeter provided as an argument:

.. code:: python3

   >>> help(str.split)

   split(self, /, sep=None, maxsplit=-1)
       Return a list of the words in the string, using sep as the delimiter string.

       sep
         The delimiter according which to split the string.
         None (the default value) means split according to any whitespace,
         and discard empty strings from the result.
       maxsplit
         Maximum number of splits to do.
         -1 (the default value) means no limit.

From this, we can see that if we call ``.split()`` without any arguments
at all, it will split the string based on any whitespace and discard any
*empty* strings. That is, if we have multiple spaces in our string, it
will treat those as a single space:

.. code:: ipython3

    singlespace = 'programming skills for phd researchers'
    multispace = 'programming        skills   for  phd     researchers'

    print(singlespace.split()) # split on any whitespace
    print(multispace.split()) # split on any whitespace

If we want to specify a single space character (``' '``), though, the
result will change:

.. code:: ipython3

    print(singlespace.split(' ')) # split on a single space
    print(multispace.split(' ')) # split on a single space

defining our own functions
--------------------------

Often, we will want to define our own **function**\ s. Using functions
has many benefits, including:

-  improving readability,
-  eliminating repetitive code,
-  allowing for easier debugging of a program,
-  and even allowing us to re-use code in other scripts/programs.

Defining a **function** in python is quite easy.

We begin the definition with a ``def`` **statement** that includes the
function name and all parameters (this first line is also called the
**header**). The header must end with a colon (``:``):

.. code:: python

   def cat_twice(str1, str2):

The **body** of the function (i.e., the set of instructions that make up
the function) is *indented* - like other forms of flow control in
python, once the interpreter sees a non-indented line, it marks the end
of the function:

.. code:: python

   def cat_twice(str1, str2):
      cat = str1 + str2
      print(cat) # this is part of the function
      print(cat) # this is part of the function

   # this is no longer part of the function

To help illustrate this, let’s define a function for calculating the
area of a circle. Mathematically, this is a function of the radius of
the circle - equal to the constant pi multiplied by the radius squared.
Run the cell below to create the new function, and then test it:

.. code:: ipython3

    from math import pi # import the constant pi from the math module

    def circle_area(radius):
        area = pi * radius ** 2 # calculate the area of the circle using the radius argument
        return area # use return to get a value back from the function

    circle_area(10) # get the area of a circle with radius 10 (should be 314.15 ...)

In the cell below, I’ve started two more functions for calculating the
surface area and volume of a sphere. For each function, fill in the code
that will return the correct result, then confirm that your function
output matches the values shown in the comment on each line.

.. code:: ipython3

    def sphere_area(radius):
        # your code goes here!

    def sphere_volume(radius)
        # your code goes here!

    print(sphere_area(10)) # get the surface area of a sphere with radius 10 (should be 1256.637)
    print(sphere_volume(10)) # get the volume of a sphere with radius 10 (should be 4188.79)

In the exercises to come, we’ll define and use a number of other
functions.

controlling flow
----------------

Some of the most important uses that we’ll have for programming are
repeating tasks and executing different code based on some condition.
For example, we might want to loop through a list of files and run a
series of commands on each file, or apply an analysis only if the right
conditions are met.

In python, we can use the ``while``, ``for``, and ``if`` operators to
control the flow of our programs. For example, given a number, we might
want to check whether the value is positive, negative, or zero, and
perform a different action based on which condition is ``True``:

.. code:: ipython3

    def pos_neg_zero(x): # a function to tell us whether a number is positive, negative, or 0
        if x > 0: # if x > 0, print that it is positive
            print(f'{x} is a positive number')
        elif x < 0: # if x < 0, print that it is negative
            print(f'{x} is a negative number')
        else: # if
            print(f'{x} is zero')

Here, we take in a number, ``x``, and execute code based on whether
``x`` is positive, negative, or zero.

Like the header of a function, an ``if`` or an ``elif`` **statement**
has to be terminated with a colon (``:``).

There isn’t a limit to the number of ``elif`` statements we can use, but
note that the order matters - once a condition is evaluated as ``True``,
the indented code is executed and the whole block is exited. For this
reason, an ``else`` **statement** is optional, but it must always be
last (since it automatically evaluates as ``True``).

Run the cell below to see how the output of the function changes based
on the input:

.. code:: ipython3

    pos_neg_zero(-1) # a negative number
    pos_neg_zero(1) # a positive number
    pos_neg_zero(False) # a weird one

Note that in the example above, ``False`` has evaluated as being equal
to zero. This is because in python, **bool** (“Boolean”) objects
(``True`` and ``False``) are subclasses of **int**, and ``False`` has a
value of ``0``, while ``True`` has a value of ``1``. For more on how
python tests for truth values, see the
`documentation <https://docs.python.org/3/library/stdtypes.html#truth-value-testing>`__.

In addition to conditional flow, we might also want to repeat actions.
For example, we can write a simple function that counts down to some
event, then announces the arrival of that event. We could define this
function using a ``while`` loop, making sure to update a variable in
each step:

.. code:: ipython3

    def countdown(n):
        while n > 0:
            print(n)
            n -= 1 # note that this is the same as n = n - 1
        print("Blastoff!")

    countdown(5) # count down from 5 to zero

Note the importance of updating the variable that we are testing in the
loop. If we remove the ``n -= 1`` line, our function will never stop
running (an **infinite loop**).

``while`` loops are useful for actions without a pre-defined number of
repetitions. We could just as easily re-define ``countdown()`` using a
``for`` loop, using ``range()``:

.. code:: ipython3

    def countdown_for(n):
        for ii in range(n, 0, -1):
            print(ii)
        print("Blastoff!")

    countdown_for(5) # run the function to count down from 5

This version uses ``range`` to iterate from ``n`` to 1 in increments of
-1, printing the value of ``i`` each time - that is, we leave ``n``
unchanged.

We can also use the ``break`` statement to **break** out of a loop:

.. code:: ipython3

    def break_example(n):
        # prints values from n to 1, then Blastoff!
        while True:  # here, the loop will always run
        # unless we reach a condition
        # that breaks out of it:
            if n <= 0:
                break
            print(n)
            n -= 1
        print("Blastoff!")

    break_example(5) # run the function to count down from 5

or the ``continue`` statement to continue to the next step of a loop:

.. code:: ipython3

    def continue_example(n):
        # given an integer, n, prints the values from 0 to n that are even.
        for x in range(n):
            if x % 2 == 1:
                continue
            print('{} is even'.format(x))

    continue_example(10) # print the even integers from 0 to 9 (remember that range(n) is not inclusive!)

importing modules
-----------------

Modules provide a convenient way to package functions and object
classes, and load these items when needed. This also means that we only
end up loading the functionality that we need, which helps save on
memory and other resources. We have already imported one such module,
the ``math`` module, which provides much more than the built-in
operators we explored earlier.

Specifically, we imported ``pi`` **from** the ``math`` module - that is,
rather than importing the entire module, we only imported the attribute
``pi``. When we import the entire module, we can access the attributes,
classes, functions, etc. using a ``.``:

.. code:: ipython3

    import math # import the entire math module

    print(math.pi) # print the value of math.pi

When we specifically name the things we want to import, we only have
access to those things - importing ``pi`` from ``math`` does not also
import ``floor`` - hence, the error message when you run the cell below:

.. code:: ipython3

    print(f'math.floor(10.19) is equal to: {math.floor(10.19)}') # print the output of math.floor(10.19)
    print(f'floor(10.19) is equal to:      {floor(10.19)}') # print the output of floor(10.19)

To import multiple things from a single module, you can separate them by
commas:

.. code:: ipython3

    from math import pi, floor, sin, cos, tan # import pi, floor, sin, cos, and tan from math

We will look quite a bit more at importing modules/packages in the
exercises to come.

recap
-----

That’s all for this exercise. In this lesson, we have introduced the
following concepts:

-  variables, objects, values, and assignment
-  data types
-  arithmetic operations
-  indexing with **str** and **list** objects
-  functions and methods
-  defining our own functions
-  flow control using logic
-  importing modules

Next, we’ll put some of this to work by having a look at a broken
program, and see if we can manage to fix it.
