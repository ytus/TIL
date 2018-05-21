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

# Pandas

## Change date to the end of a month

~~~ python
df['Date'] = pd.to_datetime(df['Date'], format="%Y%m") + pandas.tseries.offsets.MonthEnd(1)
~~~

~ https://stackoverflow.com/a/37354256
