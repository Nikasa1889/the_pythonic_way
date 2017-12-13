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
- [Data Structures](#data-structures)
  - [Indexing](#indexing)
  - [List and List comprehension](#list-and-list-comprehension)
  - [Dictionary and Dictionary comprehension](#dictionary-and-dictionary-comprehension) ([`bunch`](https://pypi.python.org/pypi/bunch))
  - [String](#string) ([`PyFormat`](https://pyformat.info/))
  - [Tupple](#tupple)
  - [Enumeration](#enumeration) ([`enum34`](https://pypi.python.org/pypi/enum34))
  - [Matrix with numpy](#matrix-with-numpy) ([`numpy`](http://www.numpy.org/), [`memmap`](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.memmap.html))
  - [Dataframe with pandas](#dataframe-with-pandas) ([`pandas`](http://pandas.pydata.org/))
- [Exceptions](#exceptions) ([`throw exception`](https://eli.thegreenplace.net/2008/08/21/robust-exception-handling/))
- [IO Operations](#io-operations)
  - [Csv, Json, and Yaml](#csv-json-and-yaml) ([`csv`](https://docs.python.org/2/library/csv.html), [`json`](https://docs.python.org/2/library/json.html), [`PyYAML`](http://pyyaml.org/wiki/PyYAMLDocumentation))
  - [Path operations](#path-operations) ([`os.path`](https://docs.python.org/2/library/os.path.html))
  - [Pretty Print](#pretty-print) ([`tabulate`](https://pypi.python.org/pypi/tabulate), [`termcolor`](https://pypi.python.org/pypi/termcolor))
  - [Progress bar](#progress-bar) ([`tqdm`](https://pypi.python.org/pypi/tqdm))
- [Process and Parallel Processing](#process-and-parallel-processing)
  - [Process](#process)
  - [Parallel Processing](#parallel-processing) ([`multiprocessing`](https://docs.python.org/2/library/multiprocessing.html))
- [Networking](#networking)
  - [Consume REST API](#consume-rest-api) ([`requests`](http://docs.python-requests.org/en/master/))
  - [Build REST API](#build-rest-api) ([`flask`](http://flask.pocoo.org/), [`flask-restplus`](http://flask-restplus.readthedocs.io/en/stable/)), [`connexion`](http://connexion.readthedocs.io/en/latest/)
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
The two most important data structures in python are `List` and `Dictionary`, with their elegant `comprehension` syntax. `numpy` is the most important data structure for scientific computing dealling with `matrix` operations. For data scientists, `pandas` and its `dataframe` data structure is the most popular way to represent a data table.
#### Indexing
```python
#TODO: Common Python indexing ways that accepted in almost every data structure
```
#### List and List comprehension
```python
xs = [1, 2, 3, 4, 5]                  #Declare a list
[f(x) for x in xs]                    #Map function f(.) to each list element
[f(x) for x in xs if is_g(x)]         #Filter with is_g(.) and map f(.) to each list element
[f(x) for xs in xss for x in xs]      #Map function f(.) to each element in a list_of_list

[f(x, y) for (x, y) in zip(xs, ys)]   #Map a function f(.,.) to a list of tupple

#sort unique elements of a list
sorted(list(set(xs)))                 #use list(set(.)) to produce list with unique elements, sorted(.) to sort.
```
#### Dictionary and Dictionary comprehension
```python
{x: x for x in xs}                    #create dict from list
[(k,dct[k]) for k in dct ]            #create list of tupple from dict
for key, value in dict.iteritems():   #Looping through key and value

#Should use `bunch` for dict with attribute-style access. JSON and YAML-friendly
import bunch
b = Bunch()
b.hello = 'world'
b['hello'] += "!"
```

#### String
You should consider reading this awesome [`PyFormat`](https://pyformat.info/) about how to format string in Python 
```python
a = b = c = 'a string'                  # Declare 3 variables contain 'a string'
d = a + c                               # String can be concanated with +
''.join[a, b, c]                        # To concanate more than 2 strings, use ''.join(), much faster than +
'%s %d %f' % ('one', 2, 3.0)            # Old style of how to format string.
'{} {} {}'.format('one', 2, 3.0)        # New style of how to format string.
'{:>10} {:^10} {:10}'.format('aligned_left', 
                      'center', 'aligned_right')
'{:>6.2f}'.format('3.141592653589793')

# A string can be substring just like a list or numpy:
a[2:]; a[:4]; a[:-1]; 

#Find index where a substring first begins in a string
str1 = "this is string example....wow!!!";
str2 = "exam";
print str1.find(str2)
```
#### Tupple
```python
#TODO: tupple 
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
## Exceptions
In Python, we usually prefer raising exceptions than returning error code, [`check here`](https://eli.thegreenplace.net/2008/08/21/robust-exception-handling/)
Use the logging package when you catch an exception so that you get a full exception traceback

```python
import logging
try:
    # change the world
except Exception as ex:
    logging.exception('')
```
## IO operations
#### CSV, Json, and Yaml
```python
json, yaml
```
#### Path operations
```python
# Join paths
os.path.join('path/the/dir','subdir/inside')
# Change working directory to the script directory, so that open file will work with relative path
abspath = os.path.abspath(__file__)
dname = os.path.dirname(abspath)
os.chdir(dname)
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
## Microservices
[12 factor](https://12factor.net/)
[Code reuse in microservices](http://blog.scottlogic.com/2016/06/13/code-reuse-in-microservices-architecture.html)
