
# Taking Control

Work through before first lab in Teaching Week 2

Author: Dr Matthew England (Coventry University)

## 1 Booleans in Python

### 1.1 The bool Datatype

We introduce another of JavaScript's core datatypes:

bool This type encodes the Boolean values True and False.

Recall that True and False were in the list of Python keywords, and so they cannot be used as variable names for example. Unlike the other datatypes we have met there are only the two Boolean values. However, there are infinitely many Boolean expressions: any expression that evaluates to either True or False. The following operators can be used to decide whether things are True or False; such decisions are the main tool for controlling the flow of program.

Some programming languages will associate False with the number 0 and True with the number 1.

While Python has the separate type for Booleans, it will convert between formats when appropriate. For
example:
```
> 1+True
2
> 4*False
0
```

Actually, when trying to generate a bool JavaScript will interpret any non-zero number of non-empty string as True.
```
> bool(452.7)
True
> bool(0)
False
> bool("Hello")
True
> bool("")
False
```

### 1.2 Comparison operators

We now introduce some new binary operators and their programming symbols in Python which all evaluate to Boolean values.

`==` equal to: returns True when the two operands are equal.

`!=` not equal: returns True when the two operands are different.

`<` (strictly) less than: returns True when the first operand is less than the second.

`<=` less than or equal to: returns True when the first operand is smaller than or the same as the second.

`>` (strictly) greater than: returns True when the first operand is bigger than the second.

`>=` greater than or equal to: returns True when the first operand is bigger than or equal to the second.

These are used in Python in the same way as the other binary operators we have met:

`<first operand> <operator symbol> <second operand>`

```
> 5 == 5
True
> 9.0000001 <= 3**2
False
> 4 > 2*2
False
```

Note that the final example is False. The symbols `>` and `<` are strict which means they exclude equality.

It is important to remember the difference between = and ==. The first is the assignment operator which assigns a variable to a value. The second is the operator for testing equality of values (or variables already assigned to values). They look similar but have very different meanings.

Python only evaluates comparison operators after it has evaluated the numerical operators we met earlier (unless parentheses instructs it otherwise)
```
> 4+5 < 6+1
False
> 4 + (5<6) + 1
6
```

The second example is because 5<6 evaluates to True which Python then converts to 1 for the numerical
addition.

These comparison operators can be used with some non-numerical data types also, such as strings.
```
> "Hello World!" == "Hello World!"
True
> "Hello world!" == "Hello World!"
False
```

The equality operator will check whether two strings are exactly the same (including the case of letters).

When comparing single characters the > and < operators refer to the ASCII ordering of symbols. See the following link for the full list: http://www.nationalfinder.com/html/char-asc.htm In particular, numbers come before letters and all capital letters come before all lower case letters.
```
> "1" < "h"
True
> "F" > "B"
True
> "F" > "b"
False
```

For longer strings the operators do a lexicographical ordering: the first two items are compared; if they differ this determines the outcome; otherwise the next two items are compared; and so on.

### 1.3 Logical Operators

We now introduce the three logical operators. These only operate on Booleans (or expressions which evaluate to them) and evaluate to a Boolean.

`not` This unary operator returns True if the sole operand evaluates to False.

`and` This binary operator returns True if both of the operands evaluate to True.

`or` This binary operator returns True if either of the two operands evaluates to True.

If the conditions to evaluate to True are not met the operators evaluate to False.
```
> not False
True
> not True
False
> True and True
True
> True and False
False
> False and False
False
> True or True
True
> True or False
True
> False or False
False
```

The operands can be any expression which evaluates to a Boolean (such as the results of comparison operators).

Comparison operators are always evaluated before logic operators, so in `CheckUser.py` there is no need for parentheses in line 4.
```
# CheckUser.py
# We see if the user can follow instructions
A_str = input (" Please enter a positive number less than 100: ")
A_float = float ( A_str )
answer = A_float > 0 and A_float < 100
print (" Followed the instructions : " + str( answer ))
```

Note that we can join logical operators together just like numerical operators as in the next example.
```
# PrimeTest.py
# A number is prime if it is not divisible by any smaller primes .
# So this script tests if 13 is prime
n = 13
divisible = ( n %2==0) or ( n %3==0) or ( n %5==0) or ( n %7==0) or ( n %11==0)
answer = not divisible
print ("Is 13 prime : " + str( answer ))
```

## 2 Conditionals
The tools in Section 1 are most useful for building code that only executes under certain conditions. This allows us to control our code based on the results of earlier calculations, or unpredictable new information like human input.

### 2.1 Conditional Execution

The simplest conditional programming tool in Python is the if statement. To use this we first type the if keyword followed by a space; a statement that evaluates to a Boolean; and then a colon. On the following lines we type code that is only to be executed when the statement is True. This code should be indented: each line starts with some white space.
```
# AgeTest1.py
userNumber_str = input (" Please enter your age: ")
userNumber = int( userNumber_str )
if userNumber <=0:
print (" That ✬s not possible !")
print (" Please try again .")
print (" Thank You")
```

Observe that when running `NumberTest1.py` if the user enters 0 or a negative number the first two print statements are executed, while the second print statement is executed whatever number they enter.

The indentation is very important: it telling Python which code is conditional and which is not. It does not matter how much indentation you use (the most common choice is 4 spaces or 1 tab). However, it is important you use the same indentation throughout, otherwise you will generate a syntax error. The colon is used to tell Python that an indented block is about to follow.

### 2.2 Alternative Execution

The if statement can be extended to execute alternative code when the control statement is False. To do this we follow the first block of conditional code with the keyword else followed by a colon and then the alternative block of code (also indented).
```
# AgeTest2.py
userNumber_str = input (" Please enter your age: ")
userNumber = int( userNumber_str )
if userNumber <=0:
  print (" That ✬s not possible !")
else :
  print (" That number makes sense . Thank You")
```

