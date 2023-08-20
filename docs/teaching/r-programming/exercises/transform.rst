transforming data
===================

.. note::

    This is a **non-interactive** version of the exercise. If you want to run through the steps yourself and see the
    outputs, you'll need to follow the setup steps and work through the notebook on your own computer.

In this lesson, we’re going to learn how we can work with datasets -
combining tables, creating and re-arranging variables, selecting and
sorting rows, and grouping and summarizing data. Mostly, we will be
using functions from the ``dplyr`` package, which is designed for data
manipulation (again, read this as “analyzing” or “working with”, not
“fabricating”!).

data
----

The data used in this exercise are the historic meteorological
observations from the `Armagh
Observatory <https://www.metoffice.gov.uk/weather/learn-about/how-forecasts-are-made/observations/recording-observations-for-over-100-years>`__
(1853-present), the Oxford Observatory (1853-present), the Southampton
Observatory (1855-2000), and Stornoway Airport (1873-present),
downloaded from the `UK Met
Office <https://www.metoffice.gov.uk/research/climate/maps-and-data/historic-station-data>`__.

Like with the Armagh dataset we used previously, I have done the
following to make the data slightly easier to work with: - Removed the
header on lines 1-5 - Replaced multiple spaces with a single space, and
replaced single spaces with a comma (``,``) - Removed ``---`` to
indicate no data, leaving these fields blank - Removed ``*`` indicating
provisional/estimated values - Removed the 2023 data - Renamed the file
(e.g., ``oxforddata.txt`` -> ``oxforddata.csv``).

If you wish to use your own data (and there are loads of stations
available!), please feel free. For the best experience, you will likely
need to repeat the steps indicated above.

loading libraries
-----------------

As before, we load the libraries that we will use in the exercise at the
beginning. We will be using three libraries: -
`readr <https://readr.tidyverse.org/>`__, for reading the data from a
file; - `ggplot2 <https://ggplot2.tidyverse.org/>`__, for plotting the
data; - and `dplyr <https://dplyr.tidyverse.org/>`__, for
transforming/manipulating the data.

.. code:: r

    library(readr) # this loads the functions we'll use to load the data
    library(ggplot2) # this loads the functions, etc. needed for us to plot
    library(dplyr) # this loads the functions, etc. needed for us to work with the data

loading the data
----------------

In this exercise, we’re going to see a number of different ways that we
can work with data tables. Before we get to this, however, we need to
load the individual data files and combine them into a single data
table.

Rather than loading all four at once and then combining them, however,
we can simplify this slightly using a **for** loop. First, we’ll load
the Armagh Observatory data, because it’s currently in a different
folder.

Rather than typing the path to the file directly, we can use
``file.path()``
(`documentation <https://rdrr.io/r/base/file.path.html>`__) to construct
a path in a *platform-independent* way. In general, we want to do this
because Windows uses ``\`` to separate folders, while Unix-style systems
such as Linux and MacOS use ``/`` - this way, we don’t run into issues
if we share our code with people working on different systems.

To construct the filename, we’re using a `relative
path <https://en.wikipedia.org/wiki/Path_(computing)#Absolute_and_relative_paths>`__
- that is, it is *relative* to some given working directory (typically
the current working directory). To get to **armaghdata.csv** from the
current directory, we have to go up a directory level (``..``), before
entering the **03.plotting** directory, and the **data** directory after
that:

.. code:: r

    station_data <- read_csv(file.path('..', '03.plotting', 'data', 'armaghdata.csv')) # use file.path to construct a path to the data file

Next, we want to make sure that we can keep track of which observation
comes from which station - so, we should add a ``station`` variable to
the table, and make sure to specify that these observations all come
from the Armagh Observatory:

.. code:: r

    station_data$station <- 'armagh' # add the station name as a column

Now, we can set up a loop to load the other 3 stations data. First, we
can create a **vector** of station names:

.. code:: r

    # create a vector of station names
    new_stations <- c('oxford', 'southampton', 'stornoway')

Now that we have the vector of station names, we can construct the
**for** loop to first read each file:

