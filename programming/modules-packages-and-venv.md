# MODULES AND PACKAGES

- **Modular Programming** refers to the process of breaking a large prgramming task into seperate, smaller, more managable subtasks.
- Individual modules can then be grouped together to create a larger application.
- There are several advantages to this:

> 1. **Simplicity:** a module typically focuses on a relatively small portion of the task at hand, and thus when working on a single module you have a smaller problem domain to think about
> 2. **Maintainability:** we can write modules in a way that minimises interdependency with other modules and as such there is a smaller likelihood that changes to a single module will have an impact on other parts of the program.
> 3. **Reusability:** code defined in a single module can easily be reused by other parts of the application
> 4. **Scoping:** Modules typically define a seperate **namespace**, which helps to avoid collisions between object names in different areas of a program.

- We can also see the advanatages of modular programing with git aswell - the number of merge conflicts will be reduced if our code is split into several smaller files rather than having it all in one big file.

## Modules vs Packages

- A **module** is a file containing python code with the ".py" extension at the end of the file.
- A **package** is a shareable collection of python modules

## Modules

### Importing a Module

- If using a module within the current file/ module, it needs to be imported.
- It is standard to do this at the top of the file - makes things clearer
- Syntax for importing a whole module:
  > ```python
  > import <module-name>
  > ```
- Syntax for importing specific objects from a module:
  > ```python
  > from <module-name> import <obj-1>, <obj-2>, <obj-3>
  > ```
- When the import line is read, python executes the whole module, regardless of whether or not we have specified specific objects to be imported.
- if the same module is imported twice, python will only execute it once

### Running Modules Directly

- Modules can also be executed directly from the command line
- If there is code that we only want to be executed when the module is run directly, and not when the module is imported, then we can use the following syntax:
  > ```python
  > if __name__ == "__main__":
  >      x = "code to be executed when module is called directly goes here"
  > ```
- The code above is not executed when the module is imported because when a .py file is imported as a module, Python sets the special dunder variable `__name__` to the name of the module. However, if a file is run as a standalone script, `__name__` is set to the string `__main__`. Thus, we can distinguish which is the case at runtime using the conditional above and modify behaviour accordingly.

## Packages

- **Packages** are a way to organise related modules into a directory heirachy.
- This allows for more structured and modular organisation of code.
- If we put files into a directory structure then the **package name** is the name of the directory, and the **module names** are the names of the .py files.
- There are 2 types of packages: _standard packages_ and _namespace packages_.

### Standard Packages

- a standard package contains an `__init__.py` file (this can be empty) and one or more modules.
- In the same way as when we import a module python runs the entire module, when we import a package python runs the `__init__.py` file.
- The syntax to import a module from a package is:
  > ```python
  > from <package-name> import <module-name>
  > ```
- Like modules, packages can also be executed directly. To do this we create a `__main__.py` file containing the directly executable code. To run this file from the command line we then use the following syntax:
  > ```bash
  >  python3 -m <package-name>
  > ```
- If we want to use code from one of the package modules, or a different package module, in the `__main__.py` file, then said modules need to be imported.
- For a module in the current package we can either use _relative import_ or _full-path import_:
  > ```python
  > # relative import
  > import .<module-name>
  >
  > # full-path import
  > import <package-name>.<module-name>
  > ```

### Namespace Packages

- Namespace packages do NOT contain an `__init__.py` file and as such do not exhibit package behaviour related to this.
- Namespace packages are used purely to organise standard packages into a namespace.

### Nested Packages

- Suppose we have a package, package-2, nested within another package, package-1, as show below.

  > - `script.py`
  > - `-> package-1`
  >   > - `module-1-package-1.py`
  >   > - `module-2-package-2.py`
  >   > - `__init__.py`
  >   > - `-> package-2`
  >   >   > - `module-1-package-2.py`
  >   >   > - `module-2-package-2.py`
  >   >   > - `__init__.py`

- To import package 2, we use the following syntax:
  > ```python
  > from <package-1>.<package-2>.<module-1-package-2> import <obj>
  > ```
- This will initialise both package 1 and package 2, i.e., run the `__init__.py` file of both package-1 and package-2.
- To access the objects in package-1 however, we needa seperate import statement as whilst package-1 is initialised above (and its object names stored) a reference to it is not created until this package specifically is imported.

## PyPi

- central repository for packages
- use pip to download and manage packages from package repositories

## Managing Dependencies and Virtual Environments

- Pip installs packages locally into a centralised area (somewhere related to where python is installed) - this can cause problems if working on multiple projects, which may each have a different set of dependencies
- The solution to this problem is to use **_virtual environments_** using venv.
- It is good practice to make a new virtual environment for each project.
- When the virtual environment is activated, we can install dependencies into the virtual environment directly using pip, and this keeps them seperate from the global environment, and keeps the global environment seperate from the venv (what is going on here is reassignment of the python path variable when working within the virtual environment).
- To **create** a virtual environment:
  > ```python
  > # to create a virtual environment
  > python3 -m venv my-venv-name
  > # to activate the virtual environment
  > source my-venv-name/bin/activate
  > # to install python packages into the virtual environment
  > python3 -m pip install package-name
  > ```
- When developing packages we store the modules/ packaes that our package is dependent on in a `requirements.txt` file.
- To see which packages are installed in a virtual environment and save them to the requirements.txt file we can run the following command:
  > ```python
  > pip freeze > requirements.txt
  > ```
- The `pip freeze` command will tell us only the packages installed in the virtual environment, and not in the global environment.
- To install everything in the requirements file we can run the command:
  > ```python
  > pip install -r requirements.txt
  > ```
