introduction to **R** using jupyterlab
=======================================

.. note::

    This is a **non-interactive** version of the exercise. If you want to run through the steps yourself and see the
    outputs, you'll need to follow the setup steps and work through the notebook on your own computer.

overview
--------

Programming is a powerful tool that allows us to do complicated
calculations and analysis, visualize data, and automate workflows to
ensure consistency, accuracy, and reproducibility in our research.

In this exercise, you will get a basic introduction to the **R**
programming language, including variables and objects, data types and
data structures, and how to control the flow of our programs. Over the
next few sessions, we will build on these ideas, using some real example
data, to get more of an idea of how to use **R** in our research.

This is an *interactive* notebook - in between bits of text, there are
interactive cells which you can use to execute snippets of **R** code.
To run these cells, highlight them by clicking on them, then press
**CTRL** and **ENTER** (or **SHIFT** and **ENTER**, or by pressing the
“play” button at the top of this tab).

objectives
----------

After finishing this exercise, you will:

-  learn and gain experience with some of the basic elements of **R**
   and programming

objects and assignment
----------------------

We’ll start by creating a new **object**, ``foo``, and *assigning* it a
**value** of ``"hello, world!"``:

.. code:: r

       foo <- "hello, world!" # assign an object using <-

In the text above (and the cell below), you should notice that the color
of different parts of the text is different. We’ll discuss different
aspects of this as we go, but pay attention to the greenish text that
comes after the ``#`` - this indicates a *comment*, meaning text that is
intended for humans to read, but that is ignored by **R**. We’ll discuss
comments more when we start looking at writing scripts, but as you work
through the exercises, make sure to read the comments - they’re there to
help you understand what each line of code actually does.

After creating the ``foo`` **object**, we use the built-in ``print()``
function (more on these later) to see the *value* of that object. Go
ahead and run the cell to get started:

.. code:: r

    foo <- "hello, world!" # assign an object using <-
    print(foo) # print the object to the terminal

You should notice that the cell has changed. First, the square brackets
(``[ ]``) have a number inside of them (``[1]``), and you can also see
the output below the cell:

``[1] "hello, world!"``

The ``print()`` function allows us to print messages and information to
the screen. We’ll see a number of other uses of it as we go, but you can
also read more about it in the
`documentation <https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/print>`__.

One important thing to remember is that the *name* of an **object** is
*case-sensitive* (meaning that ``foo`` is different from ``Foo``):

.. code:: r

    print(Foo) # this won't work, because we haven't created an object called Foo yet

We’ll see more examples of error messages later (and how to interpret
them), but hopefully the message:

``Error in print(Foo): object 'Foo' not found``

is clear enough. Because we were expecting this error message, we can
ignore it and move on.

data types
----------

So, we’ve created our first **object**, ``foo``. But what kind of object
is ``foo``? To find out, we can use the ``typeof()`` function
(`documentation <https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/typeof>`__):

.. code:: r

    typeof(foo) # use the typeof() function to find the type of an object

So ``foo`` is an object of type **character**, meaning that it is
*text*.

In general, **R** has the following basic data types:

-  **character**, for text objects
-  **numeric**, for numbers. These can be divided into the following:

   -  **double**, for floating-point (real) values
   -  **integer**, for integer values

-  **logical**, for boolean (True/False) objects
-  **complex**, for complex numbers

Let’s look at an example of a **numeric** object:

.. code:: r

    x <- 1 # assign a value of 1 to the object x
    typeof(x) # should be integer, right?

That’s interesting - even though we assigned an integer value to ``x``,
**R** has created an object of type **double**. This is because by
default, numeric values in **R** are type double.

To create an object with an **integer** value, we append an ``L`` to
each number (alternatively, we can *coerce* to the integer type using
the ``as.integer()`` function):

.. code:: r

    x <- 1L
    typeof(x)

We’ll come back to data types more as we work through the example
exercises.

data structures
---------------

Most of the time, we’ll want to use groups of data, or *data
structures*, rather than individual values. Just like with data types,
**R** has a number of different data structures, ranging from
one-dimensional to multi-dimensional structures.

vectors
~~~~~~~

A **vector** is the most basic data structure in **R** - it’s a
one-dimensional sequence of a single data type.

To assign a vector explicitly, we can use the function ``c()`` (short
for “combine”):

.. code:: r

    campuses <- c('Belfast', 'Coleraine', 'Jordanstown', 'Magee')
    print(campuses)

indexing
~~~~~~~~

To access the individual elements of a vector, we need to use the
**index** of that element, along with square brackets (``[`` and ``]``).

In the example above:

.. code:: r

   campuses <- c('Belfast', 'Coleraine', 'Jordanstown', 'Magee')

