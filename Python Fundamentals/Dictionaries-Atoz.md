# Python Dictionaries: Basic to Advanced Concepts

Dictionaries are one of Python's most powerful and versatile data structures. They store mappings between keys and values in a highly efficient way. Let's explore dictionaries from basic concepts to advanced usage patterns.

## Basic Dictionary Concepts

### Creating Dictionaries

```python
# Empty dictionary
empty_dict = {}
empty_dict2 = dict()

# Dictionary with initial values
person = {
    "name": "John",
    "age": 30,
    "city": "New York"
}

# Creating with dict() constructor
person2 = dict(name="Alice", age=25, city="Boston")

# From sequences of key-value pairs
items = [("name", "Bob"), ("age", 35), ("city", "Chicago")]
person3 = dict(items)
```

### Accessing Values

```python
person = {"name": "John", "age": 30, "city": "New York"}

# Using square brackets (raises KeyError if key doesn't exist)
name = person["name"]  # "John"

# Using get() method (returns None or default value if key doesn't exist)
age = person.get("age")  # 30
country = person.get("country")  # None
country = person.get("country", "USA")  # "USA" (default value)
```

### Modifying Dictionaries

```python
person = {"name": "John", "age": 30}

# Adding or updating key-value pairs
person["city"] = "New York"  # Add new key-value pair
person["age"] = 31  # Update existing value

# update() method to add multiple key-value pairs
person.update({"email": "john@example.com", "phone": "555-1234"})
person.update(country="USA", zip_code="10001")

print(person)
# {'name': 'John', 'age': 31, 'city': 'New York', 'email': 'john@example.com', 'phone': '555-1234', 'country': 'USA', 'zip_code': '10001'}
```

### Removing Items

```python
person = {"name": "John", "age": 30, "city": "New York", "email": "john@example.com"}

# pop() removes a key and returns its value
email = person.pop("email")  # "john@example.com"
print(person)  # {'name': 'John', 'age': 30, 'city': 'New York'}

# popitem() removes and returns the last inserted key-value pair (Python 3.7+)
last_item = person.popitem()  # ("city", "New York")
print(person)  # {'name': 'John', 'age': 30}

# del statement
del person["age"]
print(person)  # {'name': 'John'}

# clear() removes all items
person.clear()
print(person)  # {}
```

### Dictionary Methods

```python
person = {"name": "John", "age": 30, "city": "New York"}

# keys(), values(), and items() methods
keys = person.keys()  # dict_keys(['name', 'age', 'city'])
values = person.values()  # dict_values(['John', 30, 'New York'])
items = person.items()  # dict_items([('name', 'John'), ('age', 30), ('city', 'New York')])

# Note: These return view objects that dynamically reflect dictionary changes
person["country"] = "USA"
print(keys)  # dict_keys(['name', 'age', 'city', 'country'])

# Checking for keys
if "name" in person:
    print("Name exists")

# copy() creates a shallow copy
person_copy = person.copy()
```

## Intermediate Dictionary Concepts

### Dictionary Comprehensions

```python
# Creating a dictionary with dictionary comprehension
squares = {x: x*x for x in range(6)}
print(squares)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# Conditional dictionary comprehension
even_squares = {x: x*x for x in range(10) if x % 2 == 0}
print(even_squares)  # {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}

# Transforming dictionaries
prices = {"apple": 0.40, "banana": 0.50, "orange": 0.45}
double_prices = {item: price*2 for item, price in prices.items()}
print(double_prices)  # {'apple': 0.8, 'banana': 1.0, 'orange': 0.9}

# Creating dictionary from two lists
keys = ["a", "b", "c"]
values = [1, 2, 3]
mapped = {k: v for k, v in zip(keys, values)}
print(mapped)  # {'a': 1, 'b': 2, 'c': 3}
```

### Nested Dictionaries

```python
# Nested dictionaries
employees = {
    "John": {
        "id": 1001,
        "position": "Developer",
        "salary": 85000
    },
    "Alice": {
        "id": 1002,
        "position": "Designer",
        "salary": 80000
    }
}

# Accessing nested values
print(employees["John"]["position"])  # "Developer"

# Adding nested dictionary
employees["Bob"] = {"id": 1003, "position": "Manager", "salary": 95000}

# Updating nested values
employees["John"]["salary"] = 90000

# Accessing with get() to handle missing keys safely
alice_info = employees.get("Alice", {})
email = alice_info.get("email", "No email provided")
```

