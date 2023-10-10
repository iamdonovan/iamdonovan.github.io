working with pandas dataframes
==============================

.. note::

    This is a **non-interactive** version of the exercise. If you want to run through the steps yourself and see the
    outputs, you'll need to do one of the following:

    - follow the setup steps and work through the notebook on your own computer
    - open the workshop materials on `binder <https://mybinder.org/v2/gh/iamdonovan/intro-to-python/HEAD>`__ and work
      through them online
    - open a python console, copy the lines of code here, and paste them into the console to run them

In this lesson, we’re going to learn how we can work with datasets -
combining tables, creating and re-arranging variables, selecting and
sorting rows, and grouping and summarizing data. Mostly, we will be
working with ``pandas``, which is designed for data manipulation (again,
read this as “analyzing” or “working with”, not “fabricating”!).

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
available!), please feel free. I have also included a script,
``convert_metoffice.py`` (in the ``scripts/`` folder), that will do
these steps automatically. All you need to do is run the following from
a terminal:

::

       convert_metoffice.py {station}data.txt

This will create a new file, ``{station}data.csv``, that has converted +
cleaned the data into a CSV format that can easily be read by
``pandas``.

loading libraries
-----------------

As before, we load the libraries that we will use in the exercise at the
beginning. We will be using three libraries: -
`pandas <https://pandas.pydata.org/>`__, for reading the data from a
file; - `seaborn <https://seaborn.pydata.org/>`__, for plotting the
data; - `pathlib <https://docs.python.org/3/library/pathlib.html>`__,
for working with filesystem paths;

As before, we’re going to *alias* ``pandas`` as ``pd`` and ``seaborn``
as ``sns``. We only want the ``Path`` **sub-package** from ``pathlib``,
so we use ``from`` to specify this:

.. code:: ipython3

    import pandas as pd
    import seaborn as sns
    from pathlib import Path

In this exercise, we’re going to see a number of different ways that we
can work with data tables. Before we get to this, however, we need to
load the individual data files and combine them into a single data
table.

Rather than loading all four at once and then combining them, however,
we can simplify this slightly using a **for** loop. First, we’ll load
the Armagh Observatory data, because it’s currently in a different
folder.

Rather than typing the path to the file directly, we can use
``pathlib.Path``
(`documentation <https://docs.python.org/3/library/pathlib.html#pathlib.Path>`__)
to construct a path in a *platform-independent* way. In general, we want
to do this because Windows uses ``\`` to separate folders, while
Unix-style systems such as Linux and MacOS use ``/`` - this way, we
don’t run into issues if we share our code with people working on
different systems.

To construct the filename, we’re using a `relative
path <https://en.wikipedia.org/wiki/Path_(computing)#Absolute_and_relative_paths>`__
- that is, it is *relative* to some given working directory (typically
the current working directory). To get to **armaghdata.csv** from the
current directory, we have to go up a directory level (``..``), before
entering the **03.plotting** directory, and the **data** directory after
that:

.. code:: ipython3

    station_data = pd.read_csv(Path('..', '03.plotting', 'data', 'armaghdata.csv')) # use file.path to construct a path to the data file

Next, we want to make sure that we can keep track of which observation
comes from which station - so, we should add a ``station`` variable to
the table, and make sure to specify that these observations all come
from the Armagh Observatory:

.. code:: ipython3

    station_data['station'] = 'armagh' # add the station name as a column

Now, we can set up a loop to load the other 3 stations data. First, we
can create a **list** of station names:

.. code:: ipython3

    # create a list of station names
    new_stations = ['oxford', 'southampton', 'stornoway']

Now that we have the vector of station names, we can construct the
**for** loop to first read each file:

.. code:: python

       fn_data = Path('data', f"{station}data.csv")

Here, we use an **f-string** to combine the ``station`` variable (which
takes on a value from the ``new_stations`` **list** on each pass through
the loop) with ``'data.csv'``, so that the resulting file names will be
``'oxforddata.csv'``, ``'southamptondata.csv'``, and
``'stornowaydata.csv'``. We then use ``Path()`` to combine this with the
``'data'`` directory name, so that the value of ``fn_data`` is the
complete relative path to each file.

Next, we use ``pd.read_csv()`` to read in the file, and add a
``station`` variable to the table, just like we did with the Armagh
data.

