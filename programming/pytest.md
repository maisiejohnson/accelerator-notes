# TESTING WITH PYTEST

- Pytest is a python based testing framework, which is used to write and execute test codes.
- To test with pytest, we define test functions (who's names must start with 'test') and then run a command from the terminal to invoke pytest.
- Tests can be written in with the program code, or in a seperate file (the latter is more tidy). Pytest will automatically look for test functions in files that have a filename begining or ending with 'test'.
- A neat way to write tests is to have a dedicated test folder that contains files (beginning or ending with test) that contain all our test functions.

## Setting Up

- Put a `conftest.py` file in the root of the project. This file:
  - contains “global” settings for pytest, including mark registration and globally shared fixtures.
  - is responsible for giving pytest the scope- by putting the file in root, pytest will recognize the src module without needing to manually add it to PYTHONPATH

## Invoking Pytest

- We can run pytest with either of the following commands:

  ```console
  >>> pytest

  >>> python3 -m pytest
  ```

- The two commands above are almost equivalent, except that calling via python will also add the current directory to sys.path.

### Useful Command Line Flags Flags

- `-v` or `--verbose`: increases the verbosity level. The default level outputs a reasonable amount of information to debug most test failures. However when there are many differences between actual and expected data, some get hidden. In such cases pytest normally appends a message to the failure text such as:
  ```console
  ...Full output truncated (23 lines hidden), use '-vv' to show
  ```
  This tells us to see the hidden lines, we need to rerun the tests with verbosity level 2. To do this we can pass -v twice as `-v -v`, or more easily as `-vv`.
- `-k`: only run tests which match the given substring expression. An expression is a Python evaluatable expression where all names are substring-
  matched against test names and their parent classes. Example: `-k 'test_method or test_other'` matches all test functions and classes whose name contains 'test_method' or 'test_other', while `-k 'not test_method'` matches those that don't contain 'test_method' in their names. The matching is case-insensitive.
- `--full-trace`: Don't cut any tracebacks (default is to cut)
- `-h` or `--help`: Show help message and configuration info

## How Pytest Works

- Running pytest without mentioning a filename will run all files of format `test_*.py` or `*_test.py` in the current directory and subdirectories. Pytest automatically identifies those files as test files.
- We can make pytest run other filenames by explicitly mentioning them.
- Pytest requires the test function names to start with test. Function names which are not of format `test*` are not considered as test functions by pytest.

## Writing Simple Tests

Most functional tests follow the Arrange-Act-Assert model:

1. **Arrange** - this is where we set up the conditions for our test. This means pretty much everything except for the “act”. It’s lining up the dominoes so that the act can do its thing in one, state-changing step.
2. **Act** - this is the singular, state-changing action that kicks off the behavior we want to test. This behavior is what carries out the changing of the state of the system under test, and it’s the resulting changed state that we can look at to make a judgement about the behavior. This typically takes the form of a function/method call.
3. **Assert** - this is where we look at that resulting state and check if it looks how we’d expect after the dust has settled. The assert in our test is where we take that measurement/observation and check whether it aligns with what we expect.

For example:

```python
    def test_max_value():
        l = [1, 2, 3, 4, 5]
        assert max_value(l) == 5
```

## Fixtures

- In testing, a fixture provides a defined, reliable and consistent context for the tests.
- Fixtures define the steps and data that constitute the arrange phase of a test .
- In pytest, they are functions you define that serve this purpose.
- To use pytest fixtures, we need to import pytest into the test file.
- To mark a function as a pytest fixture, use the `@pytest.fixture decorator`. Then pass the name of the fixture function as an argument to the tests that we want to use it.
- If we want a given fixture to be used for all tests, we set `autouse = True` within the brackets of the fixture function.

  ```python
  import pytest


  class Fruit:
      def __init__(self, name):
          self.name = name
          self.cubed = False

      def cube(self):
          self.cubed = True

  class FruitSalad:
      def __init__(self, *fruit_bowl):
          self.fruit = fruit_bowl
          self._cube_fruit()

      def _cube_fruit(self):
          for fruit in self.fruit:
              fruit.cube()

  # Arrange
  @pytest.fixture
  def fruit_bowl():
      return [Fruit("apple"), Fruit("banana")]

  def test_fruit_salad(fruit_bowl):
      # Act
      fruit_salad = FruitSalad(*fruit_bowl)
      # Assert
      assert all(fruit.cubed for fruit in fruit_salad.fruit)
  ```

## Monkeypatching & Mocking

- Sometimes tests need to invoke functionality which depends on global settings or which invokes code which cannot be easily tested, e.g., where `print()` statements are involved, when we require user input, network access, etc.
- The `monkeypatch` fixture helps you to safely set/delete an attribute, dictionary item or environment variable, or to modify sys.path for importing.
- If we are using monkeypatching in a test, we need to pass `monkeypatch` (which is a built-in fixture) as an argument to the test.
- The `setattr` method of the `monkeypatch` fixture can be used to mock the output or behaviour of functions/ methods in the code we want to test.
- `monkeypatch.setattr()` takes the following arguments - `monkeypatch.setattr(target, name, value)`.
- For example:

  ```python
  import pytest
  import random

  def is_big_num(n=10):
      return 'BIG' if random.randint(0, 10) > 5 else 'NOT BIG'

  def test_is_big_num(monkeypatch):
      monkeypatch.setattr(random, 'randint', lambda x, y: 2)
      assert is_big_num() == 'NOT BIG'
  ```

- Note that when monkeypatching a function, the number of inputs to the `value` function must match that of the function that we are trying to monkeypatch.

### Dealing with One User Input

- We can mock user input using `monkeypatch`
- The syntax for this is either of the following

  1.  ```python
      import pytest
      import sys
      import io

      def test_my_function(monkeypatch):
        monkeypatch.setattr(sys,'stdin',io.StringIO('input str'))
        # rest of test here
        assert #assert statement here
      ```

  2.  ```python
      import pytest

      def tes_my_function(monkeypatch):
        monkeypatch.setattr('builtins.input', lambda x: 'input str')
        # rest of test here
        assert # assert statement here
      ```

      Note that the argument `x` is required in the `input_returns(x)` function, as the function which we are mocking, `builtins.input`, takes 1 argument.

### Dealine with More Than One User Input

- If me need to mock code that requires multiple user inputs, e.g., user input in a while loop, then we do this as follows:

  ```python
  import pytest

  def test_my_function(monkeypatch):
    input_values = ['input val 1', 'input val 2', ...]
    def input_returns(x):
        non local input_values
        val_to_return = input_values.pop(0)
        return val_to_return

    monkeypatch.setattr('builtins.input', input_returns)

    # rest of test here

    assert # assert statement here
  ```

- Note that the `non local ...` statement is required to modify the `input_values` list, which is in the enclosing scope (not the local scope).
- Also note that the argument `x` is required in the `input_returns(x)` function, as the function which we are mocking, `builtins.input`, takes 1 argument.

## Capturing Standard Output

- If we need to test that a function prints the correct thing, we can do this with pytest using `capsys`.
- The syntax is as follows:

  ```python
  import pytest

  def test_my_function(capsys):
    # arrange - set up context for test
    # act - call function that we expect to print something
    captured = capsys.readouterr()
    expected = 'string of what we expect to be printed'
    assert expected == captured.out
  ```

- Note that the `.out` part of `captured.out` is necessary in the assert statement because `capsys.readouterr()` returns a namedtuple with two attributes `out` (standard output) and `err` (standard error).

## Testing if a Function is Called Given Some Condition

- Suppose we have a function like the following:
  ```python
  def my_function():
    if condition == True:
        x = function1()
    else:
        x = function2()
    return x
  ```
- In this case, we ne need to test if the conditional statement works and produces the correct function call, given the conditional.
- In this case, we are not really interested in the return value of `my_function` but more so on if the correct function is called.
- We can achieve this with a monkeypatch as follows:

  ```python
  import pytest

  def test_my_function(monkeypatch):
    call_count = 0
    def counter(*args, **kwargs):
        non local call_count
        call_count += 1
        return val
    monkeypatch.setattr('function1', counter)

    # arrange - set up conditions for test
    # act - call required functions
    assert call_count = expected_val
  ```