Remember, if the condition evaluates to True the first block of code is executed and if False then the second. It is never possible for both blocks to run. These alternatives are called branches in the program.

### 2.3 Chained conditionals

In some situation there may be more than two possibilities. In this case we can extend the if statement further to check a second condition if the first is not satisfied. We follow the original conditional code for when the first statement is True with the keyword elif and then the second statement to check.
```
# AgeTest3.py
userNumber_str = input (" Please enter your age: ")
userNumber = int( userNumber_str )
if userNumber <0:
  print (" That is not possible !")
elif userNumber >115:
  print (" That is very unlikely !")
else :
  print (" That number makes sense . Thank You")
```

Chained conditionals are evaluated by Python as follows: the first statement is checked; if True the conditional block is executed and Python proceeds to the code after the conditionals; if False python checks the second statement; and so on. The keyword elif is an abbreviation of else if meaning the next block is only done if all preceding statements were False (else) and the next statement is True (if).

You can check unlimited options by using multiple elif’s but no matter how many, only one branch will ever be executed (the first which evaluates to True). So the order you test that statements can be important.
```
# AgeTest4.py
# This is flawed code - the second branch can never be accessed .
userNumber_str = input (" Please enter your age: ")
userNumber = int( userNumber_str )
if userNumber <65:
  print ("You ✬re not entitled to a discount .")
elif userNumber ==21:
  print (" That ✬s the same age as me")
```

### 2.4 Nested Conditionals

One conditional can be nested within another as in the next example. Note here that the second statement test is initiated with if rather than elif. This is because it is not part of the same control structure as the first one, rather it is just part of the code in the conditional block, like the final lies where the price is calculated.
```
# AgeTest5.py
userNumber_str = input (" Please enter your age: ")
userNumber = int( userNumber_str )
if userNumber <12:
  print ("You ✬re too young to watch this movie .")
else :
  price =15
  if userNumber >65:
    discount =10
  elif userNumber <18:
    discount =20
  else :
    discount =0
  price = 15/100*(100 - discount )
   print (" Please pay " + str( price ))
```

Unlike chained conditionals, nested conditionals allow for more than one conditional block of code to be executed. In the above example the second branch was split further into two. Note that the inner conditional code must be indented further still. The additional indentation can be any positive number of spaces (so long as it is consistent), but the traditional approach would have it twice as much as before.

It is possible to nest multiple conditions (equivalent to splitting branches further) by using more if statements and further indentation. However, nested conditionals become difficult to read very quickly and it probably better to avoid nesting too many.

Logical operators can often provide a way to simplify nested conditional statements. For example, `SingleDigitCheck1.py` and `SingleDigitCheck2.py` do the same thing.
```
# SingleDigitCheck1.py
x_str = input (" Please enter a digit : ")
x = int( x_str )
if x >0:
  if x <10:
    print (" Thank you")
  else :
    print ("Not a digit !")
else :
  print ("Not a digit !")
```

```
# SingleDigitCheck2.py
x_str = input (" Please enter a digit : ")
x = int( x_str )
if x >0 and x <10:
  print (" Thank you")
else :
  print ("Not a digit !")
```

We cannot omit a conditional block when using if statements. If you want a branch to do nothing then use the pass keyword. This forces Python to just continue with the program.
```
# UsingPass.py
bill = 95
n = int( input ("How many are we splitting the bill between ? "))
if n ==0:
  pass
else :
  print (" " + str( round ( bill /n , 2)) + " each .")
```

The if statement avoids the possibility of a divide by zero error. If the user does enter zero the program will simply end without error.

## 3 Exercises

Q1 Booleans: All the following expressions evaluate to a Boolean (True or False). First write down which you think, and then check your answer in Python.

1. not 1==1
2. not( True and False )
3. 4>4 or 3<3
4. "a"=="b" or 1!=222
5. 1<=10 and 10>=-1
6. "Test"=="test" and "test"=="test"
7. not( 100!=100.000001 and "Python"=="Fun" )
8. not( not("Python"=="Fun") or 150/5 < 60/2 )

Q2 Conditionals: Write scripts to do the following tasks using if-statements and their variants.

1. Have Python ask the user for a password. If the user answers correctly Python should print a secret message, and otherwise ask them to leave.
2. A quadratic polynomial ax2 + bx + c will have a certain number of real roots (values of x for which it vanishes) depending on the discriminant d = b2 −4ac. When d < 0 there are no roots; when d = 0 there is one root; and when d > 0 there are two. Have Python ask the user for values of a, b and c and then calculate the number of roots.
3. When using your car for work your employer gives you expenses of 50p per mile for the first 10 miles and 37 p per mile thereafter with a maximum claim of 100 miles per job. Have Python ask you for how many miles you drove and then calculate your expense claim.
4. A leap year has one extra day in February. A year can only be leap if it is divisible by 4. However, if it is also divisible by 100 then it is leap only when divisible by 400 as well. Have Python ask a user for a year and tell the user if it is leap.

## 4 Common errors

SyntaxError: can’t assign to literal

This error message could occur if you used assignment when you meant equality test.

NameError: name ’myVariable’ is not defined

This error message could occur if you meant to assign a value for the first time to myVariable but instead used the equality test

SyntaxError: unexpected indent

This occurs when Python cannot relate indented code to a control command. Check that:

– you remembered to indent the code for conditional execution;
– each line in a block of indented code has the same indent;
– there is no code indented when it shouldn’t be.

SyntaxError: invalid syntax

This can be caused by many things. Two possibilities relevant to this worksheet are:

– forgetting the colon that follows the if statement / elif statement / else statement;
– using an else or an elif keyword before the corresponding if keyword.
