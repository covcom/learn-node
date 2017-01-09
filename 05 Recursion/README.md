

# Recursion and Turtles

Work through before first lab in Teaching Week 5
Author: Dr Matthew England (Coventry University)
Contents
1 Recursive Functions 2
1.1 Definition . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 2
1.2 Base cases . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 3
2 Drawing with turtle 3
3 Exercises 4
4 Common errors 4
1
121COM: Introduction to Computing Worksheet 5: Recursion and Turtles
1 Recursive Functions
1.1 Definition
Recall that functions can call other functions. A recursive function is a function which calls itself.
Countdown.py
1 # Example from Think Python by Allen Downey .
2 def countdown ( n ):
3 if n <= 0:
4 print (" Blastoff !")
5 else :
6 print ( n )
7 countdown (n -1)
Once the function in Countdown.py is defined we can execute it, as in the following example.
>>> countdown(3)
3
2
1
Blastoff!
The output is simple but the work of the Python interpretor is actually quite complex:
The first countdown call has n = 3. Since n > 0 it prints 3 and calls itself...
The second countdown call has n = 2. Since n > 0 it prints 2 and calls itself...
The third countdown call has n = 1. Since n > 0 it prints 1 and calls itself...
The fourth (& final) countdown call has n = 0. Since n ≤ 0 it prints Blastoff! and returns None.
The third call (where n = 1) then returns None.
The second call (where n = 2) then returns None.
The first call (where n = 3) then returns None.
Hence, after the fourth call is made, there are 4 different values of n stored in memory. Python keeps
track of these, using the appropriate one each time, since they exist in different namespaces.
The function countdown would probably be easier to write with a for loop. However, for other problems
recursion is the natural way to program. Consider the factorial function which occurs throughout
mathematics. The factorial of a positive integer n is denoted usually n! and defined as
n! = (
1 if n = 0,
(n − 1)! × n if n ≥ 0.
The following function is the natural way to compute it
Factorial.py
1 def factorial ( n ):
2 # Recursive function to compute factorials .
3 if n == 0:
4 return (1)
5 else :
6 ans = n * factorial (n -1)
7 return ( ans )
>>> factorial(4), factorial(5), factorial(6)
(24, 120, 720)
2
121COM: Introduction to Computing Worksheet 5: Recursion and Turtles
1.2 Base cases
Technically all a function needs to be recursive is to call itself. However, for a function to be useful it should
also contain some way to break out of the recursion. Consider the following function.
InfiniteRecursion.py
1 def infiniteRecursion ( n ):
2 print ( n )
3 infiniteRecursion ( n +1)
If we called infiniteRecursion(1) then the function would print 1; call itself with n = 2; print 2; call itself
with n = 3; . . . The function should never stop; instead making recursive calls to itself forever. In actuality,
the Python interpreter will not let you do this. There is a limit to the number of recursive calls allowed and
when reached Python will return (a lot of) error messages. Try running the function and read these.
To avoid infinite recursion (or very long error messages) all recursive function should include a base case:
a piece of code before the recursive call that gives the option to exit. In Countdown.py and Factorial.py
there were base cases on lines 3 − 4.
2 Drawing with turtle
The power of recursion is best appreciated with graphics. We will explore this in the Lab Sheet, but first
we introduce some basic tools for drawing in Python. The Python Standard Library includes a module for
Turtle Graphics: so called because we use a turtle moving in the plane to create shapes.
Turtle1.py
1 import turtle # Allows us to use turtles
2
3 turtle . forward (50) # Tell turtle to move forward 50 units
4 # ( automatically creating turtle and screen )
5 turtle . left (90) # Tell turtle to turn left 90 degrees
6 turtle . forward (30) # Tell turtle to move forward another 30 untis .
The above code shows us the basics:
❼ The code is all contained in the turtle module so we start by importing that;
❼ The function forward moves the turtle forward, and left turns it left. There are similar commands
for moving backwards and turning right (test them).
Note that the first time we use a turtle command the module automatically creates a new window with
a screen for the turtle to draw on. If you ran the code in IDLE the window will stay open but if running
from the command line it will close once the end of the script is reached (closing the Python interpreter).
To avoid this, we can explicitly create the screen as part of the program and then have the program wait
until the user is finished before closing using the two extra lines (line 2 and line 6) in Turtle2.py
Turtle2.py
1 import turtle # Allows us to use turtles
2 myScreen = turtle . Screen () # Creates screen and assigns
3 turtle . forward (50) # Tell turtle to move forward 50 units
4 turtle . left (90) # Tell turtle to turn left 90 degrees
5 turtle . forward (30) # Tell turtle to move forward another 30 untis
6 myScreen . mainloop () # Waits until user closes screen
The turtle is always at a specified co-ordinate when the screen is considered as the (x, y)-plane. The function
position checks the turtle’s position. The following code drwas a triangle; the first print gives (0.00,0.00)
and the second (50.00,30.00).
3
121COM: Introduction to Computing Worksheet 5: Recursion and Turtles
Turtle3.py
1 import turtle # Allows us to use turtles
2 print ( turtle . position ()) # Tells us the current position
3 turtle . forward (50) # Tell turtle to move forward by 50 units
4 turtle . left (90) # Tell turtle to turn by 90 degrees
5 turtle . forward (30) # Complete the second side
6 print ( turtle . position ()) # Tells us the current position
7 turtle . goto (0 ,0) # Returns to start point forming triangle
We can colour in the shapes we draw by encasing them with the begin_fill and end_fill commands.
The following script will fill in the star drawn.
Turtle4.py
1 import turtle
2 turtle . begin_fill () # Start of shape to be filled
3 for side in range (5): # Use loop to repeat sides
4 turtle . forward (100)
5 turtle . right (120)
6 turtle . forward (100)
7 turtle . left (48)
8 turtle . end_fill () # End of shape to be filled
Other commands in the turtle library allow you to: change the colour of the lines drawn; change the
colour of filled in shapes; change the background colour of the screen; move the turtle without drawing a
line; clear the screen; and change the speed of the turtle. As with all modules in the Standard Library there
is lots of documentation available, for example at the following link.
https://docs.python.org/3.4/library/turtle.html
3 Exercises
Q1 Recursive Functions: The Fibonacci numbers Fi are defined by F1 = 1, F2 = 1, and
Fn = Fn−1 + Fn−2 for n > 2.
Write a recursive function which calculates the nth Fibonacci number Fn for a given n.
Q2 Turtle Drawing: Write scripts to have the turtle module produce images like those below. See the
documentation at the link above to find the functions needed.
4 Common errors
❼ RuntimeError: maximum recursion depth exceeded
This error message occurs when your code exceeds the maximum number of recursions for Python.
You have probably forgotten to include a base case; or your base case can never be accessed.
4