### Default Dictionaries

```python
from collections import defaultdict

# defaultdict provides default values for missing keys
# This counts word frequencies without checking if keys exist
word_counts = defaultdict(int)
words = ["apple", "banana", "apple", "orange", "banana", "apple"]

for word in words:
    word_counts[word] += 1

print(word_counts)  # defaultdict(<class 'int'>, {'apple': 3, 'banana': 2, 'orange': 1})

# defaultdict with other types
default_list = defaultdict(list)
default_list["fruits"].append("apple")
default_list["fruits"].append("banana")
print(default_list)  # defaultdict(<class 'list'>, {'fruits': ['apple', 'banana']})

# Using a factory function
def default_factory():
    return {"count": 0, "items": []}

tracker = defaultdict(default_factory)
tracker["apples"]["count"] = 3
tracker["apples"]["items"].append("Granny Smith")
print(tracker)  # defaultdict(<function default_factory>, {'apples': {'count': 3, 'items': ['Granny Smith']}})
```

### OrderedDict (Pre-Python 3.7)

```python
from collections import OrderedDict

# In Python 3.7+, regular dicts maintain insertion order
# OrderedDict is still useful for operations that depend on order

# Creating OrderedDict
ordered = OrderedDict([('apple', 5), ('banana', 3), ('orange', 2)])

# Reordering by moving to end
ordered.move_to_end('apple')
print(ordered)  # OrderedDict([('banana', 3), ('orange', 2), ('apple', 5)])

# Deleting and re-inserting changes order
ordered.pop('banana')
ordered['banana'] = 4
print(ordered)  # OrderedDict([('orange', 2), ('apple', 5), ('banana', 4)])

# Equality checks consider order
dict1 = OrderedDict([('a', 1), ('b', 2)])
dict2 = OrderedDict([('b', 2), ('a', 1)])
print(dict1 == dict2)  # False (different order)
```

## Advanced Dictionary Concepts

### Dictionary Merging (Python 3.9+)

```python
# Merging dictionaries with | operator (Python 3.9+)
dict1 = {"a": 1, "b": 2}
dict2 = {"b": 3, "c": 4}
merged = dict1 | dict2
print(merged)  # {'a': 1, 'b': 3, 'c': 4}  (dict2's 'b' takes precedence)

# Updating with |= operator
dict1 |= dict2
print(dict1)  # {'a': 1, 'b': 3, 'c': 4}

# Pre-Python 3.9 method:
dict1 = {"a": 1, "b": 2}
dict2 = {"b": 3, "c": 4}
merged = {**dict1, **dict2}  # unpacking
print(merged)  # {'a': 1, 'b': 3, 'c': 4}
```

### Dictionary Views and Set Operations

```python
dict1 = {"a": 1, "b": 2, "c": 3}
dict2 = {"b": 20, "c": 30, "d": 40}

# Keys view object supports set operations
keys1 = dict1.keys()
keys2 = dict2.keys()

# Set operations on views
print(keys1 & keys2)  # {'b', 'c'} (intersection)
print(keys1 | keys2)  # {'a', 'b', 'c', 'd'} (union)
print(keys1 - keys2)  # {'a'} (difference)
print(keys1 ^ keys2)  # {'a', 'd'} (symmetric difference)

# Items view also supports set-like operations if values are hashable
items1 = dict1.items()
items2 = dict2.items()
print(items1 & items2)  # {('c', 3)} - only common key-value pairs
```

### Custom Dictionaries by Subclassing

```python
class HistoryDict(dict):
    """Dictionary that maintains history of changes"""
    
    def __init__(self, *args, **kwargs):
        self.history = []
        super().__init__(*args, **kwargs)
    
    def __setitem__(self, key, value):
        # Record history of changes
        if key in self:
            old_value = self[key]
            self.history.append((key, old_value, value))
        else:
            self.history.append((key, None, value))
        # Call the superclass method
        super().__setitem__(key, value)
    
    def get_history(self):
        return self.history

# Using our custom dictionary
hd = HistoryDict(a=1, b=2)
hd['a'] = 10
hd['c'] = 3
hd['b'] = 20

print(hd)  # {'a': 10, 'b': 20, 'c': 3}
print(hd.get_history())  # [('a', 1, 10), ('c', None, 3), ('b', 2, 20)]
```

