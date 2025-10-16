# Python-notes
## Module I: Introduction to Python & Data Types

This note covers the fundamental concepts of Python, from how it runs to the basic data types you'll use to build programs.

---

### How Python Programs Execute 🐍

When you write a program, you save it in a file, for example, `my_program.py`. But how does the computer understand this file? Python uses a multi-step process.

1. **Source Code (`.py` file)**: This is the human-readable code you write.
2. **Compilation to Bytecode (`.pyc` file)**: When you run your script, the Python interpreter first compiles your source code into a format called **bytecode**.
    - **What does byte code mean?** Bytecode is a low-level, platform-independent set of instructions. It's not machine code (like for C/C++), but it's an intermediate language that's easier and faster for a program to understand than your original source code.
    - **What do `x.py` and `x.pyc` mean?** `x.py` is your source code file. `x.pyc` is the compiled bytecode file that Python creates to speed up execution the next time you run the program.
3. **Execution by the PVM (Python Virtual Machine)**: The bytecode is then executed by the **Python Virtual Machine (PVM)**.
    - **How does the PVM work?** The PVM is the runtime engine of Python; it's the part that truly runs your program. It reads the bytecode instruction by instruction and executes it on the host machine. Because the PVM is a piece of software, it allows Python code to be cross-platform—you can run the same `.py` file on Windows, macOS, or Linux as long as they have Python installed.

An alternative Python implementation is **PyPy**, which uses a Just-In-Time (JIT) compiler to translate bytecode into native machine code, often resulting in much faster execution for long-running programs.

---

### Memory Management & Garbage Collection 🗑️

Python manages memory automatically, which makes programming much simpler.

- **Automatic Garbage Collection**: Yes, Python supports automatic garbage collection. It's a process where the interpreter automatically frees up memory that is no longer in use. This is crucial because it prevents common programming errors like memory leaks, allowing developers to focus on logic rather than manual memory management (unlike in C).
- **Reference Counting**: The primary way Python handles this is through **reference counting**. Every object in memory has a counter that tracks how many variables (references) are pointing to it. When this count drops to zero, the object is considered "garbage" and its memory is reclaimed.
- **Forced Garbage Collection**: While it's usually automatic, you can manually trigger the garbage collection process. This is known as **forced garbage collection**. You can do this by importing the `gc` module and calling `gc.collect()`. This is rarely needed but can be useful in specific memory-critical situations.

---

### Variables, Identifiers, and Scope

### Variables and Identity

In Python, a variable is not a container for a value, but rather a **name or label that references an object** in memory.

- **How does Python see a variable?** It sees a variable as a name pointing to an object. If you write `x = 100` and then `y = x`, both `x` and `y` point to the *exact same* integer object with the value 100.
- **Finding Data Type**: To check what type of object a variable is pointing to, you use the built-in `type()` function. For example, `type(100)` would return `<class 'int'>`.
- **Finding Identity**: To find the unique memory address of the object a variable refers to, you use the `id()` function. For example, `id(x)` will give you the unique identity of the object `x` is referencing.

### Identifiers and Naming Conventions

- **Identifiers**: An identifier is the name given to entities like variables, functions, and classes. Rules for identifiers are:
    1. They must start with a letter (a-z, A-Z) or an underscore (`_`).
    2. The rest of the name can consist of letters, numbers, and underscores.
    3. They are case-sensitive (`age` is different from `Age`).
    4. They cannot be a reserved keyword (like `if`, `for`, `def`).
- **Naming Conventions**:
    - **snake_case**: For variables and functions (`my_variable`, `calculate_age`).
    - **PascalCase**: For classes (`MyClassName`).

### Local vs. Global Variables

The **scope** of a variable determines where it can be accessed.

| **Feature** | **Local Variable** | **Global Variable** |
| --- | --- | --- |
| **Definition** | Defined inside a function. | Defined outside of all functions, in the main body of the script. |
| **Scope** | Accessible only within the function where it is defined. | Accessible throughout the entire program, both inside and outside functions. |
| **Lifetime** | Created when the function is called and destroyed when the function returns. | Created when the program starts and destroyed when the program ends. |

To modify a global variable from inside a function, you must use the **`global` keyword**.

**Example:**

Python

