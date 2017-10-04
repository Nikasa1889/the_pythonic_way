# PythonSnippets
"The Pythonic way" contains a collection of useful snippets and recommendations of how to program in a "pythonic way". People that come to Python from other languages like Java, C# or R might find these snippets helpful. "The Pythonic Way" can be used as a comprehensive Python cheatsheet, where you can look for short answers and keywords of how to do things in Python, so that you can easily google further.

#Table of Content:
- [Coding Styles](#coding-styles)
  - Naming Conventions
- [Data Structures](#data-structures)
  - [List and List comprehension](#list-and-list-comprehension)
  - [Dictionary and Dictionary comprehension](#dictionary-and-dictionary-comprehension)
  - [String](#string)
  - [Enumeration](#enumeration)
  - [Matrix with numpy](#matrix)
  - [Dataframe with pandas](#pandas)
- [Exceptions](#exceptions)
- [IO Operations](#io-operations)
  - [Csv, Json, and Yaml](#csv-json-and-yaml)
  - [Path operations](#path-operations)
  - [Pretty Print](#pretty-print)
- [Process and Parallel Processing](#process-and-parallel-processing)
  - [Process](#process)
  - [Parallel Processing](#parallel-processing)
- [Networking](#Networking)
  - [Consume REST API](#consume-rest-api)
  - [Build REST API](#build-rest-api)
- [Jupyter](#jupyter)
- [Environment Management](#Environment-Management)
  - [Pip requirements](#pip-requirements)
  - [Conda environment management](#conda-environment-management)
  
## Coding Styles
#### Naming Conventions
```python
#TODO: Naming Conventions
```
## Data Structures
The two most important data structures in python are *List* and *Dictionary*. The two comes with For matrix operations, *Numpy* is the most important package for scientific computing. For data scientists, pandas dataframe is the most popular way to represent a data table. 
#### List and List comprehension
```python
[f(x) for x in xs]
[f(x) for x in xs if is_g(x)]
[f(x) for xs in xss for x in xs]

[f(x, y) for (x, y) in zip(xs, ys)]

#sort unique elements of a list
sorted(list(set(xs)))
```
#### Dictionary and Dictionary comprehension
```python
{x: x for x in xs} #create dict from list
[(k,dct[k]) for k in dct ] #create list of tupple from dict
for key, value in dict.iteritems(): #Looping through key and value
#Should use bunch for dict with attribute-style access. JSON and YAML-friendly
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
r = requests.get('https://api.github.com/events', params, auth=(username, password))
r = requests.post('http://httpbin.org/post', data = {'key':'value'})
r = requests.put('http://httpbin.org/put', data = {'key':'value'})
r = requests.delete('http://httpbin.org/delete')
r = requests.head('http://httpbin.org/get')
r = requests.options('http://httpbin.org/get')
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
## Environment Management
#### Pip requirements
```bash
#TODO:
```
#### Conda environment management
How to update/create a conda environment and activate it
```bash
conda env update --file conda_environment.yml
activate ProjectChangeTheWorld
```
Example of how to define an environment for conda:
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