In **R**, the index of a vector starts at 1. “Coleraine” is the second
element in the ``campuses`` vector, which means that it has an index of
2. We can check this with the following cell:

.. code:: r

    campuses[2] # return the second element from the 'campuses' vector

We can also use logical expressions or variables to select values from a
**vector**:

.. code:: r

    numbers <- 1:10 # create a sequence of numbers from 1 to 10

    numbers[numbers > 5] # select the values of numbers that are greater than 5

factors
~~~~~~~

**factor**\ s are vectors for categorical variables, where we have a
limited number of unique character strings. As an example,

.. code:: r

    campus <- c("Belfast", "Coleraine", "Magee", "Magee", "Coleraine", "Coleraine", "Belfast", "Jordanstown")# create a vector
    campus <- factor(campus) # turn it into a factor

    print(campus) # examine the output

In the ouptut above, you can see that just like the **vector** example
above, the output shows the contents of the factor (the list of campus
names), but it also shows the **levels**: the unique categories of the
variable. We can also specify the **levels** when creating the factor,
which can help us order and sort the categories (for example, months);
it can also help us identify data entry errors like typos (e.g.,
``Coelraine`` instead of ``Coleraine``):

.. code:: r

    campus <- c("Belfast", "Coelraine", "Magee", "Magee", "Coleraine", "Coleraine", "Belfast", "Jordanstown")# create a vector
    campus <- factor(campus, levels=campuses) # specify the levels

    print(campus)

Note how the second entry in the **factor**, is now ``NA`` (for **Not
Available**), because ``Coelraine`` is not in our list of campuses.

lists
~~~~~

**factor** and **vector** objects don’t allow for mixing types - we
can’t have a **vector** with both character and numeric values, but we
can have a **vector** of character values and a **vector** of numeric
values.

If we want to mix data types, we can use a **list**:

.. code:: r

    a <- 1:5 # a sequence of numbers from 1 to 5
    b <- c('these', 'are', 'characters') # a vector of character strings
    c <- TRUE # a single boolean value

    mixed_bag <- list(item_1=a, item_b=b, item_iii=c) # join the different objects into a list. Note that we have to specify the names of the list variables

    print(mixed_bag)

Like with **vector** objects, we can select values/objects from the
**list** using the index:

.. code:: r

    mixed_bag[2] # select the second item in the list

Note that the type of this selection is *also* a **list**:

.. code:: r

    item2 <- mixed_bag[2] # select the second item in the list and assign to a new object
    typeof(item2) # get the type of the new object

In addition to using the **index**, we can select a single variable from
the **list** using the ``$`` operator:

.. code:: r

    mixed_bag$item_b # select the item_b variable from the mixed_bag list

When we select the variable this way, the resulting object is a
**vector**, not a **list** - so the way that we select values from these
data structures matters.

data frames
~~~~~~~~~~~

While a **list** object allows us to mix and nest variables of different
data types, it is one-dimensional - there is no association between the
values of the different variables, because they can have different
lengths.

A **data frame** (or ``data.frame``) is a two-dimensional object - like
a spreadsheet table. Each variable in a **data.frame** is a **vector**,
and each **vector** has the same length.

Most often, this is how we will end up working with data sets - we load
them from a file such as an Excel spreadsheet, CSV (comma-separated
variable), or SPSS file into a **data.frame**, then work with the
**data.frame** object. We can also create our own data frame using
**vector** objects:

.. code:: r

    name <- c('Belfast', 'Derry', 'Bangor', 'Lisburn', 'Newry', 'Armagh') # a vector of city names
    population <- c(345418, 83163, 61011, 45370, 27913, 14777) # a vector of populations corresponding to each city name

    cities <- data.frame(name, population) # create a data frame from these vectors

    print(cities)

Like **vector** and **list** objects, there are a number of ways to
select values from a **data.frame** - the next four examples show
different ways of selecting by index. Have a look at each of them in
turn - note that the resulting object changes depending on how we select
them!

.. code:: r

    cities[1] # this gives us the first column, as a data.frame

.. code:: r

    cities[, 1] # this also gives us the first column, but as a vector

.. code:: r

    cities[1, ] # this gives us the first row - note that this is also a data.frame!

.. code:: r

    cities[1, 2] # this gives us the entry in the first row, second column

We can also select variables in a **data.frame** by name, using the
variable name as a **character**:

.. code:: r

    cities['name'] # returns the 'name' variable as a 6 x 1 data.frame

Using the ``$`` operator, on the other hand, returns a **vector**, not a
**data.frame**:

.. code:: r

    cities$name # this is a vector with length 6

