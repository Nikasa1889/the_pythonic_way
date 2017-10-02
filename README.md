# PythonSnippets
Collection of useful python snippets

# List comprehension
```python
[f(x) for x in xs]
[f(x) for x in xs if is_g(x)]
[f(x) for xs in xss for x in xs]
```

# Path
```python
# Change working directory to the script directory, so that open file will work with relative path
abspath = os.path.abspath(__file__)
dname = os.path.dirname(abspath)
os.chdir(dname)
```

# Jupyter
```python
!%matplotlib inline
!%config IPCompleter.greedy=True  #Press Tab to get autocomplete
```

# Consuming REST API
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
