
# Imports and Iteration

Work through before first lab in Teaching Week 3
Author: Dr Matthew England (Coventry University)
Contents
1 Using existing code 2
1.1 Function calls, input and output . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 2
1.2 The documentation . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 3
1.3 Module imports . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 3
2 Lists, strings and methods 5
2.1 Lists . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 5
2.2 Strings as sequences . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 6
2.3 Slice operator . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 6
2.4 The in operator . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 6
2.5 Methods . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 7
3 Iteration 7
3.1 While loops . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 7
3.2 For Loops . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 8
3.3 The range function and type . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 9
3.4 Nested loops . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 9
3.5 The break and continue keywords . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 9
4 Exercises 10
5 Common errors 10
1
121COM: Introduction to Computing Worksheet 3: Imports and iteration
1 Using existing code
In programming a Function is a segment of code which is encapsulated and given a name. This allows
programs to reuse the code in multiple places. A Module is a collection of functions, allowing the code to
be reused in other programs.
1.1 Function calls, input and output
To use a function write <functionName>(<arguments>) replacing <functionName> by the function’s name
and <arguments> by either the desired input value, or multiple values separated by commas. This is a
Function Call. Python evaluates the call to the function’s output, known as the return value. This can
then be printed or assigned to a variable for later use.
We have already met several functions in the previous two worksheets. For example:
❼ int, float, str, bool: these functions convert their input into output of datatype which shares
their name. The function type can be used to check what type something is.
>>> s = str(44.7)
>>> type(s)
<class ’str’>
❼ input: this functions takes a string as input; it displays this to the user and then waits for the user to
type; once they hit return the user’s response is stored as a string and outputted.
❼ print: this function converts the input to a string and then displays it to the screen.
Note that the string print produces is displayed to the screen even if we use ; to suppress the output.
>>> x = print("Hello");
"Hello"
This is because the purpose of print is communicating to the screen, not calculation. The "Hello" was
not returned as output but displayed to the screen while the function was running. However, in Python all
functions must output something: when there is no real output Python outputs a special None datatype
(referenced by the Python keyword None).
>>> type(x)
<class ’NoneType’>
All the functions above take one value as input. An example of a function which takes 2 inputs is round
which approximates the first input to the number of decimal places indicated by the second.
>>> round(100/3, 5)
33.33333
Other functions can take undetermined numbers of inputs. For example, max will identify the maximum
of its inputs (according to how values compare under the comparison operators).
>>> max(44, -700, 3.2)
44
>>> max(44, -700, 3.2, 44.0001)
44.0001
It is also possible to have functions with no input. For example, running locals() will output information
on the assigned variables that Python has access to.
2
121COM: Introduction to Computing Worksheet 3: Imports and iteration
The input to a function can in fact be anything that evaluates to a value, such as a variable or expression.
Python will always evaluate any expressions in the input before running the function.
>>> type(4/5)
<class ’float’>
>>> max(1000000/1000000, 2)
2
If the input itself includes function calls then these are also evaluated first, starting with the inner most.
>>> print("This building has seen " + str( round((2015-1233)/100,2) ) + " millennia")
This building has seen 7.82 millennia
1.2 The documentation
The functions built into Python all come with documentation. There are multiple ways to access it:
1. Online in a browser at https://docs.python.org/3.4/
2. Offline in (txt / pdf / html) if first downloaded from: https://docs.python.org/3.4/download.html
3. From the Python interpreter in conversation mode.
The latter is accessed via the function help. Running this with no input as help() opens up an interactive
help program while running it with a function name as input brings up the documentation for that function.
>>> help(round)
Help on built-in function round in module builtins:
round(...)
round(number[, ndigits]) -> number
Round a number to a given precision in decimal digits (default 0 digits).
This returns an int when called with one argument, otherwise the
same type as the number. ndigits may be negative.
The second line tells us what function calls are allowed. We knew already that this rounds the first input to
the number of digits in the second. We now also learn: that the second input is optional (indicated by the
square brackets) without which it to the nearest integer; and that the second input can be negative causing
rounding to nearest 10, 100, etc.
>>> round(10000/3,-2)
3300.0
This documentation for other functions can be lengthy. However, often the most useful information is at
the top in the list of permitted function calls. You can also get documentation for other things like operators
from help, but you should enclose the symbols in quotes first, for example help("or"). This is because
Python evaluates inputs before passing them to functions, and an or on its own would be a syntax error.
1.3 Module imports
All the functions met so far are built-in functions meaning they are encoded into the Python Interpreter
and so always available (unless you overwrite their name which is a bad idea).
There are a great many other functions already written in Python which you can use. These libraries
of code are arranged into modules or packages (we’ll explore the difference later) each of which defines
multiple functions. For example, the math module defines functions sqrt, log, sin and many more. For
efficiency we cannot have all functions ready to use at once. We instead choose which to use for each program.
3
121COM: Introduction to Computing Worksheet 3: Imports and iteration
There are various ways to access the functions in modules.
(1) from <module> import <functionName>
The function in questions is then available to use by its name. For example:
>>> from math import sqrt
>>> sqrt(4)
2.0
To import multiple functions we can list their names separated by commas.
>>> from math import sin, cos
>>> sin(cos(0))
0.8414709848078965
To import everything in a module we use an asterisk in place of <functionName>.
>>> from math import *
>>> log(100, 10)
2.0
Modules can contain values as well as functions. For example, math contains a float approximating π.
>>> pi
3.141592653589793
The following is an alternative approach to import everything from a module
(2) import <module>
When imported this way we can see everything contained in the module using the dir function on the
module name. The main difference compared to the first approach the function names have to be called in
the form <module>.<functionName> using the module name as well:
>>> import random
>>> random.randint(1,1000)
159
The function randint outputs a random integer between the two input integers, and so the output you
receive will probable be different to mine.
The second approach to importing means you have to type the module name every time you use a
function. The advantage is that it avoids name clashes. For example, if you already had a function called
randint which did something else then an import of the first type would overwrite it while an import of the
second type would not.
A third approach to this issue is to import functions and give them a new name.
(3) from <module> import <functionName> as <newFunctionName>
For example:
>>> from random import randint as randomIntegerGenerator
>>> randomIntegerGenerator(5,700)
542
The math and random modules are part of the Python Standard Library. This is an extensive collection
of code which is usually downloaded with the Python Interpreter and available for import automatically. The
standard library undergoes strict quality control and is fully documented both on-line and in the interpreter
help system. It is possible to use modules and packages from outside the Standard Library but these will
need to be first downloaded and installed.
4
121COM: Introduction to Computing Worksheet 3: Imports and iteration
2 Lists, strings and methods
2.1 Lists
A data structure is a tool to organise data on a computer. Each programming language will have several
different data structure types built-in. Picking the appropriate one for a task is a key skill for a programmer.
A sequence is the simplest theoretical data structure, being any ordered collection of values. The values
are called the elements of the sequence and the position of each value is called its index.
The list datatype in Python is an implementation of sequences. They are built using square brackets
around a comma separated sequence of values.
days = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"]
numbers = [4,8,99,-66,44,-2,0,9,4]
Note that lists can contain the same element multiple times (the int 4 is both the first and last element
in numbers. The data in lists will usually be related and it is traditional for it to all have the same type,
however Python does not enforce this.
random = ["Hello", 42, True, "why", False, 55.7]
We can refer to individual values in a list by using the list name followed by the index in square brackets.
The important thing to remember is that lists start counting from 0.
>>> days[0]
"Monday"
>>> numbers[1]
8
A common source of logic errors in Python is mistakenly counting from 1. We can also count backwards
from the end of the list by using negative numbers as the index.
>>> random[-1]
55.7
>>> days[-2]
"Thursday"
Note that the list index must always be an integer. A list with no elements is called the empty list and
can be created using square brackets with nothing inside.
emptyList = []
Note that trying to access an index of a list that does not exist (which is any index for the empty list) will
cause a runtime error. The built-in function len will return the number of elements in a list
>>> len(days)
5
Since the indices are counted from zero, a list L will always have elements indexed from 0 to len(L)-1.
We can change individual elements in a list separately via the index:
>>> random[3] = "because"
>>> random
[’Hello’, 42, True, ’because’, False, 55.7]
We can also use the + symbol to concatenate two lists into one
>>> random + numbers
[’Hello’, 42, True, ’because’, False, 55.7, 4, 8, 99, -66, 44, -2, 0, 9, 4]
5
121COM: Introduction to Computing Worksheet 3: Imports and iteration
2.2 Strings as sequences
We have already met the str datatype encoding strings. A string can be thought of as a special type of
sequence in which each element is a character (one letter string). Indeed, we can access individual characters
in a string using square brackets just like lists.
>>> word = "Good"
>>> word[1]
’o’
Just like lists, the characters are indexed from zero, and so the character with index 1 is the second letter
in the word. Also, like lists, we can use the len operator on strings.
>>> len(word)
4
Unlike lists, strings cannot have their individual elements changed. For example, word[0]="f" would
cause a runtime error. If you need to do this then use an actual list of strings.
2.3 Slice operator
We can use the square brackets to access more than one element at a time.
>>> sentence="This is a very boring sentence."
>>> sentence[10:14]
’very’
Using [m : n] returns the part of the string from the mth character to the nth character (counting from zero)
including the first but excluding the last. Note that spaces are counted as elements of the string
The output here is also a string (we may call it a substring). Using the square brackets this way is
sometimes called the slice operator. In fact, the slice operator works with all sequences - it can be used
on lists as well (returning sub-lists).
>>> days[3,5]
[’Thursday’, ’Friday’]
Although the list days has no element with index 5, this did not cause a runtime error because the slice
operator excludes the last element.
2.4 The in operator
The Python keyword in represents the in operator which is used to test membership of sequences (including
both lists and strings). It is a Boolean operator meaning it returns either True or False.
>>> "Monday" in days
True
>>> "Monday" in days[3:5]
False
>>> "Good" in "Good morning everyone"
True
>>> "Morning" in "Good morning everyone"
False
Note that when used on strings the search first string must be contained exactly (including case) and in
order to have True returned.
6
121COM: Introduction to Computing Worksheet 3: Imports and iteration
Since the in operator always returns a Boolean, it can be used as the test statement for conditionals.
InForIf.py
1 allowedAccess =[" Alice ", "Bob", "Eve"]
2 name = input (" What is your name ? ")
3 if name in allowedAccess :
4 print (" Welcome in!")
5 else :
6 print ("No access !")
2.5 Methods
Functions designed only to work with a specific type are sometimes called methods. Many of the Python
built-in types have associated built-in methods. The syntax for using methods is slightly different to normal
functions. We use the value in question (of the specified type) followed by a dot and then the normal function
call.
For example, the string method upper takes a str as input and outputs the the same string but with all
letters upper case
>>> word.upper()
’GOOD’
So instead of being inside the brackets the argument of the function (word) appeared before the call, joined
with a dot.
If a method takes more than one argument then the extra are included as normal. For example, the list
method append takes a list and a new value, returning the list enlarged by that value.
>>> days.append("Saturday")
>>> days.append("Sunday")
[’Monday’, ’Tuesday’, ’Wednesday’, ’Thursday’, ’Friday’, ’Saturday’, ’Sunday’]
Note that each new element becomes the last in the list.
3 Iteration
Iteration is the act of repeating a process. In programming iteration is used to repeat the same block of
code multiple times: after it executes the last statement in the block Python returns to the start of the
block, and so this is called looping. Python provides two constructs for controlling iteration.
3.1 While loops
A while loop will repeat a block of code so long as a given statement evaluates to True. We start a while
loop with the while keyword followed by the statement to check and then a colon. The code to be repeated
then follows, with indentation.
Countdown.py
1 n =3
2 while n > 0:
3 print ( n )
4 n = n - 1
5 print (" Blastoff !")
7
121COM: Introduction to Computing Worksheet 3: Imports and iteration
If you run Countdown.py you receive the output:
3
2
1
Blastoff!
When Python meets a while statement it first checks that the condition is satisfied: if so it executes the
indented code and then loops back to the condition check; if not if proceeds to the next statement after the
indented code. Hence if the condition was not satisfied to begin with the indented code would never get
executed (try changing the first line of Countdown.py to n=0 for example).
It is important that the indented code has the potential to change the outcome of the condition. If we
were to remove line 4 then n would never change and the code would be instructing Python to print 3 forever!
This is called an infinite loop. We usually try to avoid these (if you set one off press Ctrl+C to cancel).
3.2 For Loops
The for loop will repeat a block of code, letting a given variable be a different element of a sequence for
each loop. This variable is called the loop variable. We start a for loop with the for keyword, followed
by the name for the loop variable, the in keyword and the name of a sequence. The line is finished with a
colon and the code to be repeated follows, with indentation.
LoopThroughWeek.py
1 days = [" Monday ", " Tuesday ", " Wednesday ", " Thursday ", " Friday "]
2 for d in days :
3 print (" Today is " + d )
4 if d ==" Friday ":
5 print (" Woohoo !")
If you run LoopThroughWeek.py you receive the output:
Today is Monday
Today is Tuesday
Today is Wednesday
Today is Thursday
Today is Friday
Woohoo!
Python repeated the indented code 5 times (the length of the sequences days) each time setting the loop
variable d to be the next element in the list.
The for loop can also loop through sequences other than lists, such as strings.
Letters.py
1 word = input (" Please enter a word : ")
2 vowel = 0
3 for c in word :
4 if c in " aeiou ":
5 vowel = vowel + 1
6 print ( word + " has " + str( vowel ) + " vowels .")
Note that Letter.py has a logic error (it does not count vowels that are capital letters).
Python will let your repeated code edit the list it is iterating over, but this is bad practice and is not
recommended. If you need to edit a list while iterating it is better to use a while loop.
8
121COM: Introduction to Computing Worksheet 3: Imports and iteration
3.3 The range function and type
It is common to iterate over a sequence of successive integers. The built-in function range can build such
sequences: range(x) will go from 0 to x−1 while range(m,n) goes from m to n (including m, excluding n).
Range.py
1 # Script to observe the square function . Compare the two loops .
2 for x in range (10):
3 print ( x **2)
4 for x in range ( -10 ,11):
5 print ( x **2)
Note that range is not a list but a separate sequence datatype. We can convert them to lists easily though:
>>> list(range(10))
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
Given a list L the sequence formed by range(len(L)) can be used to iterate through all the indices of L.
3.4 Nested loops
We can place loops inside of other loops. We say that the second loop is inner and the first outer (in
comparison with their indentation). The inner loop will get executed for each run through of the outer loop.
PlayingCards.py
1 # Code to create a list of 52 strings , each representing one playing card
2 suits = [" Spades ", " Hearts ", " Clubs ", " Diamonds "]
3 ranks = [2 ,3 ,4 ,5 ,6 ,7 ,8 ,9 ,10 ," Jack "," Queen "," King ","Ace"]
4 deck =[]
5 for S in suits :
6 for R in ranks :
7 card = str( R ) + " of " + S
8 deck . append ( card )
In PlayingCards.py the outer loop was iterating over a list of length 4 and the inner loop over a list of
length 13. This produces the 4 ∗ 13 = 52 strings in the list deck.
3.5 The break and continue keywords
There are two further keywords for use in iteration.
If Python meets the continue keyword it will cease that run of the loop and return to the first line to
start again. This is useful when the code in the loop is not suitable for a particular element of the sequence.
ContinueExample.py
1 # Script to compare values of 1/i^3
2 for i in range ( -10 ,10):
3 if i ==0:
4 continue
5 print ( round (1/ i **3 , 5) )
If Python meets the break keyword in a loop it will exit and proceed to the next line of code. This can
be useful when it is not known how long a loop should last (for example, when it depends on the user).
BreakExample.py
1 while True :
2 userCommand = input ("Are you ready to continue ?")
3 if userCommand ==" yes":
4 break
9
121COM: Introduction to Computing Worksheet 3: Imports and iteration
4 Exercises
Q1 Using functions: Evaluate the following numbers as floats and round to 2 decimal places. You should
use functions and constants imported from the math module (either guess their name or look them up
in the documentation):
(a) log10(1234) (b) e
2
(c) π
2
(d) cos( π
2
) (e) sin( π
4
)
2
(f) arcsin(1)
Q2 Lists:
(a) Consider the following list of numbers: [1,2,3,3,3,4,4,5,6,7,8,9,10]. Calculate the mean,
median and mode averages as well as the standard deviation, using functions from the Standard
Library. Add the number 28 to the list and recalculate the statistics.
(b) Create a list with the months of the year as elements. Create a random birthday generator by using
the randint function twice: once to get a day of the month and again to select an index for the list.
Print out the date. Optionally, extend the code to ensure the date always exists.
Q3 While loops:
(a) A user has ↔100 to spend. Write a script where they can enter the amounts they spend until they
go over ↔100.
(b) You are served hot tea. Every time you blow on it the temperature reduces by 10%. Use a while
loop to calculate how many blows are needed to bring the tea down from 100◦C to 70◦C.
Q4 For loops:
(a) Ask the user for an integer between 0 and 12. Then use a for loop and the range function to print
the times table for that integer (the values of 3x for x between 0 and 12).
(b) Next use nested for loops to have Python print the complete 12 × 12 table. Remember that you can
use the escape sequences \t and \n in strings to create tabs and new lines respectively.
(c) Notice that the table produced above is symmetrical about the diagonal (numbers above are the
same as below). Edit the call to range so that only the bottom diagonal of the table is printed.
Q5 The break and continue keywords: Write a program to build a shopping list for a user. It should
repeatedly ask the user for items until they enter end when it should print the list. If the user has
already added an item it should be ignored the next time.
5 Common errors
❼ ImportError: No module named ’moduleName’
You tried to import a module that Python could not find. If this is your own module make sure it is
in the directory you are working. If this is third party make you sure have installed in properly.
❼ NameError: name ’functionName’ is not defined
This could occur if you tried to execute a function before you imported it.
❼ IndexError: list index out of range
You have tried to access a position in a list which does not exist. Make sure you are counting from 0.
❼ TypeError: ’str’ object does not support item assignment
You are trying to change individual characters in a string which is not permitted.
❼ Indentation errors and forgotten colons.
10