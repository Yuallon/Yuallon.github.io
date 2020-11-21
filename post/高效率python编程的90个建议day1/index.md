
### Preface

Here, I will write down my own notes of the book "*Effective Python: 90 Specific Ways to Write Better Python, 2nd Edition*". If you like, you can buy it or search its pdf on internet. I will try my best to refine the ideas in my article. Hope you will like my words.

Now, let's start!

### Item 1: Know Which Version of Python You're Using

You can figure out the version of Python you're using at runtime by these codes:

```
import sysy
print(sys.version_info)
print(sys.version)
```

Then, output will like these:

```
sys.version_info(major=3, minor=7, micro=4, releaselevel='final', serial=0)
3.7.4 (default, Aug 13 2019, 15:17:50) 
[Clang 4.0.1 (tags/RELEASE_401/final)]
```

#### Things to Remember

- Python 3 is the most up-to-date and well-supported version of Python, and you should use it for your projects.
- Be sure that the command-line **executable（实行的，执行的）** for running Python on your system is the version you expect it to be.
- Avoid Python 2, which is no longer be maintained since January 1, 2020.

### Item 2: Follow the PEP 8 Style Guide

[PEP 8 -- Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/), full-name is Python Enhancement Proposal #8, which is a style guide for how to format your Python code. You can write Python code any way you want, as long as it is valid in Python syntax. **However, using PEP-8 can make your code more readable for others.** When you work together with your co-worker and you will share your code each other. Code easier to read is important.

#### Whitespace

In Python, whitespace is syntactically significant. Python programmers are especially sensitive to the effects of whitespace on code **clarity**. Follow these guidelines related to whitespace:

- Use spaces instead of tabs or **indentation**.
- Use four space for each level of syntactically significant indenting.
- Lines should be 79 characters in length or less.
- Continuations of long expression onto additional lines should be indented by four extra spaces from their normal indentation level.
- In a file, functions and classes should be separated by two blank lines.
- In a class, methods should be separated by one line.
- In a dictionary, put no whitespace between each key and **colon**, and put a single space before the corresponding value if it fits on the same line.
- Put one -- and only one -- space before and after the = operator in a variable assignment. 
- For type **annotations**, ensure that there is no separation between the variable name and the colon, and use a space before the type information.

#### Naming

**PEP 8** suggests unique style of naming for different parts in Python. By this method, you can make it easy to distinguish which type corresponds to each name when reading code. Follow these guidelines related to naming:

- **Functions, variables, and attributes** should be in **lowcase_underscore** format.
- **Protected instance attributes** should be in **_leading_underscore** format.
- **Private instance attributes** should be in **__double_leading_underscore** format.
- **Classes** (including exceptions) should be in **CapitalizedWord** format.
- **Module-level** constants should be in **ALL_CAPS** format.
- **Instance methods** in classes should use **self**, which refers to the object, as the name of the first parameter.
- **Class methods** should use cls, which refers to the classes, as the name of the first parameter.

### Words

- **clarity**

  [adj] the quality of being clear and easy to understand 

- **indentation**

  [n] the space which starts a line of writing further from the left-hand side of the page than the other lines

- 