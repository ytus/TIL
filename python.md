# Python

## error `Object of type 'TypeError' is not JSON serializable`

When using `json.dumps()` turn errors into strings first: `str(e)` (if error message is enough).

## error `UnboundLocalError: local variable 'x' referenced before assignment`

~~~ python
x = 10
def foo():
  x += 1
~~~~

> -> `UnboundLocalError: local variable 'x' referenced before assignment`. Define `x` as `global`:

~~~ python
x = 10
def foo():
  global x
  x += 1
~~~~

~ https://docs.python.org/3/faq/programming.html#why-am-i-getting-an-unboundlocalerror-when-the-variable-has-a-value

## IPython.lib.pretty print to string, not ontput

Use `pformat`:

~~~ python
from IPython.lib.pretty import pretty

pp = pprint.PrettyPrinter(indent=4)

something = {}
pp.pformat(something)
~~~

# Pandas

## Change date to the end of a month

~~~ python
df['Date'] = pd.to_datetime(df['Date'], format="%Y%m") + pandas.tseries.offsets.MonthEnd(1)
~~~

~ https://stackoverflow.com/a/37354256

# Jupyter (Notebook/Lab)

## Show more columns in a single row of the output

~~~ python
from IPython.lib.pretty import pretty
from IPython.core.display import display, HTML

display(HTML("<style>.container { width:100% !important; }</style>")) # https://stackoverflow.com/a/34058270

pd.options.display.max_columns = 0
~~~
