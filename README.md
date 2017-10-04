# PythonSnippets
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
  - [List and List comprehension](#list-and-list-comprehension)
  - [Dictionary and Dictionary comprehension](#dictionary-and-dictionary-comprehension) ([`bunch`](https://pypi.python.org/pypi/bunch))
  - [String](#string)
  - [Tupple](#tupple)
  - [Enumeration](#enumeration) ([`enum34`](https://pypi.python.org/pypi/enum34))
  - [Matrix with numpy](#matrix-with-numpy) ([`numpy`](http://www.numpy.org/))
  - [Dataframe with pandas](#dataframe-with-pandas) ([`pandas`](http://pandas.pydata.org/))
- [Exceptions](#exceptions)
- [IO Operations](#io-operations)
  - [Csv, Json, and Yaml](#csv-json-and-yaml) ([`csv`](https://docs.python.org/2/library/csv.html), [`json`](https://docs.python.org/2/library/json.html), [`PyYAML`](http://pyyaml.org/wiki/PyYAMLDocumentation))
  - [Path operations](#path-operations) ([`os.path`](https://docs.python.org/2/library/os.path.html))
  - [Pretty Print](#pretty-print) ([`tabulate`](https://pypi.python.org/pypi/tabulate), [`termcolor`](https://pypi.python.org/pypi/termcolor))
- [Process and Parallel Processing](#process-and-parallel-processing)
  - [Process](#process)
  - [Parallel Processing](#parallel-processing)
- [Networking](#networking)
  - [Consume REST API](#consume-rest-api) ([`requests`](http://docs.python-requests.org/en/master/))
  - [Build REST API](#build-rest-api) ([`Flask`](http://flask.pocoo.org/), [`flask-restplus`](http://flask-restplus.readthedocs.io/en/stable/))
- [Jupyter](#jupyter) ([`jupyter`](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/))
  
## Coding Styles
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
# if use hanging indent: no arguments on the first line and further indentation on arguments.
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)
# Aligned with opening delimiter.
foo = long_function_name(var_one, var_two,
                         var_three, var_four)
# The closing brace/bracket/parenthesis on multi-line constructs line up under the first non-whitespace character:
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
`pip` gives you access to thousands of battle-tested Python libraries. It is the foundation of how Python becomes so convenient and powerful. In a python project, you usually find a `requirements.txt` file, which lists all the python packages that used in the project. 
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
`conda` is a highly recommended way to manage python environement. You can create a seperate python enviroment for each of your projects. Installing packages with `conda install` is also more robust than using `pip`, since it uses pre-compiled libraries.

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
The two most important data structures in python are `List` and `Dictionary`. `numpy` is the most important data structure for scientific computing, which deals with `matrix` operations. For data scientists, `pandas` and its `dataframe` data structure is the most popular way to represent a data table.
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
```python
#TODO: string
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
## IO operations
#### CSV, Json, and Yaml
```python
json, yaml
```
#### Path operations
```python
# Change working directory to the script directory, so that open file will work with relative path
abspath = os.path.abspath(__file__)
dname = os.path.dirname(abspath)
os.chdir(dname)
```
#### Pretty Print
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
## Process and Parallel Processing
#### Process
```python
#Use setproctitle to set title for python process, useful when using ps to know which process to be killed.
import setproctitle
setproctitle(title)
getproctitle() #Return current process title
```
#### Parallel Processing
```python
#TODO
```
## Networking
#### Consume REST API
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
```python
#Use Flask to build simple REST API. 
#Use Flask-restplus automatically document your API and get the swagger page for free.
from flask import Flask 
app = Flask(__name__)
@app.route("/")
def hello():
 return "Hello World!"
if __name__ == "__main__":
 app.run()
```
## Jupyter
```python
!%matplotlib inline #inclide plots from matplotlib to the jupyter notebook
!%config IPCompleter.greedy=True  #Press Tab to get autocomplete
#TODO: Widget!
```