Like we saw with **vector** objects, we can select subsets of the table
using logical statements or variables - for example, by selecting all
cities where the population is greater than 50,000:

.. code:: r

    cities[cities$population > 50000,] # gives us all rows where the population variable is larger than 50000

To get the variable names for the **data.frame**, we use the ``names()``
(`documentation <https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/names>`__)
built-in function:

.. code:: r

    names(cities)

basic arithmetic
----------------

As you might guess, we will very often want to use **R** to perform
calculations on our data. In this section, we’ll see how **R** can be
used to perform basic arithmetic operations, and we’ll discuss the order
of operations - that is, the order in which arithmetic operations are
performed.

.. code:: r

    x <- 2
    y <- 3

    print(sprintf("x + y = %s", x + y)) # print the value of x+y (addition)
    print(sprintf("x - y = %s", x - y)) # print the value of x-y (subtraction)
    print(sprintf("x * y = %s", x * y)) # print the value of x*y (multiplication)
    print(sprintf("x / y = %s", x / y)) # print the value of x/y (division)
    print(sprintf("x ^ y = %s", x ^ y)) # print the value of x^y (exponentiation)
    print(sprintf("y %% x = %s", y %% x)) # print the value of x%%y (modular division)

**R**, like other programming languages, has an order of operator
precedence - that is, the order in which operators within the same
statement are executed. They are the same as the order of operations for
basic (non-computer) arithmetic:

-  Parentheses
-  Exponentials
-  Multiplication/Division
-  Addition/Subtraction

Before executing the following cell, think about what the output should
be. Run the cell - does this result match with your expectation?

.. code:: r

    2 * (3 + 4)^2 - 1

functions
---------

So far, we’ve used a number of base functions, such as ``c()``,
``print()``, ``typeof()``, and ``names()``. We can also define our own
functions to use. This has many benefits, including:

-  improved readability of code
-  eliminating repetitive code
-  allowing for easier debugging of a program/script
-  allowing us to re-use code in other programs/scripts

In **R**, we define a function using, oddly enough, the ``function()``
function
(`documentation <https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/function>`__),
and assigning the output to our new function:

.. code:: r


   new_function <- function(arguments) {
       # this is the body of the function - add instructions (code) here
       return(something) # if we want to get the output of the function, we have to return it
   }

The arguments to ``function()`` are the arguments that we want to pass
to our new function - in essence, these are the objects that we will use
in the function. After the call to ``function()``, we have a block of
code enclosed by curly brackets (``{`` and ``}``) - this is where the
instructions (code) that make up the function go. And finally, if we
want to get something back from our function, we need to ue the
``return()`` function. If we don’t do this, **R** will run the
instructions that make up the function, but it won’t give us any output.

To help illustrate this, let’s define a function for calculating the
area of a circle. Mathematically, this is a function of the radius of
the circle - equal to the constant pi multiplied by the radius squared.
Run the cell below to create the new function, and then test it:

.. code:: r

    circle.area <- function(radius) {
        area <- pi * radius ^ 2 # alternatively, radius * radius
        return(area) # use return() to get a value back from the function
    }

    circle.area(10) # get the area of a circle with radius 10 (should be 314.15 ...)

In the cell below, I’ve started two more functions for calculating the
surface area and volume of a sphere. For each function, fill in the code
that will return the correct result, then confirm that your function
output matches the values shown in the comment on each line.

.. code:: r

    sphere.area <- function(radius) {
        # your code goes here!
    }

    sphere.volume <- function(radius) {
        # your code goes here!
    }

    print(sphere.area(10)) # get the surface area of a sphere with radius 10 (should be 1256.637)
    print(sphere.volume(10)) # get the volume of a sphere with radius 10 (should be 4188.79)

In the exercises to come, we’ll define and use a number of other
functions.

control structures
------------------

Finally, we’ll have a look at how we can use **control structures** to
control when and how different parts of our code are executed.

-  **if**, **else** blocks, for executing code depending on different
   conditions
-  **while** loops, for repeating code while a certain condition is met
-  **for** loops, for repeating code a set number of times

The basic structure of the blocks is similar to what we saw with
functions - first, we have the control statement (**if**, **else**,
**while**, etc.), followed by a *condition*, and then the code to
execute if that condition is met, enclosed in curly brackets:

.. code:: r


   control (condition) {
       # the body of the control block
   }

comparison operators
~~~~~~~~~~~~~~~~~~~~

In order to use these control structures, however, we need a statement
that can be evaluated to be ``TRUE`` or ``FALSE`` - a **conditional**
statement. Most often, we do this using one of six basic **comparison**
operators:

-  ``==``: for testing whether the value of two objects are **equal** to
   each other