Finally, we use ``pd.concat()``
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.concat.html>`__)
to combine the existing table, ``station_data``, with the newly loaded
table (``data``), and overwrite the value of ``station_data`` with this
combined table:

.. code:: python

       station_data = pd.concat([station_data, data], ignore_index=True)

Each time through the **for** loop, the value of ``station`` is updated:

.. code:: ipython3

    for station in new_stations:
        fn_data = Path('data', f"{station}data.csv") # create the filename for each csv file, using file.path and paste
        data = pd.read_csv(fn_data) # read the csv
        data['station'] = station # add the station to the table

        station_data = pd.concat([station_data, data], ignore_index=True) # combine the new data with the current data table

    print(station_data) # show the data

Note that this is one advantage of using clear, consistent naming and
formatting for data files - we can easily write a loop to load multiple
files, instead of having to write individual paths.

selecting rows using expressions
--------------------------------

Now that we have a single table, we can also look at ways that we can
select rows from the table. For a *very* in-depth overview of how
indexing and slicing works with ``pandas``, see this
`guide <https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html>`__.

We have alread seen an example of this - for example, we could select
all observations where the monthly maximum temperature (``tmax``) is
greater than 20°C by using ``.loc`` and a conditional statement:

.. code:: ipython3

    station_data.loc[station_data['tmax'] > 20]

If we want to use multiple conditions - for example, all observations
where the monthly maximum temperature is greater than 20°C, and the
monthly rainfall is grater than 100 mm, we can’t simply use the ``&``
operator with the two statements:

.. code:: ipython3

    station_data.loc[station_data['tmax'] > 20 & station_data['rain'] > 100] # this won't work to combine conditions

Instead, we have to surround each condition with parentheses first:

.. code:: ipython3

    station_data.loc[(station_data['tmax'] > 20) & (station_data['rain'] > 100)] # this will work to select tmax > 20 and rain > 100

Alternatively, we can also use the ``.query()`` method
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.query.html>`__),
which allows us to write slightly more natural expressions. The
selection above using ``.query()`` looks like this:

.. code:: ipython3

    station_data.query('tmax > 20 & rain > 100') # use query to select rows where tmax > 20 and rain > 100

We can also use variables in the query - we just need to prefix them
with ``@``:

.. code:: ipython3

    min_temp = 20 # create a new variable with a value of 20

    station_data.query('tmax > @min_temp & rain > 100') # reference the new variable in the query

using sort_values to sort rows
------------------------------

Sometimes, we might want to sort our data according to the value of
different variables. For example, we can sort the observations by
rainfall, from smallest to largest values, using ``.sort_values()``
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sort_values.html>`__):

.. code:: ipython3

    station_data.sort_values('rain') # sort by rainfall, from smallest to largest values

By default, the values are sorted in *ascending* order (from smallest to
largest, or from A to Z for characters). If we want to see the reverse,
we can set the ``ascending`` keyword argument to ``False``:

.. code:: ipython3

    station_data.sort_values('rain', ascending=False) # sort by rainfall, from largest to smallest values

Note that in both cases, ``NaN`` values come at the bottom - because
they are not numbers, they are not sorted as being greater than or less
than other values, so ``pandas`` moves them to the end by default (to
put them at the beginning, we can use the ``na_position`` argument).

find unique values
------------------

To find unique rows in a **Series** (column), we can use ``.unique()``
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.unique.html>`__).
For example, we can find the unique values of the ``station`` variable:

.. code:: ipython3

    station_data['station'].unique() # find unique values of station

We can also ``.drop_duplicates()``
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.drop_duplicates.html>`__)
to find only unique rows in a **DataFrame**. With the ``subset``
argument, we can choose which columns to use in determining whether rows
are unique/duplicated:

.. code:: ipython3

    station_data.drop_duplicates(subset='station') # find rows based on unique values of station

We can also use it to find combinations of variables:

.. code:: ipython3

    station_data.drop_duplicates(subset=['station', 'mm']) # find rows with unique station/month pairs

Note that the distinct values found above are all from the first year of
each dataset - this is because ``.drop_duplicates()`` discards all but
the first occurrence of a unique row.

counting occurrences
--------------------

If we want to count the number of non-NaN values in a table, we can use
``.count()``
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.count.html>`__):

.. code:: ipython3

    station_data.count() # count the number of non-nan values in each column