`count = 10  # This is a global variable

def my_function():
  global count  # Tells Python we want to use the global 'count'
  count = count + 1
  local_var = 5 # This is a local variable
  print(f"Inside function: Global count is {count}, Local var is {local_var}")

my_function()
print(f"Outside function: Global count is {count}")
# Trying to access local_var here would cause an error`

---

### Built-in Data Types

Python has several built-in data types to store different kinds of information.

### Numeric Types

- **`int`**: Whole numbers (e.g., `10`, `50`).
- **`float`**: Decimal numbers (e.g., `3.14`, `0.01`).
- **`complex`**: Complex numbers with real and imaginary parts (e.g., `3+4j`).

### Boolean Type (`bool`)

- The `bool` type represents one of two values: **`True`** or **`False`**. It's used for logical operations and control flow (e.g., in `if` statements).

### Sequence Types (Ordered)

- **Strings (`str`)**: A string is an immutable sequence of Unicode characters used to store text.
    - **Usage**: Strings are used for everything from storing a user's name to holding the content of a file.
    - **Example**: `my_college = "Mahatma Gandhi University"`
    - **Escape Characters**: Special characters that have a specific meaning, prefixed with a backslash (`\`). Common ones include `\n` (newline), `\t` (tab), `\\` (backslash), and `\"` (double quote).
    - **Formatted Strings (f-strings)**: A modern and easy way to embed expressions inside string literals. You prefix the string with an `f` and place variables inside curly braces `{}`.
        - `name = "Navaneeth"`
        - `greeting = f"Hello, {name}!"`
- **Lists (`list`)**: A mutable, ordered sequence of items. "Mutable" means you can change its contents (add, remove, or modify elements).
    - **Example**: `my_grades = [85, 92, 78, 92]`
- **Tuples (`tuple`)**: An immutable, ordered sequence of items. "Immutable" means once a tuple is created, you cannot change its contents.
    - **Example**: `coordinates = (10.0, 20.5)`

### Set Types (Unordered)

- **Set (`set`)**: An unordered collection of **unique** items. Duplicates are automatically removed. They are mutable.
    - **Example**: `unique_numbers = {1, 2, 3, 4, 3, 2}` (will be stored as `{1, 2, 3, 4}`)
- **Frozenset (`frozenset`)**: An immutable version of a set. Because it's unchangeable, a frozenset can be used as a key in a dictionary, whereas a regular set cannot.

### Mapping Type

- **Dictionary (`dict`)**: An unordered collection of **key-value pairs**. It's mutable and very useful for storing related data.
    - **Example**: `student = {"name": "Navaneeth", "course": "Cyber Forensics"}`

---

### User-Defined Data Types

While Python provides many built-in types, you can also create your own. **User-defined data types** are created using the **`class`** keyword. A class is a blueprint for creating objects, allowing you to bundle data (attributes) and functionality (methods) together. This is the foundation of Object-Oriented Programming (OOP).

**Example:**

Python

`class Student:
  def __init__(self, name, roll_no):
    self.name = name
    self.roll_no = roll_no

# Creating objects (instances) of the Student class
student1 = Student("Navaneeth", 101)
student2 = Student("Ajmal", 102)`

---

### Modules and Packages 📦

- **Module**: A module is a single Python file (`.py`) containing statements and definitions. It helps you logically organize your code. You can use the code from one module in another file by using the `import` statement.
- **Package**: A package is a collection of modules. In simple terms, it's a directory containing modules and a special `__init__.py` file (which can be empty). Packages allow for a hierarchical structuring of the module namespace.

---

### Comparison: Python vs. C

| **Feature** | **Python** | **C** |
| --- | --- | --- |
| **Typing** | **Dynamic**: Type is checked at runtime. | **Static**: Type must be declared and is checked at compile time. |
| **Memory Management** | **Automatic**: Garbage collection handles memory. | **Manual**: Programmer must allocate and deallocate memory (`malloc`, `free`). |
| **Execution** | **Interpreted**: Slower, but more portable. | **Compiled**: Very fast, compiled to native machine code. |
| **Syntax** | **Simple & Readable**: Closer to English, requires less code. | **Complex & Verbose**: Requires more code for the same task (e.g., semicolons, braces). |
| **Use Case** | Web development, data science, scripting, AI/ML. | System programming, embedded systems, OS development. |
