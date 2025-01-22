# Comprehensive Python, Django, and DSA Guide

## Table of Contents
1. [Python Basics](#python-basics)
2. [Object-Oriented Programming](#oop)
3. [Data Structures](#data-structures)
4. [Algorithms](#algorithms)
5. [Django Framework](#django)
6. [Advanced Topics](#advanced)

## Python Basics <a name="python-basics"></a>

### Data Types
1. **Numeric Types**
   - int: `x = 5`
   - float: `y = 3.14`
   - complex: `z = 3 + 4j`

2. **Sequence Types**
   - list: `my_list = [1, 2, 3]`
   - tuple: `my_tuple = (1, 2, 3)`
   - range: `range(5)`

3. **Text Type**
   - str: `text = "Hello, World!"`

4. **Mapping Type**
   - dict: `my_dict = {"name": "John", "age": 30}`

5. **Set Types**
   - set: `my_set = {1, 2, 3}`
   - frozenset: `frozen = frozenset([1, 2, 3])`

6. **Boolean Type**
   - bool: `is_valid = True`

7. **None Type**
   - None: `value = None`

### Control Flow
```python
# If statements
if condition:
    pass
elif other_condition:
    pass
else:
    pass

# Loops
for item in iterable:
    pass

while condition:
    pass

# Exception handling
try:
    risky_operation()
except Exception as e:
    handle_error(e)
finally:
    cleanup()
```

### Functions
```python
# Basic function
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

# Lambda function
square = lambda x: x**2

# Decorator
def my_decorator(func):
    def wrapper():
        print("Before function")
        func()
        print("After function")
    return wrapper

@my_decorator
def my_function():
    print("Main function")
```

## Object-Oriented Programming <a name="oop"></a>

### Classes and Objects
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def greet(self):
        return f"Hello, my name is {self.name}"
    
    @property
    def is_adult(self):
        return self.age >= 18
```

### Inheritance
```python
class Employee(Person):
    def __init__(self, name, age, employee_id):
        super().__init__(name, age)
        self.employee_id = employee_id
    
    def get_details(self):
        return f"{self.name} (ID: {self.employee_id})"
```

### Polymorphism
```python
class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"
```

### Encapsulation
```python
class BankAccount:
    def __init__(self):
        self.__balance = 0  # Private attribute
    
    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
    
    def get_balance(self):
        return self.__balance
```

## Data Structures <a name="data-structures"></a>

### Arrays and Lists
```python
# Dynamic Array (List in Python)
numbers = [1, 2, 3, 4, 5]
numbers.append(6)      # O(1) amortized
numbers.insert(0, 0)   # O(n)
numbers.pop()          # O(1)
numbers.remove(3)      # O(n)
```

### Linked Lists
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
    
    def append(self, data):
        if not self.head:
            self.head = Node(data)
            return
        current = self.head
        while current.next:
            current = current.next
        current.next = Node(data)
```

### Stacks and Queues
```python
# Stack using list
class Stack:
    def __init__(self):
        self.items = []
    
    def push(self, item):
        self.items.append(item)
    
    def pop(self):
        return self.items.pop()
    
    def peek(self):
        return self.items[-1]

# Queue using collections.deque
from collections import deque
queue = deque()
queue.append(1)      # enqueue
queue.popleft()      # dequeue
```

### Trees
```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

class BinarySearchTree:
    def __init__(self):
        self.root = None
    
    def insert(self, value):
        if not self.root:
            self.root = TreeNode(value)
        else:
            self._insert_recursive(self.root, value)
    
    def _insert_recursive(self, node, value):
        if value < node.value:
            if node.left is None:
                node.left = TreeNode(value)
            else:
                self._insert_recursive(node.left, value)
        else:
            if node.right is None:
                node.right = TreeNode(value)
            else:
                self._insert_recursive(node.right, value)
```

## Algorithms <a name="algorithms"></a>

### Sorting Algorithms

#### Quick Sort
```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)
```

#### Merge Sort
```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    
    result.extend(left[i:])
    result.extend(right[j:])
    return result
```

### Searching Algorithms

#### Binary Search
```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1
```

### Graph Algorithms

#### Depth-First Search (DFS)
```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()
    
    visited.add(start)
    print(start)
    
    for neighbor in graph[start]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)
```

#### Breadth-First Search (BFS)
```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    visited.add(start)
    
    while queue:
        vertex = queue.popleft()
        print(vertex)
        
        for neighbor in graph[vertex]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

## Django Framework <a name="django"></a>

### Project Structure
```
myproject/
    manage.py
    myproject/
        __init__.py
        settings.py
        urls.py
        wsgi.py
    myapp/
        __init__.py
        admin.py
        apps.py
        models.py
        views.py
        urls.py
        tests.py
```

### Models
```python
from django.db import models

class Category(models.Model):
    name = models.CharField(max_length=100)
    slug = models.SlugField(unique=True)
    
    class Meta:
        verbose_name_plural = "categories"
    
    def __str__(self):
        return self.name

class Product(models.Model):
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    description = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
```

### Views
```python
from django.views.generic import ListView, DetailView
from rest_framework import viewsets
from .models import Product
from .serializers import ProductSerializer

# Class-based view
class ProductListView(ListView):
    model = Product
    template_name = 'products/list.html'
    context_object_name = 'products'

# REST Framework viewset
class ProductViewSet(viewsets.ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

### URL Configuration
```python
from django.urls import path, include
from rest_framework.routers import DefaultRouter
from . import views

router = DefaultRouter()
router.register(r'products', views.ProductViewSet)

urlpatterns = [
    path('', include(router.urls)),
    path('products/', views.ProductListView.as_view(), name='product-list'),
]
```

## Advanced Topics <a name="advanced"></a>

### Django REST Framework Features

#### Serializers
```python
from rest_framework import serializers
from .models import Product

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = ['id', 'name', 'price', 'description']
```

#### Permissions
```python
from rest_framework.permissions import BasePermission

class IsOwnerOrReadOnly(BasePermission):
    def has_object_permission(self, request, view, obj):
        if request.method in SAFE_METHODS:
            return True
        return obj.user == request.user
```

#### Authentication
```python
from rest_framework.authentication import TokenAuthentication
from rest_framework.permissions import IsAuthenticated

class SecureViewSet(viewsets.ModelViewSet):
    authentication_classes = [TokenAuthentication]
    permission_classes = [IsAuthenticated]
```

### Python Advanced Concepts

#### Context Managers
```python
class FileManager:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None
    
    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        self.file.close()
```

#### Generators
```python
def fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        yield a
        a, b = b, a + b
```

#### Metaclasses
```python
class Singleton(type):
    _instances = {}
    
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]

class Database(metaclass=Singleton):
    def __init__(self):
        self.connection = "Connected"
```

This guide serves as a comprehensive reference for Python programming, Django web development, and fundamental data structures and algorithms. Use it as a starting point for your development journey and refer back to it as needed.
