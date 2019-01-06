# Python

## virtualenvwrapper and anaconda

virtualenvwrapper probably doesn't work correctly with conda

## pyenv install 3.7.1

First install all required dependencies:

    sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
    xz-utils tk-dev libffi-dev liblzma-dev python-openssl

~ https://github.com/pyenv/pyenv/wiki/common-build-problems

## What is the difference between venv, pyvenv, pyenv, virtualenv, virtualenvwrapper, pipenv, etc?

-> https://stackoverflow.com/a/41573588

## error `Object of type 'TypeError' is not JSON serializable`

When using `json.dumps()` turn errors into strings first: `str(e)` (if error message is enough).

## `TypeError: Object of type 'int64' is not JSON serializable`

Use custom serializer with `json.dumps*()`:

~~~ python
def json_serial(obj):
    """JSON serializer for objects not serializable by default json code"""

    if isinstance(obj, (datetime, date)):
        return obj.isoformat()
    if isinstance(obj, np.int64):
        return int(obj)
    raise TypeError("Type %s not serializable" % type(obj))

# ...
    
reusltJson = json.dumps(result, default=json_serial)
~~~

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
somethingString = pp.pformat(something)
~~~

## Show warnings' stacktraces

Change warnings into errors:

~~~ python
import warnings
warnings.filterwarnings('error')
~~~//

and use `try:` `except ... :` as with normal errors.

## Skip pytest's test

~~~ python
import pytest as pytest

pytestmark = pytest.mark.skip()   # skip all tests in this file

@pytest.mark.skip()   # skip this single test
def test_abc():
   ....
~~~

## profiling with cProfile

~~~ python
def a():
  ...
  
cProfile.runctx('a()', globals(), locals(), filename='aStats.profile')
p = pstats.Stats('aStats.profile') \
  .sort_stats('filename', 'cumtime') \
  .print_stats()
~~~

## skip pytest tests

For s single test, use decorator:

`@pytest.mark.skip()`

For a whole module, define `pytestmark`:

`pytestmark = pytest.mark.skip()`

 (~ https://docs.pytest.org/en/latest/skipping.html#skip-all-test-functions-of-a-class-or-module)

## pytest import file mismatch: (...) HINT: remove __pycache__ / .pyc files 

To remove files in pytest's caches, run:

    find . -name '*.pyc' -delete
    
(~ https://blog.mozilla.org/webdev/2015/10/27/eradicating-those-nasty-pyc-files/)

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
