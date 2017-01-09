
# Classes and Objects

Work through before first lab in Teaching Week 8
Author: Dr Matthew England (Coventry University)
Contents
1 Classes and Objects 2
1.1 Attributes . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 2
1.2 Methods . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 3
1.3 Good practice . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 4
2 More Advanced Classes 5
2.1 Private attributes . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 5
2.2 Automatic conversions . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 6
2.3 Arithmetic operations . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 7
3 Exercise 9
4 Common errors 9
1
121COM: Introduction to Computing Worksheet 8: Classes and Objects
1 Classes and Objects
Defining classes and objects allows us to create our own data types; encapsulate data with relevant methods;
maximise code reuse; and, write software that more closely resembles the real world.
Note that the Robot example in Subsection 1.1 is designed to help you understand how classes and
objects store data in Python. However, the code there does not represent good practice − a better way to
implement the Robot example is given in Subsection 1.2.
1.1 Attributes
A class defines a type, which can include: data; rules for that data; and functions to access / manipulate
it. An object is a particular instance of a class; an example where the data has particular values.
We have already met many classes. For example, the data structure list is a class and any sequence
enclosed in square brackets is an object defined as an instance of the list class.
>>> L = [1,2,3]
>>> type(L)
<class ’list’>
Similarly, int, str, dict and all the built-in data types and structures are classes and when we define data
of these types we are defining instance objects of those classes.
We can also define classes of our own. We use the class keyword; followed by the name of our class;
and then a colon. This is the header of the definition, and as usual, the body follows as an indented block
of code. Our first class below will be for robots. Currently there is no code in the body (the pass keyword
is there because we cannot have an empty code block).
Robot1.py
1 class Robot :
2 # This class will be used for robots
3 pass
Many of the built in classes had special syntax to define their instance objects (square brackets for list,
quotes for str, curly brackets for dict etc.) but in general we define objects with a function-like call to the
class name. The following assigns two objects of type Robot to the variables robot1 and robot2.
>>> robot1 = Robot()
>>> robot2 = Robot()
An object can store data, which we call attributes of the object. We use <objectName>.<attributeName>
where the dot is indicating that the attribute belongs to the object.
>>> robot1.name = "Marvin"
>>> robot1.buildYear = 1978
>>> robot2.name = "WALL-E"
>>> robot2.buildYear = 2008
Once defined, attributes can be accessed in the same way, as this next function does when printing a sentence
formed from a robot/s attributes.
>>> def printRobotAttributes(R):
print(R.name + " first appeared in " + str(R.buildYear) )
>>> printRobotAttributes(robot1)
Marvin first appeared in 1978
2
121COM: Introduction to Computing Worksheet 8: Classes and Objects
If you try to access an undefined attribute you will raise an AttributeError. Objects store their
attributes in a dictionary. We can see the dictionary of attributes using <objectName>.__dict__:
>>> robot2.__dict__
{’name’: ’WALL-E’, ’buildYear’: 2008}
Note that the classes themselves can also have attributes.
>>> Robot.number = 2
Here number is an int counting how many objects of the class there are. This attribute is shared with all
objects of the class.
>>> robot1.number
2
Suppose we want to define a third robot
>>> robot3 = Robot()
>>> robot3.name = "Johnny5"
>>> robot3.buildYear = 1986
>>> robot3.number=3
In the final line we increase number to 3. However, we find that this data is not shared with other objects
>>> robot1.number
2
This is a logic error, caused because the new number was stored in the local namespace of the object robot3,
not the namespace of the class Robot. The final line should have been Robot.number=3.
1.2 Methods
The code for the robot example could be improved in many ways:
❼ Each instance of Robot should have a name and buildYear, but there is nothing ensuring this.
❼ Each time a new Robot object is created we should increase the class attribute Number, but again,
nothing forces the user to this and we could easily make a mistake if assigning to the object attribute.
❼ The function printRobotAttributes is written specifically for input of type Robot but could be called
on anything.
We can fix these issues by improving the class definition. The key is defining methods (functions within
class definitions for use only with objects of this class).
We can take the function printRobotAttributes and move it into the class definition (taking care to
ensure proper indentation). It is now a method of the class and so is called with the dot notation following
the name of an object from that class. We do not need to include input within the brackets any-more: when
calling a method from an object using the dot syntax the object itself is passed as the first parameter.
The other problems are solved by defining a special instantiation method called __init__. This is
a method which is called automatically on an object after it is created. Other than the object itself, the
arguments of __init__ are those provided by the user on creation. The default value of any class attributes
should be given separately in the class definition
3
121COM: Introduction to Computing Worksheet 8: Classes and Objects
Robot2.py
1 class Robot :
2 """ A class to store famous robots .
3
4 Each object has attributes name and buildYear .
5 The class attribute number records how many objects have been created .
6 The only method is printRobotAttributes .
7 """
8
9 number = 0 # class attribute
10
11 def __init__ (self , N , Y ): # instantiator
12 self . name = N
13 self . buildYear = Y
14 Robot . number = Robot . number + 1
15
16 def printRobotAttributes ( R ):
17 print ( R . name + " first appeared in " + str( R . buildYear ) )
18
19 robot1 = Robot (" Marvin ", 1978)
20 robot2 = Robot ("WALL -E", 2008)
Running the above script first defines the class itself, and then two instances of it.
>>> robot1.printRobotAttributes()
Marvin first appeared in 1978
>>> robot2.printRobotAttributes()
WALL-E first appeared in 2008
Note that each time we created an object the instantiation method was called and thus the class attribute
increases.
>>> Robot.number
2
>>> robot3 = Robot("Johnny5", 1986)
>>> Robot.number
3
1.3 Good practice
The following is good practice for working with classes and functions.
❼ Start class names with a capital letter and object names with a lower case letter. Python does not
enforce this but other languages do. It differentiates between function calls and object instantiation.
❼ Start class bodies with a docstring: Good practice would be a one sentence introduction, followed by
a description of what attributes are required and methods available.
❼ Then give any class attributes set to their default values.
❼ Next give the __init__ method. This should ensure any object has the attributes essential for the
core functionality. It could also include error checking (e.g. ensuring buildYear was an int).
❼ When writing methods in a class definition use self for the first parameter name (which will be
assigned to the object which calls it). This is not enforced (indeed, in Robot2.py we left the parameter
for printRobotAttributes as R) but it adds clarity.
Some languages will require you to write each class in a separate file whose name is the same as the class.
Python does not enforce this, but it is a good technique especially when dealing with large classes.
4
121COM: Introduction to Computing Worksheet 8: Classes and Objects
2 More Advanced Classes
2.1 Private attributes
Consider Robot2.py above. The class attribute number is for keeping track of how many robots we have.
However, these is nothing to stop a user simply overwriting this data, causing the class to lose count. We
really want number to only be edited by the __init__ function in the Robot class.
A variable only accessible by functions from its class is called private. In Python we declare something
private by starting its name with two underscores. Edit Robot2.py so that all occurrences of number are
replaced with __number: then trying to access number from outside the class will give an AttributeError.
>>> Robot.number
AttributeError: type object ’Robot’ has no attribute ’number’
Methods can also be made private by adding double underscores to the start of their name. You may
have noticed that the __init__ method is not private: this is due to the extra underscores at the end which
indicates it has special properties (such as being called every time we create an instance of the class).
Now that number is private it should not get reset by a user. However, the user may wish to view it
and now has no access. The solution is to provide a method available for the user. Such methods are called
assessors or getters (and traditionally have names beginning with get).
Robot3.py
1 class Robot :
2 """ A class to store famous robots .
3
4 Each object has attributes name and buildYear .
5 The private class attribute __number records how many objects are created .
6 The only method is printRobotAttributes .
7 """
8
9 __number = 0 # private class attribute
10
11 def __init__ (self , N , Y ): # instantiator
12 self . name = N
13 self . buildYear = Y
14 Robot . __number = Robot . __number + 1
15
16 def printRobotAttributes ( self ): # object method
17 print ( self . name + " first appeared in " + str( self . buildYear ) )
18
19 def getNumber (): # class method
20 return ( Robot . __number )
Note that the new accessor getNumber is a class method (rather than an object method) as indicated by
the first parameter name not being self. Hence we access it from the class and not a particular object.
Under some circumstances we may want to allow users to edit private variables. For example, in Robot
we may be happy to allow a user to change the buildYear of a robot but want to ensure it always remains
an integer. We can put such a check in the instantiation method; but we can only maintain the guarantee if
we make the attribute private and only allow changes via a method which performs the check. Such methods
are called mutators or setters (and traditionally have names beginning with set).
Note that the new mutator setBuildYear in Robot4.py is an object method as indicated by the first
parameter being self. Hence we access it from a particular instance of the class.
5
121COM: Introduction to Computing Worksheet 8: Classes and Objects
Robot4.py
1 class Robot :
2 """ A class to store famous robots . """
3
4 __number = 0 # private class attribute
5
6 def __init__ (self , N , Y ): # instantiator
7 self . name = N
8 if type ( Y )== int:
9 self . __buildYear = Y
10 else :
11 raise TypeError ("The build year must be an int")
12 Robot . __number = Robot . __number + 1
13
14 def printRobotAttributes ( self ): # object method
15 print ( self . name + " first appeared in " + str( self . __buildYear ) )
16
17 def getNumber (): # class method
18 return ( Robot . __number )
19
20 def setBuildYear (self , Y ): # object method
21 if type ( Y )== int:
22 self . __buildYear = Y
23 else :
24 raise TypeError ("The build year must be an int")
Private attributes and Python
Private attributes are a common feature in object oriented programming. However, they are not so common
in Python programs and Python’s support for them is very limited. The use of double underscores does not
really protect the attribute: it merely relabels it so it is slightly more cumbersome to access: a process called
name mangling.
Double underscores should not be considered as providing security. Instead they can be thought of as
a shorthand comment to other developers that this variable is only for internal use and your code will not
support use-cases which edit it.
2.2 Automatic conversions
Recall that the built-in print function takes its input, tries to convert to a string, then writes to stdout.
The middle step, converting to a string, requires a tool from the data type of the input saying how it should
be displayed as a string. This takes the form of another special method __str__ which should always return
a string object. Our existing method printRobotAttributes is edited to provide this below.
Robot5.py
1 class Robot :
2 """ A class to store famous robots . """
3 __number = 0 # private class attribute
4 def __init__ (self , N , Y ): # instantiator
5 self . name = N
6 if type ( Y )== int:
7 self . __buildYear = Y
8 else :
9 raise TypeError ("The build year must be an int")
10 Robot . __number = Robot . __number + 1
11 def __str__ ( self ): # how to convert to string
12 return (" Robot " + self . name + " from " + str( self . __buildYear ) )
6
121COM: Introduction to Computing Worksheet 8: Classes and Objects
>>> robot1 = Robot("Marvin", 1978)
>>> print(robot1)
Robot Marvin from 1978
The difference between str and repr
This is another special method __repr__ which is similar to __str__ in that it converts an object to a string
representation. The two methods have different aims:
str aims to give a user-friendly string representation suitable for human reading;
repr aims to give an unambiguous string representation of an object, from which the object could be
recreated. It is mainly designed for use by other code. The main use of __repr__ is for debugging.
The built-in functions str and repr call the respective object methods for their input. Consider how
they deal with the boolean True and string "True" below:
>>> str(True)
’True’
>>> str("True")
’True’
>>> repr(True)
’True’
>>> repr("True")
"’True’"
The function str converts both the boolean and the string to the string ’True’; while repr adds the extra
quotes for the string input that Python would need to recreate it.
The function print will use the str method it is exists, and repr otherwise. In interactive mode, the
interpretor calls repr to display output from a statement.
Other conversions
There are similar special methods for converting to some of the other main data types (e.g. __int__ for
int, __float__ for float etc). These should only be used if there is an appropriate representation for your
class. For our robot example, it would not make sense to convert them to integers or floats so we do not
implement these.
2.3 Arithmetic operations
Recall that the arithmetic symbols behave differently depending on the data type:
>>> 2+2
4
>>> "2"+"2"
’22’
The binary arithmetic operators work by calling special methods of the objects forming operands. These
can be defined with more special methods in the class definition. For example, consider the class below to
represent days of the week. We define a Day by giving an integer between 1 and 7 (the internal number is
between 0 and 6 due to indicies counting from zero).
7
121COM: Introduction to Computing Worksheet 8: Classes and Objects
Day.py
1 class Day :
2 """ Class to represent days of the week """
3
4 dayTuple = ("Mon", "Tue", "Wed", " Thur ", "Fri", "Sat", "Sun")
5
6 def __init__ (self , N ):
7 if N >=0 and N <7 and type ( N )== int:
8 self . dayCode = N
9 else :
10 raise TypeError ("the dayCode should be integer between 0 and 6")
11
12 def __str__ ( self ):
13 return (" This day is a " + Day . dayTuple [ self . dayCode ])
14
15 def __add__ (self , num ):
16 if type ( num )!= int:
17 raise TypeError ("we can only add integers to a Day")
18 newDayCode = self . dayCode + num
19 newDayCode = newDayCode %7
20 return ( Day ( newDayCode ) )
The special method __add__ defines how adding an integer to a Day returns the appropriate Day object
for that many days later.
>>> d = Day(5)
>>> print(d)
This day is a Friday
>>> print(d+4)
This day is a Tuesday
The code currently has limited functionality. For example, we get an error if we try to subtract an integer.
We need to implement a separate __sub__ method for subtraction. We would also get an error if we tried
to execute 4+d. When Python encounters the + symbol acting as a binary operator it searches in the left
operand for an add method suitable for acting on the operands. If one does not exist (as in the case 4+d)
it will look for an radd method in the right operand. Adding the code in AdditionsToDay.py to the class
definition in Day.py will solve these problems.
AdditionsToDay.py
1 def __radd__ (self , num ):
2 return ( self + num )
3
4 def __sub__ (self , num ):
5 return ( self +( - num ) )
Note that in both cases we use the fact that addition of a Day object to an integer is already defined.
There are similar special methods that can be defined for all the arithmetic operators we met in Python.
See the documentation at the link below for details.
https://docs.python.org/3.4/reference/datamodel.html#emulating-numeric-types
8
121COM: Introduction to Computing Worksheet 8: Classes and Objects
3 Exercise
In a script define a Python class called BankAccount.
❼ Each instance of the class should have the attributes name, address and balance.
❼ The instantiation method should have input determining the customer name and address. It should
also set the balance to zero.
❼ Each instance should have access to methods withdraw and deposit to change the balance.
Test the class by creating two bank accounts and making some deposits and withdrawals. Once you are
satisfied, implement the following extensions in turn, testing each one.
- Make the balance a private attribute so that a user can only change it by going through the methods. Add
an accessor method getBalance which a user can use to check their balance.
- Ensure that the withdraw method does not allow a user to take out more money than their balance.
- Add an attribute bankName. This should be the same for all instances of the class.
- Add an attribute number which keeps count of how many accounts have been created.
- Write a special method so that applying print to a BankAccount object displays the name of the account
holder and their balance.
- Write a method transfer which sends money from one bank account to another.
Make sure your class includes a meaningful docstring.
4 Common errors
❼ AttributeError: <objectName> object has no attribute <attributeName>
This error message occurs if you try to access an attribute which is not defined for an object. Ensure
you got the name right, including any underscores, and that you are not trying to access a private
variable from outside the class.
❼ TypeError: <methodName>() takes 0 positional arguments but 1 was given
This error could occur if you are trying to call a class method from an object. If the method should
be for calling with an object make sure the first parameter is self. If it is meant to be a class method
call it using <ClassName>.<methodName>().
9