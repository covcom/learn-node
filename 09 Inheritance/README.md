
# Inheritance

Work through before first lab in Teaching Week 9
Author: Dr Matthew England (Coventry University)
Contents
1 Inheritance 2
1.1 Inheriting in Python . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 2
1.2 Checking an instance . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 3
1.3 Method overwriting . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 4
2 More complicated inheritance features 4
2.1 Inheriting from multiple classes . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 4
2.2 Protected Access . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 5
3 Class Hierarchies 6
4 Exercise 8
1
121COM: Introduction to Computing Worksheet 9: Inheritance
1 Inheritance
Inheritance is the ability to define a new class as an extension of an existing class. It is considered one of
the key features of object-oriented programming.
The term inheritance is used because the new class inherits the methods and attributes of the existing
class. It is also common to refer to the existing class as the parent and the new class as the child. The
more technical terms are superclass for the parent and subclass for the child.
It is possible to have further classes inheriting themselves from child classes, creating class hierarchies.
The key benefit of inheritance is code reuse:
❼ When we need different classes that have things in common we can avoid duplication by putting the
common code in a parent class.
❼ When we need a class that combines the functionality of two existing classes we can inherit from both.
1.1 Inheriting in Python
We demonstrate inheritance in Python by considering code regarding the behaviour of animals in a computer
game. All the animals will have a name, species and an id and access to a method walk. The code in
Animal1.py implements this.
Animal1.py
1 class Animal :
2
3 counter =1 # Class attribute to producing unique ids for each animal .
4
5 def __init__ (self , name , species , colour ):
6 self . name = name
7 self .id = Animal . counter
8 Animal . counter = Animal . counter +1
9 self . species = species
10 self . colour = colour
11
12 def __str__ ( self ):
13 return ("A " + self . colour + " " + self . species + " called " + self . name )
14
15 def wander ( self ):
16 print ( self . name + " is wandering ")
With the class Animal defined we can define animals as below.
>>> a1 = Animal("Clifford", "Dog", "Red")
>>> a2 = Animal("Tweety", "Bird", "Yellow")
>>> print(a1)
A Red Dog called Clifford
>>> print(a2)
A Yellow Bird called Tweety
>>> a1.wander()
Clifford is wandering
Of course, in a finished game instead of printing the final line we would cause the animated dog to move.
Although the two objects defined are both animals, we may want them to have distinct features related
to their species. For example, dogs might be friendly or not; and only dogs can bark while only birds can
fly. We can create separate classes for the species which inherit from Animal. The syntax is to include the
parent class name in parenthesis following the child class name in the header of the child class definition.
2
121COM: Introduction to Computing Worksheet 9: Inheritance
Animal2.py
1 # With class Animal already defined as in Animal1 .py
2
3 class Dog ( Animal ):
4 def __init__ (self , name , colour , friendly ):
5 Animal . __init__ (self , name , "Dog", colour )
6 self . friendly = friendly # Should be Boolean
7 def bark ( self ):
8 if self . friendly == True :
9 print ("Yap!")
10 else :
11 print (" Grrrrr ")
12
13 class Bird ( Animal ):
14 def __init__ (self , name , colour ):
15 Animal . __init__ (self , name , " Bird ", colour )
16 def fly ( self ):
17 print ( self . name + " is flying ")
We can now define the animals from their subclasses.
>>> a1 = Dog("Clifford", "Red", True)
>>> print(a1)
A Red Dog called Clifford
>>> a1.wander()
Clifford is wandering
>>> a1.bark()
Yap!
>>> a2 = Bird("Tweety", "Yellow")
>>> a2.fly()
Tweety is flying
Note the following from the examples above:
❼ In the instantiation method of the child classes we called the instantiator for the parent class. If we
had not, then the attributes name, species and colour would not have been set and so any method
which tried to use these would trigger an error.
❼ When defining from the subclass we did not require the user to enter the species as it was implied.
However, the user does now have to provide the dog class specific attribute friendly.
❼ The animals now have access to their new methods fly and bark but also the parent method wander.
Also, note that the parent method __str__ is still being called by print.
1.2 Checking an instance
If we apply the type function it identifies the child class. However, there is another built-in function
isinstance which tests for membership of a particular class. It shows that a1 is both an instance of class
Animal and class Dog.
>>> type(a1)
<class ’__main__.Dog’>
>>> isinstance(a1, Dog)
True
>>> isinstance(a1,Animal)
True
3
121COM: Introduction to Computing Worksheet 9: Inheritance
1.3 Method overwriting
If desired, a child class can override a method or attribute of the parent class. For example, in the new Dog
class definition below we have redefined how the objects are represented as strings.
Animal3.py
1 class Dog ( Animal ):
2
3 def __init__ (self , name , colour , friendly ):
4 Animal . __init__ (self , name , "Dog", colour )
5 self . friendly = friendly # Should be Boolean
6
7 def __str__ ( self ):
8 if self . friendly == True :
9 return ( Animal . __str__ ( self ) )
10 else :
11 return (" Run !!!")
>>> a3 = Dog("Spike", "Blue", False)
>>> print(a3)
Run!!!
2 More complicated inheritance features
2.1 Inheriting from multiple classes
It is possible to define a class which inherits from two (or more) parent classes. Consider the following two
scripts which defines separate classes for representing the time and date respectively.
Time.py
1 class Time ( object ):
2
3 def __init__ (self , hours =0 , minutes =0):
4 self . __hr = hours
5 self . __min = minutes
6
7 def tick ( self ):
8 """ Time advances by one minute """
9 if self . __min ==59:
10 self . __min = 0
11 if self . __hr ==23:
12 self . __hr = 0
13 else :
14 self . __hr = self . __hr +1
15 else :
16 self . __min += 1
17
18 def __str__ ( self ):
19 return ( str( self . __hr ) + ":" + str( self . __min ) )
>>> clock = Time(14,33)
>>> clock.tick()
>>> print(clock)
14:34
4
121COM: Introduction to Computing Worksheet 9: Inheritance
Date.py
1 class Date ( object ):
2 M = (0 ,31 ,28 ,31 ,30 ,31 ,30 ,31 ,31 ,30 ,31 ,30 ,31)
3
4 def __init__ (self , day =1 , month =1 , year =2015):
5 self . __day = day
6 self . __month = month
7 self . __year = year
8
9 def forward ( self ):
10 numDays = Date . M [ self . __month ]
11 if self . __day == numDays :
12 self . __day = 1
13 if ( self . __month == 12):
14 self . __month = 1
15 self . __year += 1
16 else :
17 self . __month += 1
18 else :
19 self . __day += 1
20
21 def __str__ ( self ):
22 return str( self . __day )+"-"+ str( self . __month )+ "-"+ str( self . __year )
>>> calendar = Date(31,1,2015)
>>> calendar.forward()
>>> print(calendar)
1-2-2015
We create a third class, which is a child two both Time and Date, which will record both the date and time.
DateTime.py
1 from Date import Date
2 from Time import Time
3
4 class DateTime ( Date , Time ):
5 def __init__ (self , day , month , year , hours , minutes ):
6 Date . __init__ (self , day , month , year )
7 Time . __init__ (self , hours , minutes )
8 def __str__ ( self ):
9 return Date . __str__ ( self ) + ", " + Time . __str__ ( self )
>>> watch = DateTime(28,11,2015,23,42)
>>> print(watch)
28-11-2015, 23:42
>>> watch.tick()
>>> print(watch)
28-11-2015, 23:43
2.2 Protected Access
Note that as written above, the watch will go wrong when the time passes midnight. We will need to write
new code which links the date and time functionality together. One difficulty here will be that the DateTime
class cannot access the Date and Time attributes as they are private. To overcome this many languages have
a third class of access for attributes besides private and public: protected access is when an attribute can
5
121COM: Introduction to Computing Worksheet 9: Inheritance
only be accessed from inside its class, or any other classes that inherit from it. Python does not support
this feature, but developers often start attribute names with a single underscore to indicate that this is their
intended use. I.e., we would replace all occurrences of __day with _day etc.
3 Class Hierarchies
As mentioned at the start we can continue the inheritance process defining hierarchies of classes.
VehicleClasses.py
1 class Vehicle :
2 def __init__ (self , wheels , motor ):
3 self . wheels = wheels
4 self . motor = motor
5 def move ( self ):
6 print (" Vehicle moving ")
7
8 class Car ( Vehicle ):
9 def __init__ (self , doors ):
10 self . doors = doors
11 Vehicle . __init__ (self , 4 , True )
12 def openDoor (self , i ):
13 if i in range (1 , self . doors +1):
14 print (" Opening door ")
15 def rev ( self ):
16 print (" vroooom ")
17
18 class SmallCar ( Car ):
19 def __init__ ( self ):
20 Car . __init__ (self , 2)
21
22 class LargeCar ( Car ):
23 def __init__ ( self ):
24 Car . __init__ (self , 4)
25
26 class Bike ( Vehicle ):
27 def __init__ (self , motor ):
28 Vehicle . __init__ (self , 2 , motor )
29 def doWheelie ( self ):
30 print (" Doing Wheelie !")
31
32 class Bicycle ( Bike ):
33 def __init__ ( self ):
34 Bike . __init__ (self , False )
35
36 class MotorBike ( Bike ):
37 def __init__ ( self ):
38 Bike . __init__ (self , True )
39 def rev ( self ):
40 print (" vroooom ")
In VehicleClasses.py we define 7 different classes in a hierarchy. Note the following points:
❼ The hierarchy is 3 levels deep. No matter how deep the children still have access to the attributes and
methods from higher up. Objects from all 7 classes have the method move.
❼ The instantiation method for Car calls that of Vehicle. The method for SmallCar calls the method
for Car but not Vehicle (because the call to Car.__init__ itself calls Vehicle.__init__).
6
121COM: Introduction to Computing Worksheet 9: Inheritance
The diagram below is a class diagram showing the inheritance relationships. Each box is a class, with
each arrow pointing from a child to a parent. Within each class box there are lists of attributes and methods
defined (excluding instantiation). This is an example of a UML diagram (studied in detail in module 104KM).
It can often be useful to plan code by first drawing such diagrams in order to identify the best choice
of hierarchy. For example, in the code above we defined the rev method twice (once for cars and again for
motorbikes). We could avoid this by introducing an eighth class for motorised vehicles which defines the
method and inherits it to both subclasses. Adding the extra class may seem like more work, but it makes
the project more manageable: when we need to edit the rev code it is in one place.
7
121COM: Introduction to Computing Worksheet 9: Inheritance
If we are unsure about a hierarchy we can always check the parents of a class by viewing the special
attribute __bases__. For example, with the code defining the second diagram:
>>> MotorBike.__bases__
(<class ’__main__.Bike’>, <class ’__main__.MotorisedVehicle’>)
>>> Bike.__bases__
(<class ’__main__.Vehicle’>,)
Note that __bases__ is an attribute of the class, not the instances. If we ask for the parents of the class
Vehicle we get a surprising result:
>>> Vehicle.__bases__
(<class ’object’>,)
Vehicle inherits from the built-in class object. This is the default if no other parent class is specified. In
fact, all classes exist in a single hierarchy and eventually inherit from object, which is the only class to have
no parent.
>>> object.__bases__
()
4 Exercise
Create code to implement a database of people in a university. There should be a parent class Person and
sub-classes Staff and Student. Create further subclasses for the different types of staff (Academic and
SupportStaff) and student (Undergraduate and Postgraduate).
Attributes should include name, id, address, officePhone, salary, jobTitle, modulesTaught, fees,
courseEnrolled, modulesTaken. Place these in the classes so that you avoid code duplication but that they
are only available to the appropriate people. Consider which attributes should be private; and write accessor
and mutator methods where appropriate.
Start the exercise by planning your code with a class diagram. Finish by writing some tests that demonstrate
the functionality of your database.
8