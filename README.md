# timeplot.py
Time graph plotting library for OSU CS325

## Installation
```
pip install timeplot
```

## timeplot.timeplot
Plot the runtime of a function based on input data.

Keyword arguments:
fs -- either a single function or list of functions to be tested
input\_data\_sets-- either a set of data to be input into the function or a list of sets. each set can be either a set of single arguments to be directly
    inputted or a set of dicts representing kwargs
filename -- output filename (default "")
    supported formats include, but are not limited to:
        - png
        - pdf
        - svg
interps -- whether or not to interpret the data in input\_data\_set as a collection. if TRUE, it will be interpreted as such (default cycle(True))
test\_params -- the names of the parameters to be tested as strings, iff input\_data\_set is a set of dicts represents kwargs (default cycle(""))

Keyword-only arguments:
plot\_options -- options for the plot's display, as a dictionary
    options include:
        - title
        - x-label
        - y-label
        - colors: an iterator listing the colors that different series will cycle through
legends -- legend names. if left to None, will default is the calling functions' __name__ properties (default None)
preview\_plot -- whether or not to display a preview of the plot in a window (default True)


## Basic usage
```py
from timeplot import timeplot

# This assumes that you do not want to save it to a file, input the data directly as the ONLY parameter to the function,
# and use the default interpretation of "size" (collection interpretation)
timeplot(function_list_or_single_function, list_of_sets_containing_data_or_single_set)
```

## Some more advanced usage
```py
from timeplot import timeplot

# Write output to a file
# supported types:
# - png
# - pdf
# - svg
# - and more, but who cares about the rest
# Be sure to include the extension in the filename
timeplot(fs, sets, filename)

# Write output to a file without preview
timeplot(fs, sets, filename, preview_plot=False)

# Interpret data size as scalar instead of collection. This is useful for functions like `pow` or `sqrt`.
from itertools import repeat
timeplot(fs, sets, interps=repeat(False))
```

## Other functions
timeplot.with\_timer(f: Callable) -> Callable
Embellish a function with timing information.

Given a function f, returns a new function equivalent
to that original function but returning a tuple containing
the original results and embellished timing data.


timeplot.make\_timedata(f: Callable,
                        input\_set\_data: set,
                        interp\_as\_coll: bool = True,
                        testing\_parameter: str = "")
Measure the runtime performance of a function with differently-sized inputs and return a dataframe with that information.

Keyword arguments:
f -- the function to be tested
input\_data\_set -- the set of data be input into the function. can be either a set of single arguments to be directly
    inputted or a set of dicts representing kwargs
interp\_as\_coll -- whether or not to interpret the data in input\_data\_set as a collection. if TRUE, it will be interpreted as such
testing\_parameter -- the name of the parameter to be tested, iff input\_data\_set is a set of dicts represents kwargs (default "")
