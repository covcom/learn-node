
# Handling Errors

Work through before first lab in Teaching Week 7
Author: Dr Matthew England (Coventry University)
Contents
1 System tools 2
1.1 Standard Streams . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 2
1.2 Interpreter Arguments . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 3
2 Exceptions 4
2.1 Handling Exceptions . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 4
2.2 Raising Exceptions . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 6
3 Exercises 7
4 Common errors 7
1
121COM: Introduction to Computing Worksheet 7: Exceptions
1 System tools
The sys module provides access to variables used by, and functions to interact with, the interpreter. We
highlight two particularly useful features here and refer to the online documentation for the rest.
https://docs.python.org/3.4/library/sys.html
1.1 Standard Streams
These are the three standard pre-connected Input / Output (I/O) communication channels:
stdin: Standard Input - for passing data into Python;
stdout: Standard Output - for passing data out of Python;
stderr: Standard Error - for passing error messages out of Python.
The stdin stream is connected to the keyboard with the stdout and stderr streams connected to the
environment that launches the Python Interpretor (such as IDLE, another IDE or the command line shell).
We have used the streams already: print uses the stdout stream and input the stdin stream.
The sys module defines a data type for each stream. These behave like the file objects returned by the
open function (see Week 6 notes). In particular, there are methods to read from stdin and write to stdout.
>>> import sys
>>> sys.stdout.write("Hello")
Hello5
The character 5 at the end of the output is not a typo. The function write:
❼ writes the input string to the stdout stream as a function side effect; and
❼ returns as output the length of the input string (5 characters in this case).
When we run functions in the interactive interpretor session Python prints their output and so the function
performs both these actions to give the output as shown.
>>> x = sys.stdin.read()
hello
is anything happening?
what is going on?
Executing the read function in the above code starts Python reading input from the stdin stream (the
keyboard). This will continue uninterrupted until Python reads an end of file character (even if we enter
newlines). Pressing Ctrl+D (the control and D key at the same time) will generate this character on most
system (allowing you to exit the sequence without closing Python).
The following Python script demonstrates how we can redirect output to a file (very useful if the output
is valuable or produced too quickly to read at the time). Note that before redirecting the script saves the
location of the normal stdout stream so that we can easily return to the default settings!
Redirect.py
1 import sys
2 print (" Message 1")
3 saveOutLocation = sys . stdout
4 f = open (✬out .log ✬, ✬w✬)
5 sys . stdout = f
6 print (" Message 2")
7 sys . stdout = saveOutLocation
8 f . close ()
2
121COM: Introduction to Computing Worksheet 7: Exceptions
If you run the script the only output is Message 1 but if you check the directory you are working in
there should be a file out.log with a single line reading Message 2.
We note that there are easier ways of redirecting output when running Python from the command line
(a linux bash shell could do this in a single line for example).
1.2 Interpreter Arguments
The sys module gives users access to a variable argv assigned to a list. When accessed while running a
script the first entry argv[0] is the file name of the script.
PythonArguments.py
1 import sys
2 n = len( sys . argv )
3 print (" Length of argv : ", n )
4 for i in range ( n ):
5 if i ==0:
6 print (" File Name : ", sys . argv [ i ])
7 else :
8 print (" Argument " + str( i ) , sys . argv [ i ])
If the above script was run without arguments (as all scripts we have been running so far are) then it
would print two lines:
Length of argv: 1
File Name: <FilePath>\PythonArguments.py
where <FilePath> is the location of the script on the computer.
Like a function, a script can be run with arguments which is useful if the values of certain data are not
known at the time of writing the code, or if a script is to be used multiple times on different data. The
arguments are passed into Python alongside the name of the script to be run: they are then assigned to the
parameters argv[1], argv[2], argv[3], and so on.
It is not possible to run a script with arguments in IDLE: IDLE is a tool for working exclusively in
Python, while running Python with arguments is only required when working with multiple programs. To
run Python on a script with arguments from the command line (obtained by entering cmd at the Start Menu
in Windows) we write python, then a space, then name of the file, then the arguments all separated by space.
We consider running the following from command line (as indicated by the different prompt $$$ rather than
>>> we use for the Python interactive interpretor prompt).
$$$ python PythonArguments.py Hello "How Are You"
Then we should receive output
Length of argv: 3
File Name: PythonArguments.py
Argument 1: Hello
Argument 2: How Are You?
Note that the second arguments is interpreted as a single argument string since we enclosed it in quotes.
3
121COM: Introduction to Computing Worksheet 7: Exceptions
2 Exceptions
Runtime errors are sometimes called exceptions because they often mean something exceptional has happened.
When a runtime error is triggered in Python an error message is generated which consists of two
parts, the error type and a more specific message, separated by a colon.
>>> y = x**2
Traceback (most recent call last):
File "<pyshell#6>", line 1, in <module>
y = x**2
NameError: name ’x’ is not defined
In the above example a runtime error occurred because x was used before it was assigned. The error
message is the final line; the error type NameError and the error message name ’x’ is not defined. The
three lines above the error message are the traceback. The traceback is useful for locating errors when code
is spread over several files.
2.1 Handling Exceptions
When a runtime error occurs the default behaviour is for the program to halt with the error message printed
to stderr. However, it may be possible to ”handle” this exception and have the program continue, using
the try and except keywords. Consider the following script.
Distribute1.py
1 try :
2 # Script to evenly distribute
3 n = input ("How many people ? ")
4 pc = 100/ int ( n )
5 print (" Everyone gets " + str( pc ) + "%")
6 except ZeroDivisionError :
7 print ("No one gets anything ")
Try running the code and entering different values when prompted. The first block (following try)
gets executed each time; if the user enters a positive integer then the percentage is printed and the second
code block (following except) is never run; but if they enter 0 then instead of dividing by zero in line 4
and printing the error message Python executes the second code block, following except. We say that the
ZeroDivisionError has been caught.
Try running the code again and this time enter two when prompted. This will trigger the following error
message: ValueError: invalid literal for int() with base 10: ’two’. This time the error was
not of type ZeroDivisionError and so not caught. We could catch this exception also by using a tuple of
error types instead of just one after except.
Distribute2.py
1 try :
2 # Script to evenly distribute
3 n = input ("How many people ? ")
4 pc = 100/ int ( n )
5 print (" Everyone gets " + str( pc ) + "%")
6 except ( ZeroDivisionError , ValueError ):
7 print (" Unacceptable Input ")
4
121COM: Introduction to Computing Worksheet 7: Exceptions
Alternatively, we can have multiple except blocks so we can handle the different error types individually.
Distribute3.py
1 try :
2 n = input ("How many people ? ")
3 pc = 100/ int ( n )
4 print (" Everyone gets " + str( pc ) + "%")
5 except ZeroDivisionError :
6 print ("No one gets anything ")
7 except ValueError :
8 print (" Unacceptable Input ")
Note that only one except block can ever be executed in each run (relating to the first runtime error
triggered in the code block after try).
We may want to use information from the error message. In this case we use the as keyword to assign
the error message to a variable.
Distribute4.py
1 try :
2 n = input ("How many people ? ")
3 pc = 100/ int ( n )
4 print (" Everyone gets " + str( pc ) + "%")
5 except ZeroDivisionError :
6 print ("No one gets anything ")
7 except ValueError as err :
8 print ("You triggered a ValueError with message : ")
9 print ( err )
We can use the except line without declaring any error type. This will now catch all runtime errors. It
should be used with extreme caution since it could mask important problems.
Distribute5.py
1 try :
2 n = input ("How many people ? ")
3 pc = 100/ int ( n )
4 print (" Everyone gets " + str( pc ) + "%")
5 except :
6 print (" Something bad happened !")
When using except without an error type it should be the last except clause (as any others following it
would never get executed). One common use of a try-except statement is to ensure files are always closed
properly. However, Python has a better way to achieve this: a finally statement which would get executed
under all circumstances (whether exception is triggered or not).
Distribute6.py
1 f = open ("out.txt", "w")
2 print (" File Open ")
3 try :
4 n = input ("How many people ? ")
5 pc = 100/ int ( n )
6 f . write (str( pc ))
7 finally :
8 f . close ()
9 print (" File Closed ")
Note that even when the user inputs 0 the message File Closed is still printed.
5
121COM: Introduction to Computing Worksheet 7: Exceptions
We can combine finally with except as follows.
Distribute7.py
1 f = open ("out.txt", "w")
2 print (" File Open ")
3 try :
4 n = input ("How many people ? ")
5 pc = 100/ int ( n )
6 f . write (str( pc ))
7 except ZeroDivisionError :
8 print ("No one gets anything ")
9 finally :
10 f . close ()
11 print (" File Closed ")
Only one except clause ever gets executed, but in all cases the finally clause is executed.
If a ZeroDivisionError is triggered the code handles it; appropriate since it is an exceptional case where
the function is not required to do anything. However, if a ValueError occurs then the exception is allowed
to rise to the user; appropriate since the function was used incorrectly: it was not exceptional behaviour but
a real mistake. In this case the program halts and the error sent to stderr, but not before the file is closed.
2.2 Raising Exceptions
If your program detects an error condition, you can make it raise an exception of its own using the raise
keyword. The keyword should be followed by an exception. We can use the built in exception types detailed
in the documentation at the link below.
https://docs.python.org/3.4/library/exceptions.html
Consider the following example. Note that the input to NameError becomes the detailed error message sent
to stderr. Raising an exception is sometimes called throwing an exception.
Day.py
1 def numToDay ( n ):
2 Mtup = (" ", " Mon", " Tue", " Wed", " Thu", " Fri", " Sat", " Sun")
3 if n >7:
4 raise ValueError (" There are only 7 days !")
5 else :
6 return ( Mtup [ n ])
7
8 numToDay (8)
When raising an error try to pick an appropriate error type from those built-in and detailed at the link
above. In later weeks we will see how to define our own error types. In the meantime, you can always use
the most generic type, Exception
6
121COM: Introduction to Computing Worksheet 7: Exceptions
3 Exercises
Q1 Standard Streams: Experimenting to determine the following, and write short examples to demonstrate
your findings.
(a) What are the differences between the functions sys.stdout.write and print?
(b) What are the differences between the functions sys.stdin.read and input
Q2 Parameter Arguments: Experiment to determine the following, and write short examples to demonstrate
your findings.
(a) What is the value of argv[0] when accessed in interactive mode rather than within a script?
(b) What happens if we pass 100 and True as arguments to a script. Can we compute with them as an
integer and a boolean?
Q3 Handling Exceptions: Write a function called add which takes two inputs a and b, then outputs their
sum a+b. If the sum is not defined for the inputs then the function should catch the TypeError and
instead print a message to the user and return None.
Q4 Raising Exceptions: Copy out the code from Day.py above. Extend it so that it will raise a TypeError
if the input n is not of type int. Can you think of any other checks needed to ensure n is valid?
4 Common errors
❼ TypeError: must be str, not <DataType>
This could occur if you are trying to use sys.stdout.write with an argument that is not a string.
❼ TypeError: exceptions must derive from BaseException
This could occur if your are trying to raise an error, but the variable or value following the raise
keyword is not actually an exception.
7