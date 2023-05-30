# 0x05 Python - Exceptions

- Errors and Exceptions: Until now error messages haven’t been more than mentioned, but if you have tried out the examples you have probably seen some. There are (at least) two distinguishable kinds of errors: syntax errors and exceptions.

1. Syntax Errors
- Syntax errors, also known as parsing errors, are perhaps the most common kind of complaint you get while you are still learning Python:

while True print('Hello world')
  File "<stdin>", line 1
    while True print('Hello world')
                   ^
SyntaxError: invalid syntax

- Exceptions
Even if a statement or expression is syntactically correct, it may cause an error when an attempt is made to execute it. Errors detected during execution are called exceptions and are not unconditionally fatal: you will soon learn how to handle them in Python programs. Most exceptions are not handled by programs, however, and result in error messages as shown here:

10 * (1/0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
>>> 4 + spam*3
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'spam' is not defined
>>> '2' + 2
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can only concatenate str (not "int") to str

The last line of the error message indicates what happened. Exceptions come in different types, and the type is printed as part of the message: the types in the example are ZeroDivisionError, NameError and TypeError. The string printed as the exception type is the name of the built-in exception that occurred. This is true for all built-in exceptions, but need not be true for user-defined exceptions (although it is a useful convention). Standard exception names are built-in identifiers (not reserved keywords).

The rest of the line provides detail based on the type of exception and what caused it.

The preceding part of the error message shows the context where the exception occurred, in the form of a stack traceback. In general it contains a stack traceback listing source lines; however, it will not display lines read from standard input.

Built-in Exceptions lists the built-in exceptions and their meanings.

- Handling Exceptions
It is possible to write programs that handle selected exceptions. Look at the following example, which asks the user for input until a valid integer has been entered, but allows the user to interrupt the program (using Control-C or whatever the operating system supports); note that a user-generated interruption is signalled by raising the KeyboardInterrupt exception.

>>>
while True:
    try:
        x = int(input("Please enter a number: "))
        break
    except ValueError:
        print("Oops!  That was no valid number.  Try again...")

The try statement works as follows.

First, the try clause (the statement(s) between the try and except keywords) is executed.

If no exception occurs, the except clause is skipped and execution of the try statement is finished.

If an exception occurs during execution of the try clause, the rest of the clause is skipped. Then, if its type matches the exception named after the except keyword, the except clause is executed, and then execution continues after the try/except block.

If an exception occurs which does not match the exception named in the except clause, it is passed on to outer try statements; if no handler is found, it is an unhandled exception and execution stops with a message as shown above.

A try statement may have more than one except clause, to specify handlers for different exceptions. At most one handler will be executed. Handlers only handle exceptions that occur in the corresponding try clause, not in other handlers of the same try statement. An except clause may name multiple exceptions as a parenthesized tuple, for example:

... except (RuntimeError, TypeError, NameError):
...     pass
A class in an except clause is compatible with an exception if it is the same class or a base class thereof (but not the other way around — an except clause listing a derived class is not compatible with a base class). For example, the following code will print B, C, D in that order:

class B(Exception):
    pass

class C(B):
    pass

class D(C):
    pass

for cls in [B, C, D]:
    try:
        raise cls()
    except D:
        print("D")
    except C:
        print("C")
    except B:
        print("B")
Note that if the except clauses were reversed (with except B first), it would have printed B, B, B — the first matching except clause is triggered.

When an exception occurs, it may have associated values, also known as the exception’s arguments. The presence and types of the arguments depend on the exception type.

The except clause may specify a variable after the exception name. The variable is bound to the exception instance which typically has an args attribute that stores the arguments. For convenience, builtin exception types define __str__() to print all the arguments without explicitly accessing .args.

>>>try:
    raise Exception('spam', 'eggs')
except Exception as inst:
    print(type(inst))    # the exception type
    print(inst.args)     # arguments stored in .args
    print(inst)          # __str__ allows args to be printed directly,
                         # but may be overridden in exception subclasses
    x, y = inst.args     # unpack args
    print('x =', x)
    print('y =', y)

<class 'Exception'>
('spam', 'eggs')
('spam', 'eggs')
x = spam
y = eggs
The exception’s __str__() output is printed as the last part (‘detail’) of the message for unhandled exceptions.
## Learning Objectives

At the end of this project, you are expected to be able to explain to anyone, without the help of Google:

## General
- Why Python programming is awesome
- What’s the difference between errors and exceptions
- What are exceptions and how to use them
- When do we need to use exceptions
- How to correctly handle an exception
- What’s the purpose of catching exceptions
- How to raise a builtin exception
- When do we need to implement a clean-up action after an exception

# Tasks
- 0-safe_print_list.py
- 1-safe_print_integer.py
- 2-safe_print_list_integers.py
- 3-safe_print_division.py
- 4-list_division.py
- 5-raise_exception.py
- 6-raise_exception_msg.py
- 100-safe_print_integer_err.py
- 101-safe_function.py
- 102-magic_calculation.py
- 103-python.c
