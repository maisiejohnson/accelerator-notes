# FUNCTION ARGUMENTS

In Python, there a 3 common types of function arguments:

- **Positional arguments:** arguments that are called by their position in the function definition.
- **Keyword arguments:** arguments that are called by their name.
- **Default arguments:** arguments that are given default values.

### Positional Arguments

- The most straightforward way to pass arguments to a Python function is with **positional arguments**.
- In the function definition you specify a comma seperated list of of parameters.
- When the function is called you specify the corresponding list of arguments.
- The arguments passed to the function when it is called are then bound to the function parameters in the function definition in order.
- With positional arguments, the arguments in the call and the parameters in the definition must agree both in order and in number. For this reason, positional arguments are also called **required arguments**, as you can't leave any out when calling the function, nor can you specify extra ones.

### Keyword Arguments

- When calling a function, you can specify arguments in the form `<keyword> = <value>`.
- In this case, each `<keyword>` must exactly match a parameter in the function definition. Referencing a keyword that doesn't match any of the declared parameters generates an exception.
- Using keyword arguments lifts the restriction on argument order - each keyword argument explicitly designates a specific parameter by name, so you can specify them in any order.
- As with positional arguments, the number of arguments and parameters must still match.

  ```python
  def func(a, b, c, d):
      print(a, b, c, d)

  # the following code is not valid becuase positional arguments come after keyword arguments
  f(1, c=3, b=2, 4)

  >>> SyntaxError: 'positional argument follows keyword argument'

  # the following code is not valid as the positional arguments are not in sequential order
  f(1, 4, b=2, c=2)

  >>> TypeError: 'f() got multiple values for argument 'b''
  ```

- When positional and keyword arguments are both present, then the keyword arguments must come after the positional arguments. Furthermore, any positional arguments must be in sequential order without any positional arguments before the first keyword argument missing.

### Default Parameters

- If a parameter specified in a Python function definition has the form `<name> = <value>`, then `<value>` becomes a default value for that parameter.
- If this argument is left out when the function is called, then the argument assumes its default value.

Whilst these are the most common argument types, we can make functions more flexible by allowing for a variable number of arguments.

### Python Gotcha: Mutable Default Parameters

- Things can get weird if you specify a default parameter value that is a mutable object.
- This is because Python's deafult arguments are evaluated only once, and that is when the function is defined, not when the function is called.
- Thus, if a mutable default argument is mutated within the function body, then it is mutated for all future function calls. For example:

  ```python
  def f(x=[]):
      x.append('/')
      print(x)

  f()
  >>> '["/"]'

  f()
  >>> '["/","/"]'

  f()
  >>> '["/","/","/"]'
  ```

## Variable Number of Arguments:

- In Python there is an additional operator called the **unpacking operator** (`*`). The unpacking operator allows us to give our functions a variable number of positional or keyword arguments. These are conventionally referred to as `*args` and `**kwargs` respectively.

### Variable Number of Positional Arguments: `*args`

- `*args` allows us to pass a variable number of **positional arguments** to a function.
- Python packs up the `*arg` parameters into a tuple, which we can then reference in the function body by the name following the unpacking operator (in this case 'args'), which can be set to any value that we wish.
- When we call the function we then pass to the function any arguments that we wish to, seperated by commas.
- For example:
  ```python
    def sum_numbers(*numbers):
        result = 0
        for num in numbers:
            result += num
        return result
  ```

### Variable Number of Keyword Arguments: `**kwargs`

- `**kwargs` works just like args but instead of accepting positional arguments it accepts keyword arguments.
- Python packs up the `**kwarg` arguments into a dictionary, which we can then reference in the function body by the name followin the unpacking operator (in this case 'kwargs).
- When we call the function we pass in any number of arguments of the form `<keyword> = <value>`, seperated by commas.
- For example:
  ```python
    def print_key_value_pairs(**kwargs):
        for (key, value) in kwargs.items():
            print(f"{key}: {value}")
  ```

### Ordering Arguments in a Function

- If we want to include a combination of positional arguments, a variable number of positional arguments and a variable number of keyword arguments, then the correct order for the parameters in the function definition is:
  1. Standard arguments
  2. `*args` arguments
  3. `**kwargs` arguments
- For example, this function definition is correct:
  ```python
      def my_function(a, b, *args, **kwargs):
          pass
  ```

## Unpacking with the Asterix Operators: `*` & `**`

- The unpacking operators are operators that unpack the values from iterable objects in Python.
- The single asterix operator `*` can be used on any iterable that python provides, while the double asterix operator `**` can only be used on dictionaries.
- Below are some examples:

  ```python
  # unpacking a list and passing it to a function
  def my_sum(*args):
      result = 0
      for x in args:
          result += x
      return result

  l1 = [1, 2, 3]
  l2 = [4, 5]
  l3 = [6, 7, 8, 9]

  print(my_sum(*l1, *l2, *l3))
  >>> 45

  # splitting lists with unpacking operators
  l = [1, 2, 3, 4, 5, 6]
  a, *b, c = l

  print(a, b, c)
  >>> '1 [2, 3, 4, 5] 6'

  # merging lists
  list1 = [1, 2, 3]
  list2 = [4, 5, 6]
  merged_list = [*list1, *list2]

  print(merged_list)
  >>> '[1, 2, 3, 4, 5, 6]'

  # merging dictionaries
  d1 = {'A': 1, 'B': 2}
  d2 = {'C': 3, 'D': 4}
  merged_dict = {**d1, **d2}

  print(merged_dict)
  >>> '{"A": 1, "B": 2, "C": 3, "D": 4}'
  ```
