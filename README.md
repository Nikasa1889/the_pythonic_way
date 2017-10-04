# PythonSnippets
Collection of useful python snippets

## Data Structures
#### List comprehension
```python
[f(x) for x in xs]
[f(x) for x in xs if is_g(x)]
[f(x) for xs in xss for x in xs]

[f(x, y) for (x, y) in zip(xs, ys)]

#sort unique elements of a list
sorted(list(set(xs)))
```
#### Dictionary comprehension
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
## IO operations
#### Serialize, Deserialize
```python
json, yaml
```
#### Path
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
## Processes and Parallel
#### Process
```python
#Use setproctitle to set title for python process, useful when using ps to know which process to be killed.
import setproctitle
setproctitle(title)
getproctitle() #Return current process title
```
## Jupyter
```python
!%matplotlib inline
!%config IPCompleter.greedy=True  #Press Tab to get autocomplete
```
## Networking
#### Consuming REST API
```
import requests
params = {'param_1': 1, 'param_2': 2}
r = requests.get('https://api.github.com/events', params, auth=(username, password))
r = requests.post('http://httpbin.org/post', data = {'key':'value'})
r = requests.put('http://httpbin.org/put', data = {'key':'value'})
r = requests.delete('http://httpbin.org/delete')
r = requests.head('http://httpbin.org/get')
r = requests.options('http://httpbin.org/get')
```

## Environement Management
#### Pip requirements.txt
```bash
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