### ChainMap - Multiple Dictionary View

```python
from collections import ChainMap

# ChainMap combines multiple dictionaries without copying
defaults = {'color': 'red', 'user': 'guest'}
user_settings = {'color': 'blue'}

settings = ChainMap(user_settings, defaults)
print(settings['color'])  # 'blue' (from user_settings)
print(settings['user'])   # 'guest' (from defaults)

# Adding a new dictionary to the chain
command_line_args = {'color': 'green', 'output': 'verbose'}
settings = ChainMap(command_line_args, user_settings, defaults)
print(settings['color'])  # 'green' (highest priority)

# Mutations affect the first dictionary in the chain
settings['color'] = 'yellow'
print(command_line_args)  # {'color': 'yellow', 'output': 'verbose'}
```

### Counter Dictionary

```python
from collections import Counter

# Counter is a specialized dictionary for counting
inventory = Counter(['apple', 'banana', 'apple', 'orange', 'banana', 'apple'])
print(inventory)  # Counter({'apple': 3, 'banana': 2, 'orange': 1})

# Adding more items to count
inventory.update(['apple', 'mango', 'pear'])
print(inventory)  # Counter({'apple': 4, 'banana': 2, 'orange': 1, 'mango': 1, 'pear': 1})

# Most common elements
print(inventory.most_common(2))  # [('apple', 4), ('banana', 2)]

# Mathematical operations
inventory1 = Counter(apples=3, oranges=1)
inventory2 = Counter(apples=1, bananas=2)
print(inventory1 + inventory2)  # Counter({'apples': 4, 'bananas': 2, 'oranges': 1})
print(inventory1 - inventory2)  # Counter({'apples': 2, 'oranges': 1})
```

### Using dictionaries as caches or memoization

```python
# Using dictionary for memoization (caching function results)
def fibonacci_memo(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fibonacci_memo(n-1, memo) + fibonacci_memo(n-2, memo)
    return memo[n]

print(fibonacci_memo(100))  # Very fast, without memoization this would take forever

# Better approach using functools.lru_cache
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(100))  # Still very fast with proper caching
```

## Dictionary Performance Considerations

### Time Complexity

Operation | Average Case | Amortized Worst Case
--- | --- | ---
Access | O(1) | O(n)
Insert | O(1) | O(n)
Delete | O(1) | O(n)
Search | O(1) | O(n)

```python
# Dictionary lookups are much faster than list lookups for large data
import time

# Setup
data_size = 1000000
lookup_key = 500000

# Dictionary lookup
my_dict = {i: f"value_{i}" for i in range(data_size)}
start_time = time.time()
result = my_dict[lookup_key]
dict_time = time.time() - start_time

# List lookup (linear search)
my_list = [(i, f"value_{i}") for i in range(data_size)]
start_time = time.time()
for item in my_list:
    if item[0] == lookup_key:
        result = item[1]
        break
list_time = time.time() - start_time

print(f"Dictionary lookup: {dict_time:.10f} seconds")
print(f"List lookup: {list_time:.10f} seconds")
print(f"Dictionary is {list_time/dict_time:.0f}x faster")
```

### Memory Usage

```python
import sys

# Compare memory usage of dictionary vs list for same data
data = [("key1", "value1"), ("key2", "value2"), ... ("key1000", "value1000")]
dict_data = dict(data)
list_data = data

dict_size = sys.getsizeof(dict_data) + sum(sys.getsizeof(k) + sys.getsizeof(v) for k, v in dict_data.items())
list_size = sys.getsizeof(list_data) + sum(sys.getsizeof(k) + sys.getsizeof(v) for k, v in list_data)

print(f"Dictionary size: {dict_size} bytes")
print(f"List size: {list_size} bytes")
```

## Real-World Applications

### JSON Processing

```python
import json

# Converting Python dict to JSON string
person = {
    "name": "John",
    "age": 30,
    "city": "New York",
    "languages": ["Python", "JavaScript", "C++"],
    "is_employee": True,
    "address": {
        "street": "123 Main St",
        "zip": "10001"
    }
}

json_str = json.dumps(person, indent=4)
print(json_str)

# Converting JSON to Python dict
parsed_data = json.loads(json_str)
print(parsed_data["address"]["street"])  # "123 Main St"

# Writing dict to JSON file
with open("person.json", "w") as f:
    json.dump(person, f, indent=4)

# Reading JSON from file
with open("person.json", "r") as f:
    loaded_person = json.load(f)
```