If we want to find the frequency of each distinct row in a
**DataFrame**, we can use ``.value_counts()``
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.value_counts.html>`__).
By itself, this looks at all columns in a row to determine whether or
not the row is unique. More often, we will probably want to specify
which columns to use with the ``subset`` argument.

For example, we can count the number of times each station observed
rainfall greater than 150 mm in a month by first using ``query()`` to
select all rows where ``rain`` is greater than 150, then use
``value_counts()`` with the ``subset`` argument to count the number of
unique occurrences of ``station`` in the resulting table:

.. code:: ipython3

    station_data \
        .query('rain > 150') \
        .value_counts(subset='station')

From this, we can quickly see that Stornoway Airport, located in the
Outer Hebrides, has far more months with heavy rainfall (278) than any
other station in our dataset; by contrast, Oxford has only recorded 12
such months between 1853 and 2022.

Note that in this cell, we’re also using the **line break** character,
``\``, to split the call across multiple lines to help with readability.
As far as python is concerned, there is no difference between this:

.. code:: python

   station_data \
       .query('rain > 150') \
       .value_counts(subset='station')

and this:

.. code:: python

   station_data.query('rain > 150').value_counts(subset='station')

But, the former can be easier to read/understand what is being done. You
will likely see code written in both styles, but I will try to break
things into different lines when it makes sense.

adding columns to the table
---------------------------

In a previous exercise, we saw how we can add a variable/column to a
**DataFrame** using the output of a function:

.. code:: ipython3

    station_data['date'] = pd.to_datetime({'year': station_data['yyyy'], 'month': station_data['mm'], 'day': 1})

And, we saw how we could assign values to a column based on the values
in other columns:

.. code:: python

   station_data['season'] = '' # initialize an empty string column
   station_data.loc[station_data['mm'].isin([1, 2, 12]), 'season'] = 'winter' # if month is 1, 2, or 12, set season to winter
   station_data.loc[station_data['mm'].isin(range(3, 6)), 'season'] = 'spring' # if month is 3, 4, or 5, set season to spring
   station_data.loc[station_data['mm'].isin(range(6, 9)), 'season'] = 'summer' # if month is 6, 7, or 8, set season to summer
   station_data.loc[station_data['mm'].isin(range(9, 12)), 'season'] = 'autumn' # if month is 9, 10, or 11, set season to autumn

Now, let’s look at another way that we can accomplish the same thing, in
a slightly more “`pythonic <https://stackoverflow.com/a/25011492>`__”
way, by using some of the features of the language.

First, we’ll use ``range()``
(`documentation <https://docs.python.org/3/library/functions.html#func-range>`__)
to get a list of numbers from 1 to 12, corresponding to the months of
the year:

.. code:: ipython3

    months = range(1, 13) # get a list of numbers from 1 to 12

Next, we’ll use list multiplication and addition to create a list of the
season names for each month:

.. code:: ipython3

    seasons = ['winter'] * 2 + ['spring'] * 3 + ['summer'] * 3 + ['autumn'] * 3 + ['winter']

    seasons # show the list of season names for each month

We could, of course, have written this out explicitly:

.. code:: python

   seasons = ['winter', 'winter', 'spring', 'spring', 'spring', 'summer', 'summer', 'summer', 'autumn', 'autumn', 'autumn', 'winter']

Instead, we have used the fact that multiplying a **list** by an integer
repeats the **list**, and adding **list**\ s together *concatenates*
them, to simplify this (and also to remind you of these properties of
**list**\ s).

Next, we can create a **dict()** using ``zip()``
(`documentation <https://docs.python.org/3/library/functions.html#zip>`__)
to create pairs of month number/season name values:

.. code:: ipython3

    dict(zip(months, seasons)) # create a dict() of month/season pairs

Finally, we will use ``.map()``
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.map.html>`__)
to assign season names to each row, based on the value of ``mm`` (the
month number):

.. code:: ipython3

    station_data['season'] = station_data['mm'].map(dict(zip(months, seasons)))

    station_data.head(n=12) # show the first 12 rows of the table

re-naming columns
-----------------

Often, we may also want to rename variables to make them easier to
read/understand. For example, the ``yyyy``, ``mm``, and ``af`` variables
in our table are not necessarily the easiest to understand. We can
rename them to more clear names, such as ``year``, ``month``, and
``air_frost``, using the ``.rename()`` method
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.rename.html>`__).

To make it clear that we are renaming the columns, we’ll use the
``columns`` argument, passing a ``dict()`` of old/new names. We also
want this change to happen “in place”, meaning that it should update the
column names of the existing **DataFrame**, rather than returning a new
**DataFrame**:

.. code:: ipython3

    station_data.rename(columns={'yyyy': 'year', 'mm': 'month', 'af': 'air_frost'}, # rename columns using old/new name pairs
                        inplace=True # update the values of this dataframe, not return a new one
                       )

    station_data.head(n=5) # show the first 5 rows of the dataframe