.. code:: r

       fn_data <- file.path('data', paste(station, 'data.csv', sep="")

Here, we first use ``paste()`` to combine the ``station`` variable
(which takes on a value from the ``new_stations`` **vector** on each
pass through the loop) with ``'data.csv'``, using a separator (``sep``)
value of ``""`` so that the resulting file names will be
``'oxforddata.csv'``, ``'southamptondata.csv'``, and
``'stornowaydata.csv'``. We then use ``file.path()`` to combine this
with the ``'data'`` directory name, so that the value of ``fn_data`` is
the complete relative path to each file.

Next, we use ``read_csv()`` to read in the file, and add a ``station``
variable to the table, just like we did with the Armagh data.

Finally, we use ``bind_rows()``
(`documentation <https://dplyr.tidyverse.org/reference/bind_rows.html>`__)
to combine the existing table, ``station_data``, with the newly loaded
table (``data``), and overwrite the value of ``station_data`` with this
combined table:

.. code:: r

       station_data <- bind_rows(station_data, data)

Each time through the **for** loop, the value of ``station`` is updated:

.. code:: r

    for (station in new_stations) {
        fn_data <- file.path('data', paste(station, 'data.csv', sep="")) # create the filename for each csv file, using file.path and paste
        data <- read_csv(fn_data) # read the csv
        data$station <- station # add the station to the table

        station_data <- bind_rows(station_data, data) # combine the new data with the current data table
    }

    print(station_data) # show the data

Note that this is one advantage of using clear, consistent naming and
formatting for data files - we can easily write a loop to load multiple
files, instead of having to write individual paths.

using filter() to select rows
-----------------------------

Now that we have a single table, we can also look at ways that we can
select rows from the table. We have alread seen an example of this - for
example, we could select all observations where the monthly maximum
temperature (``tmax``) is greater than 20°C:

.. code:: r

    station_data[station_data$tmax > 20, ]

However, there’s a small problem with this. In the example above, you
can see that there are a number of rows where the values are all ``NA``
- this is because of how **R** handles NA values with the *extraction
operators* (``[]``). Rows where ``tmax`` is missing (the value is
``NA``) also show up, because a comparison operator with ``NA`` returns
``NA``, **not** ``TRUE``/``FALSE``:

.. code:: r

    station_data$tmax > 20

When we then use this **vector** to *index* the **tibble**, the
corresponding rows are filled with ``NA`` values due to something called
*vector recycling* (see
`here <https://homerhanumat.github.io/r-notes/vector-recycling.html>`__
for more information if you’re interested).

We could write a combined conditional expression to select the correct
rows:

.. code:: r

    (station_data$tmax > 20) & (!is.na(station_data$tmax))

Here, the conditional is ``TRUE`` only when ``tmax > 20`` **and**
``tmax`` is not ``NA``. However, there is an easier, clearer way, using
``dplyr::filter()``
(`documentation <https://dplyr.tidyverse.org/reference/filter.html>`__):

.. code:: r

    station_data |> filter(tmax > 20) # use filter to select rows where tmax > 20

Here, we’re using an operator we haven’t seen before: the ``|>``
(“pipe”) operator.

In brief, ``|>`` tells **R** to take the output of the thing on the
left, and pass it to the function call on the right. Thinking about this
mathematically, ``x |> f(y)`` is equivalent to ``f(x, y)``. We can also
use this to combine multiple function calls - so, ``x |> f(y) |> g(z)``
is equivalent to ``g(f(x, y), z)``, and so on.

So, this:

.. code:: r

    station_data |> filter(tmax > 20) # use filter to select rows where tmax > 20

Is the same as this:

.. code:: r

    filter(station_data, tmax > 20) # use filter to select rows where tmax > 20

With only one function call, the difference may not seem like much - as
we will see, the real power comes when we are combining many function
calls together.

We can also use ``filter()`` with combined conditionals - for example,
to select all monthly observations where ``tmax`` is greater than 20°C
and ``rain`` is greater than 100 mm:

.. code:: r

    station_data |> filter(tmax > 20 & rain > 100) # use filter to select rows where tmax > 20 and rain > 100

using arrange() to sort rows
----------------------------

Sometimes, we might want to sort our data according to the value of
different variables. For example, we can sort the observations by
rainfall, from smallest to largest values:

.. code:: r

    station_data |> arrange(rain) # sort by rainfall, from smallest to largest values

By default, the values are sorted in *ascending* order (from smallest to
largest, or from A to Z for characters). If we want to see the reverse,
we can use ``desc()``
(`documentation <https://dplyr.tidyverse.org/reference/desc.html>`__):

.. code:: r

    station_data |> arrange(desc(rain)) # sort by rainfall, from largest to smallest values

We can also combine different variables to sort by - for example,
sorting by ``season`` and ``rainfall``:

.. code:: r

    station_data |> arrange(season, desc(rain)) # sort by season, then rainfall in descending order

using distinct() to find unique rows
------------------------------------

To find unique rows in the dataset, we can use ``distinct()``
(`documentation <https://dplyr.tidyverse.org/reference/distinct.html>`__).
By itself, ``distinct()`` uses all of the variables to determine whether
rows are distinct; most of the time, we likely want to use it to find
unique values of a given variable:

.. code:: r

    station_data |> distinct(station) # find distinct values of station names

We can also use it to find combinations of variables:

.. code:: r

    station_data |> distinct(station, mm) # find distinct pairs of station and month values

We can also use the ``.keep_all`` argument to keep the other columns
while filtering for unique rows:

.. code:: r

    station_data |> distinct(station, mm, .keep_all = TRUE) # keep all columns while finding distinct pairs of station and season values

Note that the distinct values found above are all from the first year of
each dataset - this is because ``distinct()`` discards all but the first
occurrence of a unique row.

counting occurrences with count()
---------------------------------

If we want to count the number times a particular value occurs in the
table, we can use ``count()``
(`documentation <https://dplyr.tidyverse.org/reference/count.html>`__).
We can also use this in combination with other functions - for example,
we can count the number of times each station observed rainfall greater
than 150 mm in a month by first using ``filter()`` to select all rows
where ``rain`` is greater than 150, then use ``count()`` to count the
number of unique occurrences of ``station`` in the resulting table:

.. code:: r

    station_data |> filter(rain > 150) |> count(station, sort = TRUE) # select all rows where rain > 150, then count the number of occurrence of station, sorted in descending order

From this, we can quickly see that Stornoway Airport, located in the
Outer Hebrides, has far more months with heavy rainfall (278) than any
other station in our dataset; by contrast, Oxford has only recorded 12
such months between 1853 and 2022.

adding variables to the table using mutate()
--------------------------------------------

In a previous exercise, we saw how we can use **R**\ ’s built-in
functionality to add variables to a data frame:

.. code:: r

       armagh$date <- as.Date(paste(armagh$yyyy, armagh$mm, "1", sep="/"), format="%Y/%m/%d")

We can also use ``mutate()``
(`documentation <https://dplyr.tidyverse.org/reference/mutate.html>`__).
This is more flexible than the built-in functionality, because it also
allows us to add more than one new variable, and it allows us to specify
where to put the new variables(s) using the ``.before`` or ``.after``
arguments. For example, to place the new ``date`` variable on the
left-hand side of the column, we can use ``.before = 1``:

.. code:: r

    station_data |> mutate(date = as.Date(paste(yyyy, mm, "1", sep = "/"), format = "%Y/%m/%d"), .before = 1) # use mutate to add a date variable, before the other variables

Note that we haven’t assigned the output, so ``station_data`` is
unchanged, and the new variable is only printed. We may want to
overwrite our existing data by assigning the output to the same
**object**, or we may want to create a new **object** with the output.
Ultimately, the choice depends on what we’re planning to do.

We can also use ``mutate()`` to add multiple variables to the table -
for example, adding the ``season`` and ``date`` variables as we saw
previously:

.. code:: r

    station_data <- station_data |> mutate(
        season = case_when(
            mm %in% c(1, 2, 12) ~ 'winter', # if month is 1, 2, or 12, set it to winter
            mm %in% 3:5 ~ 'spring', # if month is 3, 4, 5, set it to spring
            mm %in% 6:8 ~ 'summer', # if month is 6, 7, 8, set it to summer
            mm %in% 9:11 ~ 'autumn', # if month is 9, 10, 11, set it to autumn
        ),
        date = as.Date(paste(yyyy, mm, "1", sep="/"), format="%Y/%m/%d") # add a date variable
    )

    print(station_data)

By default, ``mutate()`` adds variables to the right hand side of the
table; in addition to specifying where to put them using ``.before`` and
``.after``, we will also see how we can re-arrange the variables in the
table later on.

using select() to select columns
--------------------------------

Sometimes, we might want to select a single variable, or a handful of
variables from a table - we can do this using ``select()``
(`documentation <https://dplyr.tidyverse.org/reference/select.html>`__):

.. code:: r

    station_data |> select(date, tmax, station) # select only the date, tmax, and station variables

We can also select a subset using a range of columns:

.. code:: r

    station_data |> select(tmax:sun) # select columns between tmax and sun (inclusive)

and we can also select a subset by specifying which columns not to use:

.. code:: r

    station_data |> select(!tmax:sun) # select columns except those between tmax and sun (inclusive)

And, we can also select columns by their type using ``where()``
(`documentation <https://tidyselect.r-lib.org/reference/where.html>`__).
For example, to select only variables that are **numeric**, we can use
the ``is.numeric()`` function
(`documentation <https://rdrr.io/r/base/numeric.html>`__):

.. code:: r

    station_data |> select(where(is.numeric)) # select only numeric variables

using rename() to rename columns
--------------------------------

Often, we may also want to rename variables to make them easier to
read/understand. For example, the ``yyyy``, ``mm``, and ``af`` variables
in our table are not necessarily the easiest to understand. We can
rename them to more clear names, such as ``year``, ``month``, and
``air_frost``, using the ``rename()`` function
(`documentation <https://dplyr.tidyverse.org/reference/rename.html>`__):

.. code:: r

    station_data <- station_data |> rename(year = yyyy, month = mm, air_frost = af) # rename yyyy to year, mm to month, and af to air_frost

    print(station_data)

using relocate() to move columns
--------------------------------

With ``mutate()``, we saw how we can specify where to put new variables,
using the ``.before`` and ``.after`` arguments. If we aren’t creating
new variables, we can still re-arrange variables using ``relocate()``
(`documentation <https://dplyr.tidyverse.org/reference/relocate.html>`__),
which works in much the same way. We can specify which column to move a
variable ``.before`` or ``.after``; like with ``select()``, we can also
move a range or selection of columns at once. In the cell below, we’re
going to first move ``date`` so that it is the first column (before
``year``); then, we move ``season`` so that it comes after ``month``:

.. code:: r

    station_data |>
        relocate(date, .before = year) |>  # move date to before year
        relocate(season, .after = month) -> # move season to be after month
    station_data # use the -> assignment operator to assign the output to station_data

    print(station_data)

In the cell above, note that we have used ``->`` (the **right-hand
assignment operator**) to assign the ouput of the second ``relocate()``
function to the object ``station_data``. Unlike the expression operator
we have used so far (``<-``, the **left-hand assignment operator**),
``->`` assigns the value of the expression on the left side of the
operator, and assigns it to the object on the *right-hand* side.

Normally, we tend to use ``<-``, but sometimes, especially with long
“sentences” with multiple function calls, it can make sense to use
``->`` at the end, rather than the beginning - the end result will be
the same.

saving data to a file
---------------------

Finally, let’s save our cleaned, re-arranged dataset to a file, using
``write_csv()``
(`documentation <https://readr.tidyverse.org/reference/write_delim.html>`__).
In the simplest case, ``write_csv()`` takes two arguments: first, the
data table to be written to disk, and second, the filename to write the
data to. We’ll save our file to the ``'data'`` folder, with a filename
of **combined_stations.csv**:

.. code:: r

    write_csv(station_data, file.path('data', 'combined_stations.csv')) # write station_data to a file in the data folder

Now, we’ll be able to load this file when we want to do further
analysis, rather than needing to re-run the steps to load each file,
combine the tables, create new variables, and so on. We’re continuing to
use a **comma-separated variable** (**.csv**) file format, though there
are a number of different format options available - for more
information, check the
`documentation <https://readr.tidyverse.org/reference/write_delim.html>`__.

grouping data
-------------

Next, we’ll see how we can use different tools to aggregate and
summarize our data, starting with ``group_by()``
(`documentation <https://dplyr.tidyverse.org/reference/group_by.html>`__).
To start, we’ll group the data by ``station``:

.. code:: r

    station_data |> group_by(station) # group the data by station

This looks largely the same as the previous output, with one important
distinction: this is now a **grouped_df**, rather than a **spec_tbl_df**
- this means that when we call the ``summarize()``
(`documentation <https://dplyr.tidyverse.org/reference/summarise.html>`__)
function on the output, the summary is calculated based on each *group*,
rather than all values of the variable. For example, if we want to
calculate the mean of ``tmax`` for each station:

.. code:: r

    station_data |>
        group_by(station) |> # group the data by station
        summarize(
            tmax = mean(tmax, na.rm = TRUE) # calculate the mean of tmax, ignoring NA values
        )

We can also group based on multiple variables - for example, by both
``station`` and ``season``:

.. code:: r

    station_data |>
        group_by(station, season) |> # group the data by station, then season
        summarize(
            tmax = mean(tmax, na.rm = TRUE), # calculate the mean of tmax, ignoring NA values
            rain = mean(rain, na.rm = TRUE)  # calculate the mean of rain, ignoring NA values
        )

Now, let’s combine this with what we learned in the previous lesson (the
plotting exercise) to create a plot that shows the distribution of
rainfall by season, separated by station.

First, we want to create a plot that shows the density distribution of
rainfall for each season, using ``facet_wrap()`` to create a single
panel for each station:

.. code:: r

    ggplot(data=station_data, mapping=aes(x=rain)) + # create a plot with tmax on the x-axis, colored by season
        geom_density(mapping=aes(color=season, fill=season), alpha=0.4, linewidth=1) + # add a density plot with transparency of 0.4 and lines of width 1
        facet_wrap(~station) -> # create one panel for each station
    rain_plot # assign the plot to a variable

    rain_plot

Next, we can use ``group_by()`` and ``summarize()`` to calculate the
mean rainfall for each station, and assign this to a new object,
``mean_values``:

.. code:: r

    mean_values <- station_data |>
        group_by(station) |> # group by station value
        summarize(rain = mean(rain, na.rm = TRUE)) # calculate the mean of rain, ignoring NA values

Now, to add a vertical line to our plot, we use ``geom_vline()``
(`documentation <https://ggplot2.tidyverse.org/reference/geom_abline.html>`__),
along with ``mean_values``, to place a vertical line in each panel where
the mean rainfall value is:

.. code:: r

    rain_plot <- rain_plot +
        geom_vline(data = mean_values, mapping = aes(xintercept = rain), linewidth = 1, linetype = 'dashed') # add dashed vertical lines at the mean rainfall value

    rain_plot

In the next panel, write some lines of code to change the axes labels
and increase the font size for the tick labels, axis labels, and panel
labels.

.. code:: r

    # your code goes here!

Now that you have finished the plot, be sure to save it to a file:

.. code:: r

    ggsave('seasonal_rain_distribution.png', plot=rain_plot) # save the plot to a file

slicing the dataset
-------------------

We’ll finish up by looking at a few functions that we can use to *slice*
a dataset - that is, extract specific rows from a group. For example, we
can combine ``group_by()`` and ``slice_max()``
(`documentation <https://dplyr.tidyverse.org/reference/slice.html>`__)
to find the maximum monthly temperature from each season:

.. code:: r

    station_data |>
        group_by(season) |>
        slice_max(tmax, n=1) # take the top n rows based on the value of tmax

This lets us quickly see the observations corresponding to the highest
temperature in each season - split between Southampton for autumn and
spring, and Oxford for summer and winter. If we want to select the
minimum, we can use ``slice_min()``:

.. code:: r

    station_data |>
        group_by(season) |>
        slice_min(tmax, n=1) # take the bottom n rows based on the value of tmax

Here, you can also see that by default, ``slice_min()`` (and
``slice_max()``) keep tied values - so we end up with 6 rows instead of
4. If we want to discard ties, we can use the ``.with_ties`` argument
set to ``FALSE``.

If we only want the first or last row from a group, regardless of the
value, we can use ``slice_head()`` to select the first n rows, and
``slice_tail()`` to select the last n rows:

.. code:: r

    station_data |>
        group_by(season) |>
        slice_head(n=1) # take the first n rows

Finally, we can select a random sample from each group using
``slice_sample()``:

.. code:: r

    station_data |>
        group_by(season) |>
        slice_sample(n=5) # take a random sample of 5 rows from each season

exercise and next steps
-----------------------

That’s all for this exercise. To practice your skills, create a notebook
file that does the following:

-  loads the libraries that you need
-  loads the saved data file (**combined_stations.csv**)
-  helps you answer the following questions:

   -  what station has the highest recorded rainfall in the dataset, and
      on what date?
   -  what season has the lowest average rainfall for each station?
   -  what year saw the most total rainfall, using data from all four
      stations?
   -  what is the lowest average annual temperature in the dataset, as
      measured by one station?

For a bonus, try downloading an additional dataset from the `Met
Office <https://www.metoffice.gov.uk/research/climate/maps-and-data/historic-station-data>`__,
saving it to the **data** folder. Next, open a **Terminal** and enter
the following:

.. code-block:: text

       python convert_metoffice.py data/{station}

remembering to replace ``{station}`` with the name of the file that you
just downloaded (e.g., ``durhamdata.txt``). This will convert the
``.txt`` file into a ``.csv`` file, using the steps outlined at the top
of the exercise. In your new notebook file, remember to add this new
data to your existing dataset (and re-save the file!), then repeat the
analysis above.
