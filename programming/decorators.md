# DECORATORS

## Functions as First-Class Objects

- In Python, **first-class objects** are handled uniformly throughout - theu may be stored in data structures, passed as arguments or used in control structures.
- In python, functions are first-class objects, meaning that they have the following properties:
  - A function is an instance of the object type
  - You can store the function in a variable
  - You can pass the function as a parameter to another function
  - You can return the function from a function
  - You can store them in data structures, such as hash tables, lists etc.

### Ineer Functions

- It is possible to _define_ functions _inside other functions_.
- Such functions are called **inner functions**.
- Inner functions are not defined until the parent function is called, as they are locally scoped to the parent - i.e., they only exist inside the parent function as local variables.

## Decorators

- A decorator is a function that takes another function and extends the behaviour of that function without explicitly modifying the function.

### Basic Decorators Syntax

- In decorators, functions are taken as the argument into another function and then called inside the wrapper function, which is defined inside the decorator function. For example:

  ```python
  def my_decorator(function_to_be_used):

      def wrapper():
          print('This is before the function executes')
          function_to_be_used()
          print('This is after the function executes')

      return wrapper
  ```

- Now suppose we have another function that we want to decorate - we do this as follows:
  ```python
  @my_decorator
  def print_hello():
      print('Hello World')
  ```
- Now if we call this function, we will see the follwoing behaviour:
  ```python
  print_hello()
  >>> 'This is before the function executes'
  >>> 'Hello World'
  >>> 'This is after the function executes'
  ```

### Decorating Functions with Arguments

- If we want to dectorate a function that takes arguments, we need to make sure our decorator takes the same number of arguments. For example, if we wanted to decorate the following function
  ```python
  @my_decorator
  def square(x):
      return x ** 2
  # ^ THIS WONT WORK
  ```
  we would have to modify our decorator to take one argument, as it currently takes no positional aruments (i.e., the function `wrapper()` takes no arguments), but when we call `square(x)` we are passing to the decorator 1 argument.
- At the same time, we want our decorators to be reusable, so we use `*args` and `**kwargs` for the inner function.
- For example:

  ```python
  def my_decorator2(func_to_be_used):
      def wrapper(*args, **kwargs):
          print('Before function execution')
          func_to_be_used(*args, **kwargs)
          print('After function execution')
      return wrapper

  @my_decorator2
  def square(x):
      return x ** 2
  # ^ THIS WILL NOW WORK
  ```

### Returning Values from Decorated Functions

- To return a value from a decorated function, we need to make sure the wrapper function (i.e., the inner function) returns the return value of the function to be decorated.
- See the code below for how this works:
  ```python
  def my_decorator2(func_to_be_used):
      def wrapper(*args, **kwargs):
          print('Before function execution')
          return_value = func_to_be_used(*args, **kwargs)
          print('After function execution')
          return return_value
      return wrapper
  ```

### Using Functools

- Functools is a standard Python module for higher-order functions (functions that act on or return other functions).
- `wraps()` is a decorator that is applied to the wrapper function of a decorator, and it updates the properties of the wrapper function to look like the wrapped function by copying attributes such as `__name__`, `__doc__` (the docstring), etc.

  ```python
  # Without functools
  def decorate(f):
      def wrapper(*args, **kwargs):
          '''This is the wrapper function'''
          print('begin')
          val = f(*args, **kwargs)
          print('finished')
          return val

  @decorate
  def cubed(x):
      '''This returns the cube of a given number'''
      return x ** 3

  print(cubed(3).__doc__)
  >>> 'This is the wrapper function'

  # With functools
  import functools
  def decorate(f):

      @functools.wraps
      def wrapper(*args, **kwargs):
          '''This is the wrapper function'''
          print('begin')
          val = f(*args, **kwargs)
          print('finished')
          return val

  @decorate
  def cubed(x):
      '''This returns the cube of a given number'''
      return x ** 3

  print(cubed(3).__doc__)
  >>> 'This returns the cube of a given number'
  ```
