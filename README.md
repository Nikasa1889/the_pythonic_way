# the_pythonic_way
`the_pythonic_way` contains a collection of useful snippets and recommendations of how to program in a "Pythonic way". People that come to Python from other languages like Java, C# or R might find these snippets helpful. `the_pythonic_way` can be used as a comprehensive Python cheatsheet, where you can look for short answers and keywords of how to do things in Python, so that you can easily google further.

# Table of Content:
- [Coding Styles](#coding-styles) ([`PEP 8`](https://www.python.org/dev/peps/pep-0008/), [Google Style](https://google.github.io/styleguide/pyguide.html))
  - [Naming Conventions](#naming-conventions)
  - [Code Layout](#code-layout)
  - [Code Quality Tools](#code-quality-tools) ([`.editorconfig`](http://editorconfig.org/), [`PyLint`](https://www.pylint.org/))
- [Environment Management](#environment-management) 
  - [Pip requirements](#pip-requirements) ([`pip`](https://pip.pypa.io/en/stable/))
  - [Conda environment management](#conda-environment-management) ([`conda`](https://conda.io/docs/))
- [Pythonic Objects, Protocols, and ABCs](#) ([`abc`](https://docs.python.org/3/library/collections.abc.html), [`UML`](https://gitlab.com/yahya-abou-imran/collections-abc-uml/blob/master/plantuml/full.svg))
- [Data Structures](#data-structures)
  - [Tuple and Tuple Unpacking](#tuple-and-tuple-unpacking) ([`tuple`](https://docs.python.org/3.6/library/stdtypes.html#tuple))
  - [List and List comprehension](#list-and-list-comprehension)
  - [Deque, Synchronized Queue, Priority Queue](#other-list-related)
  - [String](#string) ([`f-strings`](https://www.python.org/dev/peps/pep-0498/), [string manipulations](https://docs.python.org/3.6/library/stdtypes.html#str), [regular expression](https://docs.python.org/3.6/library/re.html))
  - [Common Sequence Operations and Indexing](#common-sequence-operations-and-indexing)
  - [Dictionary and Dictionary comprehension](#dictionary-and-dictionary-comprehension) ([`bunch`](https://pypi.python.org/pypi/bunch))
  - [Set](#set)
  - [Enumeration](#enumeration) ([`enum34`](https://pypi.python.org/pypi/enum34))
  - [Matrix with numpy](#matrix-with-numpy) ([`numpy`](http://www.numpy.org/), [`memmap`](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.memmap.html), [`bcolz`](https://github.com/Blosc/bcolz))
  - [Dataframe with pandas](#dataframe-with-pandas) ([`pandas`](http://pandas.pydata.org/))
- [Numeric and Bit Operators](#numeric-and-bit-operators)
- [Control Flows](#control-flows) ([`compound statements`](https://docs.python.org/3/reference/compound_stmts.html))
- [Functional Programming](#functions)
- [Modules](#modules)
- [Exceptions](#exceptions) ([`throw exception`](https://eli.thegreenplace.net/2008/08/21/robust-exception-handling/))
- [Debugging](#debugging) ([`pdb`](https://stackoverflow.com/questions/1623039/python-debugging-tips), [`ipdb`](http://devmartin.com/blog/2014/10/trigger-ipdb-within-ipython-notebook/))
- [IO Operations](#io-operations)
  - [Csv, Json, and Yaml](#csv-json-and-yaml) ([`csv`](https://docs.python.org/2/library/csv.html), [`json`](https://docs.python.org/2/library/json.html), [`ujson`](https://pypi.org/project/ujson/), [`PyYAML`](http://pyyaml.org/wiki/PyYAMLDocumentation))
  - [Path operations](#path-operations) ([`pathlib`](http://pbpython.com/pathlib-intro.html), [`os.path`](https://docs.python.org/2/library/os.path.html))
  - [Pretty Print](#pretty-print) ([`tabulate`](https://pypi.python.org/pypi/tabulate), [`termcolor`](https://pypi.python.org/pypi/termcolor))
  - [Progress bar](#progress-bar) ([`tqdm`](https://pypi.python.org/pypi/tqdm))
- [Process and Parallel Processing](#process-and-parallel-processing)
  - [Process](#process)
  - [Parallel Processing](#parallel-processing) ([`multiprocessing`](https://docs.python.org/2/library/multiprocessing.html))
- [Networking](#networking)
  - [Consume REST API](#consume-rest-api) ([`requests`](http://docs.python-requests.org/en/master/))
  - [Build REST API](#build-rest-api) ([`flask`](http://flask.pocoo.org/), [`flask-restplus`](http://flask-restplus.readthedocs.io/en/stable/), [`connexion`](http://connexion.readthedocs.io/en/latest/))
- [Scikit-learn](#scikit-learn) ([`LabelEncoder`](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html))
- [Jupyter](#jupyter) ([`jupyter`](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/))
- [Microservices](#microservices) ([`12 factor`](https://12factor.net/))
## Coding Styles
[`PEP 8`](https://www.python.org/dev/peps/pep-0008/) is highly recommended to go through, at least once in you life. It lists all the coding rules that accepted by the whole Python ecosystem. The [Google Style](https://google.github.io/styleguide/pyguide.html) is also a very good and comprehensive reference.
#### Naming Conventions
```python
import os                            #lower_case for package name, as short as possible (use abbrs)
class MyBag:                         #CapitalizedWords for class name
    """Example class with types documented in the docstring.
       You should always use CapitalizedWords for class name
    """
    MAX_OVERFLOW = 10                #ALL_CAPITALIZED for constant
    def __init__(self):              
        self.data = []
                                     #blank line between two methods/functions
    def add_x(self, x):              
    """ Example of class method, which should has lower_case_underscore name
    Args:
        x (int): The first parameter.
    Returns:
        bool: True if successful, False otherwise.
    """
        self.data.append(x)

    def _hidden_add(self, x):        
    """ Use _single_leading_underscore for weak "internal use" indicator"""
        pass
```
#### Code Layout
```python
# Use 4 spaces indentation
# Limit all lines to 79 characters
# Use utf-8 file encoding
# Always try to align with opening delimiter.
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# if use hanging indent: no arguments on the first line and further indentation on arguments.
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)
# The closing brace/bracket/parenthesis on multi-line constructs line up 
# under the first non-whitespace character:
my_list = [
    1, 2, 3,
    4, 5, 6,
    ]
```
#### Code Quality Tools
You can define a [`.editorconfig`](http://editorconfig.org/) file at the root folder of your python project. It is recognized by many common Python IDE and version control system such as Pycharm and github. These programs automatically enforces the rules defined in the `.editorconfig` file. A common setting for python is 
```yaml
root = true

[*]
charset = utf-8
indent_style = space
indent_size = 4
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true

[*.{html,js,css,json,yml,yaml}]
indent_size = 2

[Makefile]
indent_style = tab
```
You can use [`PyLint`](https://www.pylint.org/) to analyze your code and ensure the code quality.
## Environment Management
#### Pip requirements
[`pip`](https://pip.pypa.io/en/stable/) gives you access to thousands of battle-tested Python libraries. It is the foundation of how Python becomes so convenient and powerful. In a python project, you usually find a `requirements.txt` file, which lists all the python packages that used in the project. 
```yaml
Flask>=0.12.2
flask-restplus>=0.10.1
PyYAML>=3.12
requests>=2.18.4
pyOpenSSL>=17.3.0
cryptography==1.9
```
All the requirements can be installed by using pip:
```bash
pip install -r requirements.txt
```
#### Conda environment management
[`conda`](https://conda.io/docs/) is a highly recommended way to manage python environement. You can create a seperate python enviroment for each of your projects. Installing packages with `conda install` is also more robust than using `pip`, since it uses pre-compiled libraries.

Example of how to define an environment for conda in a `conda_environement.yml` file:
```yaml
name: ProjectChangeTheWorld
dependencies:
  - python = 2.7.13
  - pip:
    - Flask>=0.12.2
    - flask-restplus>=0.10.1
    - PyYAML>=3.12
    - requests>=2.18.4
    - pyOpenSSL>=17.3.0
    - cryptography==1.9
```
How to update/create a conda environment using the `conda_environement.yml` file, and activate it:
```bash
conda env update --file conda_environment.yml
activate ProjectChangeTheWorld
```

## Data Structures
The three most popular and important built-in data structures in python are `tuple`, `list` and `dict` with their elegant `comprehension` syntax; come behind are `str` and `set`. `generator` is a powerful and elegant way to iterate over any type of container object. `numpy` is the most important data structure for scientific computing dealling with `matrix` operations. For data scientists, `pandas` and its `dataframe` data structure is the most popular way to represent a data table.

#### Tuple and Tuple Unpacking
[`tuple`](https://docs.python.org/3.6/library/stdtypes.html#tuple) is immutable sequences, typically used to store collections of heterogeneous data (data of different types). Tuple is an important concept in functional programming, where all variables are immutable. It can be used as a flexible version of C `struct`. It is commonly used to pack mutiple results returned by a function. Note that `tuple` is a sequence structure, so all [common sequence operations and indexing](#common-sequence-operations-and-indexing) can be used.

```python
tp = ('a', 1, 'b', 2)                 # declare a tuple
tp = 'a', 1, 'b', 2                   # you do not need paratheses to declare tuple

a, av, b, bv = tp                     # unpacking tuple into variables, useful 
def f(tp):                                  # function that concate string at even index, 
  return (''.join(tp[::2]), sum(tp[1::2]))  #   and sum of number at odd index of input tuple.
name, total = f(tp)                   # unpacking tuple returned by a function
```

#### List and List comprehension
List are mutable sequences, typically used to store collections of homogeneous items (items of the same data type).
```python
## Declare list
xs = [1, 2, 3, 4, 5]                  # declare a list
ys = list(range(5))                   # convert range; generator; tuple;... to list by using list(.)
sorted(xs, reverse=True)              # sort a list
xts = tuple(xs)                       # convert list into tuple, which is immutable and can be distribute
a,b,c = [1, 2, 3]                     # unpack list to multiple variables; number of variables must equal length of list

## List comprehension
[f(x) for x in xs]                    # map function f(.) to each element of xs. xs can be any sequence like list, string, tuple.
[f(x) for x in xs if is_g(x)]         # filter with is_g(.) and map f(.) to each list element
[f(x) for xs in xss for x in xs]      # map function f(.) to each element in a list_of_list and flatten it
[[f(x) for x in xs] for xs in xss]    # nested list comprehension, apply f(.) to each element of list_of_list, preserving structure
[f(x, y) for (x, y) in zip(xs, ys)]   # map a function f(.,.) to a list of tupple

## Modify list
xs.append(6)                          # append 6 to the end of list xs
xs.extend(ys)                         # append all elements of ys to the end of xs
xs.insert(0, 6)                       # insert 6 to position 0 of xs
xs.pop()                              # remove last element of xs and return its value
xs.pop(2)                             # remove element at index 2 of xs
xs.reverse()                          # reverse the elements of xs (in-place)

## Sort a list
sorted(xs, reverse=True)              # return sorted version of xs (asc if reverse=True, otherwise, desc)
[x[0] for x in sorted(enumerate(xs), key=lambda tup:tup[1])] # return index of sorted elements of xs

## Unique list
list(set(xs))                         # return new list with unique elements of xs
```
#### String
In python, `str` is a sequence of char, which means all [common sequence operations](#common-sequence-operations-and-indexing) can be used. Here I only list string-specific operations, which includes [string format](https://www.python.org/dev/peps/pep-0498/), [string manipulations](https://docs.python.org/3.6/library/stdtypes.html#str), and [regular expression](https://docs.python.org/3.6/library/re.html).

Python supports multiple ways to format text strings. These include [`%-formatting`](https://pyformat.info/) , [`str.format()`](https://pyformat.info/), and `string.Template`. But in most case, the best way to format string in Python is by using Literal String Interpolation, or usually referred to as [`f-strings`](https://www.python.org/dev/peps/pep-0498/).

```python
# String format
st = 'one'; n_1 = 2; n_2 = 3.0
'%s %d %f' % (st, n_1, n_2)             # %-formatting
'{} {} {}'.format('one', 2, 3.0)        # str.format()
f'{st} {n_1} {n_2}'                     # Literal String Interpolation, or f-strings

# String manipulation
'   spacious   '.strip()                # Remove leading and trailing spaces
st.startswith('on')                     # Check if st start with 'on'; can specify start and end index
st.startswith('ne')

''.join(['1', '22', 'xx'])              # join list of strings into a single string
', '.join(['1', '22', 'xx'])            # join list of strings with ', ' as seperator
'1,2,3'.split(',')                      # split a string using ',' as seperator.
'1,2,3'.split(',', maxsplit=1)          # split a string maxsplit times using ',' as seperator (return ['1', '2,3'])

st.replace('ne', 'NE')                  # return a copy of the string with all occurrences of 'ne' replaced by new 'NE'.

# String search
#Find index where a substring first begins in a string
str1 = "this is string example....wow!!!";
str2 = "exam";
str1.find(str2)                         # return the lowest index in str1 where str2 is found.
str1.find(str2, start=10, end=20)       # return the lowest index in range [start:end] where str2 is found in str1
str1.index(str2)                        # like find(), but raise ValueError when the str2 is not found.

# Regular Expression
import re
text = "He was carefully disguised but captured quickly by police."
re.findall(r"\w+ly", text)             # find all occurrences of a pattern (return ['carefully', 'quickly'])
for m in re.finditer(r"\w+ly", text):  # find all matches with their positions.
    print(f'{m.start()}-{m.end()}: {m.group(0)}')
re.search(r"\w+ly", text)              # return match object contains first match of pattern. 
                                       #   match object has info about where the match occurs
re.sub(r"\w+ly", '__', text)           # replace all occurences of a pattern with the string '__'.
re.sub(r"\w+ly", f, text)              # replace all occurences x of a pattern with f(x).
re.split(r"but", text)                 # split string into list of strings using any substring that satisfies the pattern
```

#### Common Sequence operations and Indexing
All sequence data structures, including `tuple`, `list`, and `string`, accepts the following [common sequence operations](https://docs.python.org/3.6/library/stdtypes.html#typesseq-common). 
```python
xs = [3, 5, 7, 9]         # xs is a sequence, can be list, tuple, or string
ys = [2, 4, 6, 8]
x = 1                     # x is an item

x in xs                   # check if x is in xs
x not in xs               # check if x is not in xs
xs.count(x)               # number of items equal to x in xs
xs + ys                   # create new sequence by concenate xs and ys
xs*3                      # create a new sequence by concenate xs 3 times to itself
len(xs); min(xs); max(xs) # length, min, and max value of xs

#Indexing
xs[1]                     # return item 1 of xs; the first index is always 0
xs[0:2]                   # slice of xs from 1 to 3
xs[0:3:2]                 # slice of xs from 0 to 3 with step 2
xs[::2]                   # all items at even index
xs[1::2]                  # all items at odd index
xs[:-1]                   # all items except the last
xs.index(x, 1, 3)          # index of the first occurence of x in xs that comes after the 1th and before 3th item.

#Looping
[f(x) for x in xs]                    # map function f(.) to each list element
[f(idx, x) for idx, x in enumerate(xs)] # use enumerate(.) to loop through elements of a sequence with index

#Unpacking
a, b, c = xs             # unpack elements of xs into a, b, and c; len(xs) must equal 3
f(*xs)                   # the single star operator unpacks the sequence xs into positional arguments of f(.)
```
#### Generator and Yield
[`generator`](https://wiki.python.org/moin/Generators)

#### Dictionary and Dictionary comprehension
```python
{x: x for x in xs}                    # create dict from list
[(k,dct[k]) for k in dct ]            # create list of tupple from dict
for key, value in dict.iteritems():   # looping through key and value

#Should use `bunch` for dict with attribute-style access. JSON and YAML-friendly
import bunch
b = Bunch()
b.hello = 'world'
b['hello'] += "!"
```

#### Enumeration
```python
#Use enum34
#TODO
```
#### Matrix with numpy
```python
#TODO: Use numpy
```
#### Dataframe with pandas
```python
#TODO: Use pandas
```
## Control Flows
[`Compound Statments`](https://docs.python.org/3/reference/compound_stmts.html)
```python
#TODO: if, while, for
```
## Functions
```python
#TODO: def, lambda, * star o
```
## Modules
```python
#TODO: import, isort, PYTHONPATH
```
## Exceptions
In Python, we usually prefer raising exceptions than returning error code, [`check here`](https://eli.thegreenplace.net/2008/08/21/robust-exception-handling/)
Use the logging package when you catch an exception so that you get a full exception traceback

```python
import logging
try:
    # change the world
except Exception as ex:
    logging.exception('', exc_info=True)
```
You can setup custom logger (file or stream handler) like this:

```python
logger = logging.getLogger(__name__)
logger.setLevel(logging.DEBUG)

formatter = logging.Formatter('%(asctime)s:%(name)s:%(message)s')

file_handler = logging.FileHandler('sample.log')
file_handler.setLevel(logging.ERROR)
file_handler.setFormatter(formatter)

stream_handler = logging.StreamHandler()
stream_handler.setFormatter(formatter)

logger.addHandler(file_handler)
logger.addHandler(stream_handler)
...
logger.Info("Everything is working fine, sir!")
logger.exception("Alert, Alert!")
```

## Debugging
Create a pbd breakpoint by putting this line wherever you like [`Read More`](https://stackoverflow.com/questions/1623039/python-debugging-tips):
```python
import pdb; pdb.set_trace();
```
I usually prefer to experiment codes in Jupyter. You can use [`ipdb`](http://frid.github.io/blog/2014/06/05/python-ipdb-cheatsheet/) to debug in Jupyter. To [`trigger`](http://devmartin.com/blog/2014/10/trigger-ipdb-within-ipython-notebook/) a debugging session in Jupyter, at the following line to your code at where you want to start debugging:

```python
from IPython.core.debugger import Tracer; Tracer()()
```

## IO operations
#### CSV, Json, and Yaml
```python
json, yaml
```
#### Path operations
You can either use `os` package
```python
# Join paths
os.path.join('path/the/dir','subdir/inside')
# Change working directory to the script directory, so that open file will work with relative path
abspath = os.path.abspath(__file__)
dname = os.path.dirname(abspath)
os.chdir(dname)
```
Or you can use [`pathlib`](http://pbpython.com/pathlib-intro.html), which is much more convient way to deal with path and files in Python.
```python
from pathlib import Path
in_file_1 = Path.cwd() / "in" / "input.xlsx"                    #No need for complicated os.path.join(.)
[file for file in Path.cwd().iterdir() if not file.is_dir() ]   #Easy to iterate a directory (cwd in this case)
```
#### Pretty Print
Use `tabulate` to pretty print tabular data, and `termcolor` to colorize terminal output.
```python
#Pretty print for tabular data, use tabulate
from tabulate import tabulate
print tabulate({"Name": ["Alice", "Bob"], "Age": [24, 19]}, headers="keys")

#Color for terminal output, to easily get attention, use termcolor
from termcolor import colored, cprint
text = colored('Hello, World!', 'red', attrs=['reverse', 'blink']); print(text)
cprint('Hello, World!', 'green', 'on_red')
print_red_on_cyan = lambda x: cprint(x, 'red', 'on_cyan')
print_red_on_cyan('Hello, World!')
```
#### Progress bar
Instantly make your loops show a smart progress meter. Just wrap any iterable with tqdm(iterable), and you’re done!
```python
from tqdm import tqdm
for i in tqdm(range(10000)):
    ...
```
## Process and Parallel Processing
#### Process
```python
#Use setproctitle to set title for python process, useful when using ps to know which process to be killed.
import setproctitle
setproctitle(title)
getproctitle() #Return current process title
```
#### Parallel Processing
The recommended way to spawn mutiple processes in Python is to use the `multiprocessing` package.
```python
import multiprocessing

def worker(num):
    """thread worker function"""
    print 'Worker:', num
    return

if __name__ == '__main__':     # always check for __main__ to prevent recursive spawning
    jobs = []
    p1 = multiprocessing.Process(target=worker, args=(1,))
    p2 = multiprocessing.Process(target=worker, args=(2,))
    p1.start()
    p2.start()
    p1.join()  # wait for worker 1
    p2.join()  # wait for worker 2
```
## Networking
#### Consume REST API
Being the most downloaded package on pip, `requests` has everything you need when interacting with REST APIs
```python
import requests
params = {'param_1': 1, 'param_2': 2}
resp = requests.get('https://api.github.com/events', params, auth=(username, password))
resp = requests.post('http://httpbin.org/post', data = {'key':'value'})
resp = requests.put('http://httpbin.org/put', data = {'key':'value'})
resp = requests.delete('http://httpbin.org/delete')
resp = requests.head('http://httpbin.org/get')
resp = requests.options('http://httpbin.org/get')
```
#### Build REST API
`flask` is the most common way to create a microservice in Python, which has many plugins that you can add to your service. The most common plugin is `flask-restplus`, which automatically document your API and get you the swagger page for free.
You can also try `connexion`, which built on top of `flask` and following the "API design first" principle.
```python
from flask import Flask 
app = Flask(__name__)
@app.route("/")
def hello():
 return "Hello World!"
if __name__ == "__main__":
 app.run()
```
## Scikit-learn
```python
#sklearn.preprocessing.LabelEncoder
from sklearn import preprocessing
le = preprocessing.LabelEncoder()
le.fit([1, 2, 2, 6])
le.classes_
# array([1, 2, 6])
le.transform([1, 1, 2, 6]) 
# array([0, 0, 1, 2]...)
le.inverse_transform([0, 0, 1, 2])
# array([1, 1, 2, 6])
```
## Jupyter
```python
!%matplotlib inline #inclide plots from matplotlib to the jupyter notebook
!%config IPCompleter.greedy=True  #Press Tab to get autocomplete
#TODO: Jupyter Widget!
```
## Coding Workflow
I use Jupyter and Vim8 together to program. I experiment my code first in Jupyter and reorganize things using Vim8. Code can be debugged in Jupyter with `ipdb`. To maintain session, I use `tmux`. I setup Vim8 similar to what introduced here: [Use VIM as a python IDE](http://liuchengxu.org/posts/use-vim-as-a-python-ide/)

Useful shortcuts in VIM. Some I configured myself, some are default behavior of VIM or its plugins.

| Shortcut | Function |
| --- | --- |
| `"+` | Select + (system clipboard) as vim register. Need `vim-gtk`|
| `Ctr-c ; Ctr-p` | Copy to and Paste from the system clipboard |
| `tab` | Fill spaces as tabbing the whole line, even in insert mode |
| `shift-tab` | Delete tabbing of the whole line |
| `space` | Toggle code fold |
| `Ctr-y` | Run YAPF for code reformating |
| `bb` | In insert mode, put breakpoint |
| `\d` | Go to code definition |
| `\r` | Rename |
| `Ctr-o` | Go to previous place |
| `Ctr-space` | Autocomplete with Jedi-vim |
| `:Isort` | Run isort to sort and clean import section |
| `F3` | Run AutoFormat (call autopep8) |

Vim search pattern in all files: `:vimgrep /pattern/ ./**/*.py | cw`

Note: To use `tmux-yank` while opening tmux through a SSH connection, you must have X forwarding enabled. Add -X option to ssh command, and make sure the ssh server has enabled X-forwarding.
## Microservices
[12 factor](https://12factor.net/)

[Code reuse in microservices](http://blog.scottlogic.com/2016/06/13/code-reuse-in-microservices-architecture.html)

[Don't share libraries among microservices](https://blog.philipphauer.de/dont-share-libraries-among-microservices/)