-  ``!=``: for testing whether the value of two objects are **not
   equal** to each other
-  ``<``: for testing whether the value of one object is **less than**
   the value of another object
-  ``<=``: for testing whether the value of one object is **less than or
   equal to** the value of another object
-  ``>``: for testing whether the value of one object is **greater
   than** the value of another object
-  ``>=``: for testing whether the value of one object is **greater than
   or equal to** the value of another object

These are not the only ways that we can write conditional statements,
but they are some of the most common, especially as we’re starting out.

if … else statements
~~~~~~~~~~~~~~~~~~~~

We’ll start with a very basic control structure: an **if** statement.
The code inside of the block is excecuted only if the condition is met -
if not, the script/program continues without running the code inside of
the block:

.. code:: r

    x <- 2

    if (x > 0) {
        print("x is a positive number")
    }

In the example above, the code inside of the block
(``print("x is a positive number")``) will only be executed if the
condition ``x > 0`` is met - if the value of ``x`` is less than zero,
nothing will happen (change the value of ``x`` in the cell above to see
for yourself!).

We may also want to provide alternatives, where two or more blocks of
code are executed depending on the evaulation of one or more conditional
statements. We’ll begin with the most basic, an **if … else** statement:

.. code:: r

    x <- -1

    if (x > 0) {
        print("x is a positive number")
    } else {
        print("x is less than or equal to 0")
    }

In an **if … else** statement, we start with the **if** statement.
Immediately after the **if** statement, we place the **else** statement.
The code in this block will only be executed if the **condition** is
``FALSE`` - if the **condition** is ``TRUE``, the code in the **if**
statement is executed, and the code in the **else** statement is
skipped.

We can also evaluate more than one condition, using an **else-if**
statement:

.. code:: r

    x <- 1

    if (x > 0) {
        print("x is a positive number")
    } else if (x == 0) {
        print("x is equal to 0")
    } else {
        print("x is a negative number")
    }

With an **else-if** statement, we can have as many conditional branches,
or cases, as we like. The **else** block at the end is optional, but it
has to come at the end. This is because only one of these blocks can be
executed - the block corresponding to the *first* condition that returns
``TRUE`` when evaluated.

while loops
~~~~~~~~~~~

A **while** loop is used to repeat a section of code, so long as a given
condition is met. At the beginning of each iteration of loop, the
interpreter checks the condition - if it is ``TRUE``, the code is
executed; if ``FALSE``, the code inside the loop is skipped.

When defining a **while** loop, it’s extremely important to remember to
provide some way for the condition to evaluate as ``FALSE`` - if the
condition is always ``TRUE``, the loop will never stop running (an
**infinite** loop). Most often, we can do this by updating the variable
that is evaluated in the condition, as seen in the example below:

.. code:: r

    n <- 10

    print("Countdown begins. Launch in ...")
    while (n > 0) {
        print(n)
        n <- n - 1 # subtract one from n
    }
    print("Blastoff!")

Here, the value of ``n`` changes each time the loop is run, so it will
(eventually) reach 0, and the loop will terminate.

for loops
~~~~~~~~~

A **for** loop is used to repeat code for a set number of repetitions -
for example, each value in a sequence or a **vector**. At the beginning
of the loop, the value of the **iterator** takes on the first value in
the sequence; when the program reaches the bottom of the loop, it
returns to the top and changes the value of the **iterator** to the next
value in the sequence. We can see this using our ``campus`` **vector**
from earlier:

.. code:: r

    campuses <- c('Belfast', 'Coleraine', 'Jordanstown', 'Magee')

    # loop over all of the values in campuses
    for (campus in campuses) {
        print(campus) # print the campus name
    }

We can also combine control structures - for example, by including an
**if … else** statement inside of a **for** loop:

.. code:: r

    campuses <- c('Belfast', 'Coleraine', 'Jordanstown', 'Magee')

    # loop over all of the values in campuses
    for (campus in campuses) {
        if (campus == 'Coleraine') {
            # if the value of campus equals 'Coleraine', end the loop
            break # break
        } else {
            print(campus) # print the campus name
        }
    }

The ``break`` statement statement is used to “break out” of a **for**
loop - once a condition is met that causes it to be executed, the loop
is terminated and the program continues running from there.

recap
-----

That’s all for this exercise. In this lesson, we have introduced the
following concepts:

-  variables, objects, values, and assignment
-  data types
-  data structures:

   -  vectors
   -  lists
   -  data frames

-  indexing
-  arithmetic operations
-  functions
-  flow control using logic

Next, we’ll put some of this to work by having a look at a broken
program, and see if we can manage to fix it.
