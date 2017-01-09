
# Defining Functions

Work through before first lab in Teaching Week 4
Author: Dr Matthew England (Coventry University)
Contents
1 Creating functions 2
1.1 Function definitions . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 2
1.2 Return values . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 2
1.3 Docstrings . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 4
1.4 Scope . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 4
2 Exercises 5
3 Common errors 5
1
121COM: Introduction to Computing Worksheet 4: Defining functions
1 Creating functions
1.1 Function definitions
As well as using other people’s function we will also need to create our own. To do this we use the def
keyword followed by the name of our new function and then names for the parameters (the input) in a
bracketed list. This line is called the function header finishes with a colon (indicating indented code is to
follow). The indented lines contain the function body: statements to be executed each time the function
is called. The following script gives a simple example.
Greeting1.py
1 def giveGreeting ( name , formal ):
2 """ This function will give a personalised greeting .
3 The first argument should be a string and the second a Boolean ."""
4 if formal :
5 print (" Good Morning " + name + ".")
6 else :
7 print ("Hi " + name + "!")
If you run the script there will be no output. That does not mean that nothing happened however. If ran
in IDLE it would mean that the function is now available to call in the conversation window. When Python
executes a function declaration it is defining that function for later use, not actually running it. The next
script both defines the function and also calls it.
Greeting2.py
1 def giveGreeting ( name , formal ):
2 """ This function will give a personalised greeting .
3 The first argument should be a string and the second a Boolean ."""
4 if formal :
5 print (" Good Morning " + name + ".")
6 else :
7 print ("Hi " + name + "!")
8 giveGreeting (" President Obama ", True )
9 giveGreeting (" Barack ", False )
When a function is defined in the same script it is used we must define it before we try to execute it.
Also, when defining a function Python will notice any syntax errors, but it will not pick up run-time
errors until the function is actually called. For example, if you ran the next script you should see the print
statement before the error message is triggered.
RunTimeError.py
1 def terribleFunction ( num ):
2 """ All this function does is trigger a runtime error !"""
3 x = num /0
4 print ("All fine so far")
5 terribleFunction (3)
The rules and recommendations for naming functions are the same as for variables (see Worksheet 1
Section 2.4). It is a good idea to give functions meaningful names, which describe what they do (rather than
how they do it).
1.2 Return values
The function giveGreeting took input and then printed a message. Most functions do not print anything,
instead, they produce output which the user can print, store or calculate with further as they prefer. When
writing a function we use the return key word to define output. If Python encounters this when running
the function then it ceases computation and returns the following value as output.
2
121COM: Introduction to Computing Worksheet 4: Defining functions
Area1.py
1 import math
2 def areaCircle ( radius ):
3 """ Function to calculate area of circle with given radius """
4 if radius >=0:
5 area = math . pi * radius **2
6 return ( area )
7 print (" Cannot have negative radius ")
8 areaCircle (3)
When the script Area1.py is run it first imports the math module, then defines a function to calculate
the area of a circle, before executing that function for the case with radius 3. In the function call the radius
is positive and so the return statement triggered. The print statement is only to be used when the radius
is negative. We do not need to test for this (or make the alternative conditional with else) since when not
negative the return statement is triggered and computation ceases before the final line.
The function calculates the area and outputs it, but since the script then does nothing with it there is
no visible outcome. Usually we would print or do some further computation as in Area2.py.
Area2.py
1 import math
2 def areaCircle ( radius ):
3 """ Function to calculate area of circle with given radius """
4 area = math . pi * radius **2
5 return ( area )
6 v = areaCircle (3)*10
7 print (" Volume of cylinder with radius 3 and height 10: " + str( v ) )
Functions can have more than one return statement, as in the next example.
absolute.py
1 def absolute_value ( x ):
2 """ Function to return absolute value of x"""
3 if x < 0:
4 return -x
5 if x > 0:
6 return x
7 print ( abs (5) , abs ( -4) , abs (0) )
The function absolute_value removes the negative sign from numbers. Note that when run with input 0
no return statement is triggered (as neither statement in the conditionals evaluates to True). When Python
reaches the end without meeting the return keyword it automatically outputs None (this happened also in
giveGreeting above). It would be more appropriate for absolute_value to consider the case x = 0.
Return values within a function can be of different types, but this is generally a bad idea. Functions
that go on to be used elsewhere have to be predictable - it would be difficult for another program to make
good use of a function that sometimes returns strings and sometimes integers. Many other programming
languages (like C++) would not allow this so try not to do it. An exception to this advice would be returning
None in circumstances where the normal output cannot be generated. The next function normally processes
scores out of 30 into percentages out of 100, but if a student forgot to submit it receives and returns None.
scoreToPercentage.py
1 def scoreToPercentage ( S ):
2 """ Convert score out of 30 to percentage """
3 if S == None :
4 return None
5 else :
6 return S /30*100
3
121COM: Introduction to Computing Worksheet 4: Defining functions
1.3 Docstrings
You may have noticed that all the functions in this Section have started with strings enclosed in triple
quotes. These strings have acted like comments telling us what the function does. Technically they are not
comments, but docstrings. It is good practice for all functions to start with a doc string describing at least
what they do and any assumptions made on the input.
1.4 Scope
We call the variables assigned within functions local. Variables local to a function are only available within
that function. The Python Interpreter removes them from memory when the function call finishes so if you
wanted them for later you should return them as output.
For example, running the next script will cause the string to be printed 5 times before an error message
triggered by line 7 trying to access a variable that no longer existed.
Scope1.py
1 def repeat (S , num ):
2 """ Function to print a string multiple times on different lines """
3 L = S +"\n"
4 L = L * num
5 print ( L )
6 repeat ("I will learn to love Python ", 5)
7 print ( L )
The scope of a variable (or a particular variable assignment) are the parts of the program where that
assignment is valid. The scope at a point in the program is the set of variable assignments currently
active. We could say line 7 is outside the scope of variable L; or that L is outside the scope at line 7.
The variable names given to the input arguments in the function header are also local. Hence the same
problem would occur in Scope1.py if we replaced line 7 with print(S) or print(num)
Although variables defined inside a function are local only to it, those defined outside of function declarations
(in what is called the main namespace) are still in scope. The next example demonstrates:
Scope2.py
1 def praise ():
2 L = "We love " + name + "!\n"
3 print ( L *5)
4 name =" Python "
5 praise ()
The function praise could access the variable name even though it was defined outside. Further, the
variable was defined after the function itself. There would only be a problem is the function was executed
before the variable defined. Functions also have access to anything imported into the main namespace.
Earlier, the function areaCircle used the constant math.pi imported outside the function definition.
Although functions can access variables in the main namespace, they will not overwrite them. If you run
the next script you will see the final print statement would still be C++.
Scope3.py
1 name = "C++"
2 def praisePython ():
3 name = " Python "
4 print ("We love " + name + "!")
5 praisePython ()
6 print ( name )
Variables assigned within functions are local to that function - even if they have the same name they are
in a different namespace and stored in different memory.
4
121COM: Introduction to Computing Worksheet 4: Defining functions
2 Exercises
Q1 Write a function that takes a number as an argument and prints positive if the number is greater than
zero; negative if less than zero and zero otherwise.
Q2 Write a function that takes a name in a string as input and then prints the Happy Birthday song
dedicated to that person.
Q3 Degrees in Centigrade can be converted to Fahrenheit using the formula
F = 1.8 × C + 32
Write two functions: one which inputs Centigrade and returns Fahrenheit; and another that inputs
Farenheit and returns Centigrade.
Q4 In the Imperial system weight is measured in stones and pounds (14 pounds in a stone). We can convert
to the metric system using the following formula which is correct to 2dp:
20 stone = 127 kg.
Write two functions: one which goes from imperial to metric and another from metric to imperial. The
first will have two inputs and one output; the second one input and two outputs.
Q5 In the UK return addresses are traditionally written right aligned at the top of a letter. Write a function
that takes a single string as input. The string should be an address with different lines separated by
commas. The function should print the address right aligned on separate lines 70 characters wide.
Q6 Functions can return other functions. Write a function that takes one argument x: if x = 0 return None;
otherwise return a function that will divide its input by x. Use your first function to create a halving
function and a quartering function. Try them out.
3 Common errors
❼ SyntaxError: expected an indented block
This could occur if you forgot to indent the function body in the function definition.
❼ NameError: name ’functionName’ is not defined
This could occur if you tried to execute a function before you defined it.
❼ NameError: name ’localVariableName’ is not defined
This could occur if you tried to use a previously defined variable outside of its scope. For example,
trying to use a local variable in the main script.
❼ Indentation errors and forgotten colons.
5