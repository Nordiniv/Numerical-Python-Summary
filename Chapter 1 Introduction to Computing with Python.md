# Chapter 1 Introduction to Computing with Python

## Why Python?

In computational problem-solving, it is, of course, important to consider the
performance of algorithms and their implementations. It is natural to strive for
efficient high-performance code, and optimal performance is indeed crucial for many
computational problems.
Python is considered a glue language, which means that it is used to connect multiple languages, like C, C++, and Fortran; hence it's able to have libraries -like BLAS- and packages -like SciPy- written in low-level languages to secure high performance.

## Environments for Computing with Python

There are many configurations of environments that can be used to run Python. The most common are:

* The Python interpreter or the IPython console to run code
interactively. Together with a text editor for writing code, this
provides a lightweight development environment
* The Jupiter Notebook, which is a web-based application that allows you to write and execute Python code. The Jupiter Notebook is available on most operating systems.
* The Spyder IDE, which is a graphical user interface (GUI) that allows you to write and execute Python code. Spyder is available on most operating systems.

Jupyter is preferred for exploratory computing and data analysis. Spyder is preferred for scientific computing and software development.

## The Python Interpreter and IPython Console

Python interpretter can execute code by typing `python filename.py` in the terminal. IPython is an enhanced version of the Python interpreter. It provides a more powerful interactive environment for Python. IPython can be started by typing `ipython` in the terminal.

### Input and Output caching

Input cells in python are denoted by In [ ]: and output cells are denoted by Out [ ]:.
Both the input and the output of previous cells can later be accessed through the In and Out variables that are automatically created by IPython. The In and Out
variables are a list and a dictionary, respectively, that can be indexed with a cell number.

#### Example

``` python
In [1]: 3 * 3; #semicolon suppresses output
In [2]: In[1]
Out[2]: '3 * 3;'
In [3]: Out[1]
    KeyError: 1
In [4]: In.insert(1, '9'); In #supresses output for what's before ;
Out[4]: ['', '9', '3 * 3;', 'In[1]', 'Out[1]', 'In']
In [5]: Out
Out[5]: {2: '3 * 3;', 4: ['', '9', '3 * 3;', 'In[1]', 'Out[1]', 'In', 'Out']}
```

### Autocompletion and Object Introspection

Autocompletion in IPython is contextual, and it will
look for matching variables and functions in the current namespace or among the attributes and methods of a class when invoked after the name of a class instance. For example, os.\<TAB> produces a list of the variables, functions, and classes in the os
module, and pressing TAB after having typed os.w results in a list of symbols in the os
module that starts with w:

``` python
In [7]: import os
In [8]: os.w<TAB>
os.wait os.wait3 os.wait4 os.waitpid os.walk os.write os.writev
```

### Documentation

Documentation can be accessed by typing ? after a function or class name. For example, the following command displays the documentation for the os.walk function:

``` python
In [9]: os.walk?
```

``` Markdown
Signature: os.walk(top, topdown=True, onerror=None, followlinks=False)
Docstring:
Directory tree generator.

For each directory in the directory tree rooted at top (including top
itself, but excluding '.' and '..'), yields a 3-tuple

    dirpath, dirnames, filenames
```

Docstrings can be specified for Python modules, functions, classes, and their attributes and methods. A well-documented module therefore includes a full API documentation in the code itself. From a developer’s point of view, it is convenient to be able to document a code together with the implementation. This encourages writing and maintaining documentation, and Python modules tend to be well documented. From a user’s point of view, it is convenient to be able to access the documentation from within the Python interpreter. This encourages reading the documentation, and Python users tend to be well informed. Shoutout to [this](https://www.python.org/dev/peps/pep-0257/) PEP.

### Interaction with the System Shell

This two-way communication with the IPython console and the system shell can be very convenient when, for example, processing data files. By way of illustration, Nordin was competing in a Kaggle competition and needed to download the data files from the competition page. He Kaggle CLI tool to download the data files, and then used the unzip command to extract the files:

``` python
In [10]: ! kaggle competitions download -c 'ieee-final-round'
In [11]: path = ! ls | grep zip
In [12]: ! unzip $path
```

Since most of work was done on Google Colab, other linux commands were very useful and could be accessed by typing ! before the command. Of course if colab's VM was running on Windows, the commands would be different.

### IPython Magic Commands

IPython provides a set of magic commands that can be used to control the behavior of the IPython console. Magic commands are prefixed with the % character. For example, the `%timeit` magic command can be used to time the execution of a Python statement and `%%timeit` can be used to time the execution of a whole cell. The following example shows how to use the `%timeit` magic command to time the execution of a Python statement:

``` python
In [13]: %timeit L = [n ** 2 for n in range(1000)]
```

``` Markdown
191 µs ± 782 ns per loop (mean ± std. dev. of 7 runs, 10000 loops each)
```

Check `%prun` for a similar functionality but with more detailed information.

Magic commands support `?` postfix to display documentation.

```python
In [1]: %prun?
Docstring:
Run a statement through the python code profiler.
```

[Python code profiler](https://docs.python.org/3/library/profile.html) is a tool that gives detailed information about what part of the computation takes more time.

Shoutout to Datacamp's course on [Writing Efficient Python Code](https://www.datacamp.com/courses/writing-efficient-python-code).

### File System Navigation

Ipython provides a set of magic commands that can be used to navigate the file system and are very similar to UNIX-like commands but system independent, therefore it can work on Windows as well as Linux.

`%ls` (list files), `%pwd` (return current working directory), `%cd` (change working directory), `%cp` (copy file), `%less` (show the content of a file in the pager), and `%%writefile filename` (write content of a cell to the file filename).

When `%automagic` is activated (type %automagic at the IPython prompt to toggle this feature), the % sign that precedes the IPython commands can be omitted, unless there is a name conflict with a Python variable or function. However, for clarity, the % signs are explicitly shown here.

### Running Scripts from the IPython Console

IPython can be used to run Python scripts. For example, the following command runs the script `script.py`:

``` python
In [14]: %run script.py #script.py contains some cool numerical analysis code.
```

all the variables and functions defined in the script are now available in the IPython console. a `-p` can be used to access the profiler.

``` python
In [15]: %who #list all all defined symbols (variables and functions).
```

``` Markdown
predcorr modEuiler Euiler rk4 
```

`%whos` is `%who` on steroids.

Shoutout to Nordin's [Numerical Methods Sheet Solution](https://github.com/Nordiniv/Numerical-Methods).

### `%debug`

After the traceback of an unintercepted exception has been printed to the IPython console, it is possible to step directly into the Python debugger using the IPython command %debug. This possibility can eliminate the need to rerun the program from the beginning using the debugger or after having employed the common debugging method of sprinkling print statements into the code. If the exception was unexpected and happened late in a time-consuming computation, this can be a big time-saver.

Type a question mark at the debugger prompt to show a [help](https://docs.python.org/3/library/pdb.html) menu that lists available commands:

``` markdown
ipdb> ?
```

### Reset

The `%reset -f` magic command can be used to reset the namespace to its initial state, (-f is a force flag). This is useful when you want to start over with a clean slate. Importing a module after resetting reenables a cached version of the module from the previous import. If this is not desired, the `%reset -f -s` magic command can be used to reset the namespace and also clear the cache.