Many of the methods that we are working with in this exercise have an
``inplace`` argument - by default, ``pandas`` assumes that you don’t
want to overwrite the existing **DataFrame** object with these changes.
If we don’t use the ``inplace`` argument, we need to assign the output
to a new variable in order to use it; for example:

.. code:: python

   new_df = old_df.rename(columns={'old_name': 'new_name'})

selecting columns
-----------------

Selecting columns from a **DataFrame** works similarly to selecting
rows. We can use square brackets (``[`` and ``]``) along with the name
of the column (as a **str**\ ing) to select a single column:

.. code:: ipython3

    station_data['rain'] # select the rain column

If we want to select multiple columns, we can use a **list** of column
names inside of the square brackets:

.. code:: ipython3

    station_data[['date', 'rain', 'station', 'season']] # select the date, rain, station, and season columns

Note that the order of the output will be the same as the order of the
input - so, this is one way that we can also re-arrange columns.

You can also select a *slice* of columns using the ``:`` operator. Note
that unlike how we have seen this used before, when used to select
columns (or rows) from a **DataFrame** using labels, ``:`` is inclusive:

.. code:: ipython3

    station_data.loc[:, 'year':'rain'] # select all columns from year to rain (inclusive)

Finally, we can also use ``.filter()``
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.filter.html>`__)
to select columns:

.. code:: ipython3

    station_data.filter(['date', 'rain']) # select the date and rain columns using filter()

re-arranging columns using reindex()
------------------------------------

We might also want to re-arrange the order of columns - there are a
number of different ways to do this, but we’ll have a look at using
``.reindex()``
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.reindex.html>`__).

First, we can create a **list** of the column names, in the order we
want to see them. We then pass this to ``.reindex()``, using the
``columns`` argument:

.. code:: ipython3

    new_order = ['date', 'year', 'month', 'season', 'station', 'tmax', 'tmin', 'air_frost', 'rain', 'sun']
    station_data = station_data.reindex(columns=new_order) # change the order of the columns and assign the output to the same variable

    station_data.head() # show the first 5 rows of the dataframe

saving data to a file
---------------------

Now that we have combined the different data files, added some new
columns to our data, and re-named and re-arranged the columns, we should
save our dataset to a file. We’ll use the ``.to_csv()`` method
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html>`__)
to do this. As with reading files, though, there are other file
formatting options.

Once again, we will use ``Path`` to create a path object to write the
file to; we also set the ``index`` argument to ``False`` so that
``pandas`` doesn’t write the row numbers to the file:

.. code:: ipython3

    station_data.to_csv(Path('data', 'combined_stations.csv'), index=False)

Now, we’ll be able to load this file when we want to do further
analysis, rather than needing to re-run the steps to load each file,
combine the tables, create new variables, and so on.

grouping data
-------------

Next, we’ll see how we can use different tools to aggregate and
summarize our data, starting with ``.groupby()``
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.groupby.html>`__).
To start, we’ll group the data by ``station``:

.. code:: ipython3

    station_data.groupby('station') # group the data by station

Here, we don’t see anything special - just that the output of
``.groupby()`` is, by itself, a **DataFrameGroupBy** object. Among other
things, though, we can use this object to calculate `descriptive
statistics <https://pandas.pydata.org/pandas-docs/stable/reference/groupby.html#dataframegroupby-computations-descriptive-stats>`__
for each column, based on the applied groupings.