### Configuration Management

```python
# Using dictionaries for configuration settings
default_config = {
    "database": {
        "host": "localhost",
        "port": 5432,
        "user": "admin",
        "password": "default_password"
    },
    "api": {
        "version": "v1",
        "rate_limit": 100,
        "timeout": 30
    },
    "logging": {
        "level": "INFO",
        "file": "app.log"
    }
}

# Load user config and override defaults
user_config = {
    "database": {
        "host": "db.example.com",
        "password": "user_secret"
    },
    "logging": {
        "level": "DEBUG"
    }
}

# Merging configurations (simple approach)
def merge_configs(default, override):
    """Deep merge dictionaries with nested structures"""
    result = default.copy()
    
    for key, value in override.items():
        if isinstance(value, dict) and key in result and isinstance(result[key], dict):
            result[key] = merge_configs(result[key], value)
        else:
            result[key] = value
            
    return result

config = merge_configs(default_config, user_config)
print(config["database"]["host"])  # "db.example.com"
print(config["database"]["port"])  # 5432 (from default)
print(config["logging"]["level"])  # "DEBUG" (overridden)
```

### Graph Representation

```python
# Using dictionaries for graph representation (adjacency list)
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E']
}

# Depth-first search using dictionary graph
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()
    visited.add(start)
    print(start, end=' ')
    
    for neighbor in graph[start]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)

print("DFS traversal:")
dfs(graph, 'A')  # A B D E F C

# Breadth-first search
from collections import deque

def bfs(graph, start):
    visited = set([start])
    queue = deque([start])
    result = []
    
    while queue:
        vertex = queue.popleft()
        result.append(vertex)
        
        for neighbor in graph[vertex]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
    
    return result

print("\nBFS traversal:")
print(bfs(graph, 'A'))  # ['A', 'B', 'C', 'D', 'E', 'F']
```

## Best Practices for Using Dictionaries

1. **Use `get()` for safe access**:
   ```python
   # Instead of:
   value = my_dict[key] if key in my_dict else default
   
   # Use:
   value = my_dict.get(key, default)
   ```

2. **Use dictionary comprehensions for transformations**:
   ```python
   # Instead of:
   result = {}
   for k, v in my_dict.items():
       result[k] = transform(v)
   
   # Use:
   result = {k: transform(v) for k, v in my_dict.items()}
   ```

3. **Use `defaultdict` when building dictionaries with default values**:
   ```python
   # Instead of:
   groups = {}
   for key, value in items:
       if key not in groups:
           groups[key] = []
       groups[key].append(value)
   
   # Use:
   from collections import defaultdict
   groups = defaultdict(list)
   for key, value in items:
       groups[key].append(value)
   ```

4. **Consider `Counter` for frequency counts**:
   ```python
   # Instead of:
   counts = {}
   for item in items:
       counts[item] = counts.get(item, 0) + 1
   
   # Use:
   from collections import Counter
   counts = Counter(items)
   ```

5. **Use dictionary unpacking for merging**:
   ```python
   # Python 3.9+:
   merged = dict1 | dict2
   
   # Earlier versions:
   merged = {**dict1, **dict2}
   ```

6. **Use items() for iteration when you need both keys and values**:
   ```python
   # Instead of:
   for key in my_dict:
       value = my_dict[key]
       # process key and value
   
   # Use:
   for key, value in my_dict.items():
       # process key and value
   ```

7. **Remember that dictionary keys must be hashable**:
   
   - Lists and dictionaries can't be keys (they're mutable)
   - Tuples can be keys if all their elements are hashable
   - Custom objects need to implement `__hash__` and `__eq__` methods

### What Does "Hashable" Mean?

- A hashable object in Python is one that:
- Has a hash value that never changes during its lifetime (__hash__ method)
- Can be compared to other objects (__eq__ method)
- If a == b, then hash(a) == hash(b)

### Why Dictionary Keys Must Be Hashable

- Dictionaries use hash tables internally for fast lookups. When you use a key:
- Python computes its hash value
- Uses this hash to determine where to store the value
- For lookup, recomputes the hash to find the value quickly