For example, we can use ``.mean()``
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.SeriesGroupBy.mean.html>`__)
to calculate the mean value of each column (specifying
``numeric_only=True`` to make sure that we only get a result for numeric
columns):

.. code:: ipython3

    station_data \
        .groupby('station') \
        .mean(numeric_only=True) # specify numeric_only=True to avoid warning messages

Note that by default, ``.groupby()`` drops ``NaN`` values - if we want
to keep these, we need to specify ``dropna=False`` when we create the
groupings.

Now, let’s combine this with what we learned in the previous lesson (the
plotting exercise) to create a plot that shows the distribution of
rainfall by season, separated by station. First, we want to create a
plot that shows the density distribution of rainfall for each season,
using ``sns.FacetGrid()`` to create a single panel for each station:

.. code:: ipython3

    g = sns.FacetGrid(data=station_data, col='station', hue='season', col_wrap=2) # create a 2x2 grid with a panel for each station
    g.map_dataframe(sns.kdeplot, x='rain', fill=True) # plot the density of rainfall
    g.add_legend() # add a legend

Next, we can use ``group_by()`` to calculate the mean rainfall for each
station, and assign this to a new variable, ``mean_values``:

.. code:: ipython3

    mean_values = station_data.groupby('station')['rain'].mean()

Now, we’ll iterate over axis and mean value pairs to plot a vertical
line using ``matplotlib.pyplot.axvline()``
(`documentation <https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.axes.Axes.axvline.html>`__).
As we mentioned in the previous exercise, ``seaborn``, like many other
plotting packages, is built on top of ``matplotlib`` - meaning that many
``seaborn`` objects inherit from correpsonding ``matplotlib`` objects.

First, though, we’ll make sure that we’re plotting in the correct panel
by using the ``axes_dict`` *attribute* of our **FacetGrid**:

.. code:: ipython3

    g.axes_dict # show the dict of key/value pairs for the facetgrid

We can iterate over the ``index`` of ``mean_values`` (which corresponds
to each station), then use the ``axes_dict`` to plot a vertical line
corresponding to each mean value:

.. code:: ipython3

    for station in mean_values.index: # iterate over station names
        g.axes_dict[station].axvline(x=mean_values[station], color='k', linestyle='--') # plot a vertical line at the mean rain value for each station

    g.fig # show the updated figure

In the next panel, write some lines of code to change the axes labels
and increase the font size for the tick labels, axis labels, and panel
labels:

.. code:: ipython3

    # your code goes here!

Now that you have finished the plot, be sure to save it to a file:

.. code:: ipython3

    g.fig.savefig('seasonal_rain_distribution.svg')

slicing
-------

We’ll finish up by looking at a few functions that we can use to *slice*
a dataset - that is, extract specific rows from a group. For example, we
can use ``.loc`` along with the ``.idxmax()`` function
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.idxmax.html>`__)
to get the row corresponding to the maximum value of ``rain`` (for the
minimum, we would use ``.idxmin()``):

.. code:: ipython3

    station_data.loc[station_data['rain'].idxmax()] # use idxmax to find the index of the maxmimum value

We can also make use of ``.head()``
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.head.html>`__),
along with ``.sort_values()``, to select ``n`` rows corresponding to the
maximum value of one or more variables:

.. code:: ipython3

    station_data \
        .sort_values('rain', ascending=False) \
        .head(n=5)

Alternatively, we can use ``.tail()``
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.tail.html>`__),
which returns the last ``n`` rows of the **DataFrame** (note, however,
that this may give us ``NaN`` values):

.. code:: ipython3

    station_data \
        .sort_values('rain') \
        .tail(n=5)

Let’s say that we wanted to find the month with the most rain from each
of the stations. To do this, we can first sort ``rain`` in descending
order, then group based on ``station``, before using ``.head()`` to
select the first row for each value of ``station``:

.. code:: ipython3

    station_data \
        .sort_values('rain', ascending=False) \
        .groupby('station') \
        .head(n=1)

Finally, we can select a random sample from a **DataFrame** using
``.sample()``
(`documentation <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sample.html>`__).
On a grouped **DataFrame**, we get a random sample from each group:

.. code:: ipython3

    sample = station_data \
        .groupby('station') \
        .sample(5)

exercise and next steps
-----------------------

That’s all for this exercise. To practice your skills, create a notebook
file that does the following:

-  loads the libraries that you need
-  loads the saved data file (**combined_stations.csv**)
-  helps you answer the following questions:

   -  what station has the highest recorded rainfall in the past 20
      years, and on what date?
   -  what season has the lowest average rainfall? is it the same season
      for all four stations?
   -  what station has recorded the most months with ``tmin`` < 1°C? are
      all these observations from a single season?
   -  what is the median rainfall in months where ``tmax`` is greater
      than 20°C? make sure that your result is a number, not a
      **DataFrame**!
   -  what year saw the most total rainfall, using data from all four
      stations?
   -  what are the top 5 driest years, using only data from stations in
      Britain?
   -  what is the lowest annually-averaged monthly minimum temperature
      in the dataset, as measured by a single station?
   -  what is the sunniest month, on average, in Armagh?

      -  bonus: write a line that will rename the months from the number
         to a 3-letter abbreviation (**hint**: we saw an example of this
         using ``.map()``)

For a bonus, try downloading at least one additional dataset from the
`Met
Office <https://www.metoffice.gov.uk/research/climate/maps-and-data/historic-station-data>`__,
saving it to the **data** folder, and using the script provided
(``convert_metoffice.py``) to convert the ``.txt`` file into a ``.csv``
file.

In your new notebook file, remember to add this new data to your
existing dataset (and re-save the file!), then repeat the analyis
questions above.