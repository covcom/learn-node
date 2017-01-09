
# Working with Data

Work through before first lab in Teaching Week 6
Author: Dr Matthew England (Coventry University)
Contents
1 Data Structures 2
1.1 Tuples . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 2
1.2 Sets . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 3
1.3 Dictionaries . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 4
2 Files 6
2.1 Open, close, read and write . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 6
2.2 Pickling . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 7
3 Exercises 8
4 Common errors 8
1
121COM: Introduction to Computing Worksheet 6: Working with Data
1 Data Structures
A data structure is a way of organizing data in a computer / program. We have already met one Python
data structure: the list datatype. This was a type of sequence (ordered collection of values) which we
defined with square brackets around a comma separated sequence of values. Revisit the Week 3 material for
more details. Here we consider some of the other data structures available in Python
1.1 Tuples
A tuple is another of Python’s data structure which implements sequences. We define them with round
brackets around a comma separated sequence of values.
>>> t = (1,2,3)
(1,2,3)
>>> type(t)
<class ’tuple’>
Since tuples are sequences they support the sequence operations common to lists and strings.
>>> t[0:2]
(1,2)
>>> t[-1]
3
Note that just like lists tuples index from 0. Also like lists, tuples can store data of different types, including
more tuples.
>>> t = ("hello", 100, True, ("a", "b", "c"))
>>> t[3][1]
"b"
The main difference between tuples and lists is that lists are mutable and tuples immutable. This means
that you can edit the individual elements in a list but not a tuple (trying to do so will trigger a type error).
Tuples should be used to store data that will not change during the program (e.g. months of the year).
We can use tuples to assign multiple values at once.
>>> (x,y) = (2,4)
>>> y
4
This offers a useful way to swap variables, since with tuple assignment all assignments are done together
rather than one by one.
>>> (x,y) = (y,x)
>> y
2
Note that to create a tuple with just one element it is necessary to include a comma (otherwise the round
brackets are treated as regular parenthesis and so have no effect).
>>> t1 = ("hello")
>>> t2 = ("hello",)
>>> type(t1)
<class ’str’>
>>> type(t2)
<class ’tuple’>
An empty tuple is created simply using ().
2
121COM: Introduction to Computing Worksheet 6: Working with Data
1.2 Sets
A set is an unordered collection of unique values. Sets differ from sequences is two main ways: (1) the order
of elements is not relevant; (2) there cannot be duplicate elements. They are implemented in Python as the
set datatype and constructed via a comma separated sequence of values inside curly brackets.
>>> s = {4,4,4,3,5,6,6,10}
>>> type(s)
<class ’set’>
While sets may be defined with a given order and duplicates they will not be stored that way. For example,
if we call the set s defined above we see the duplicates have been removed and the order is different.
>>> s
{10, 3, 4, 5, 6}
Note that the order is not intuitive. Since a set is not a sequence we cannot use the sequence operators like
slice. However, there do exist functions for set operations such as union for combining sets; intersection
for finding elements common to both and difference for finding elements in one but not another.
>>> hasMetro = {"London", "Glasgow"}
>>> hasRingroad = {"London", "Coventry"}
>>> hasEither = hasMetro.union(hasRingroad)
>>> hasEither
{’Glasgow’, ’London’, ’Coventry’}
>>> hasBoth = hasMetro.intersection(hasRingroad)
>>> hasBoth
{’London’}
Note that it does not matter what order the parameters are for union and intersection. However, it does
matter for difference:
>>> noRingroad = hasMetro.difference(hasRingRoad)
>>> noRingroad
{’Glasgow’}
>>> noMetro = hasRingroad.difference(hasMetro)
>>> noMetro
{’Coventry’}
Sets are most useful when a program has need for these operations.
Sets are mutable, although there is an immutable version available called frozenset.
Note that to define an empty set you must used set() instead of { }. The latter defines an empty
dictionary, our next topic.
3
121COM: Introduction to Computing Worksheet 6: Working with Data
1.3 Dictionaries
A dictionary is a data structure where data is accessed by referring to another piece of data. Another name
for this data structure is an associative array. Dictionaries consist of key-value pairs where the key is
used to access the values. They are analogous with actual dictionaries where we find the definition of a word
by looking up the word itself.
The data structure is implemented in the dict datatype, and is defined with curly brackets around a
comma separated sequence of key values pairs in which the keys and values are connected by colons (:).
The next example defines a dictionary for translating between English and Spanish numbers. The English
words are the keys and the Spanish words the values.
>>> eng2sp = { "one":"uno", "two":"dos", "three":"tres" }
>>> eng2sp
{’one’: ’uno’, ’three’: ’tres’, ’two’: ’dos’}
The presence of the colons indicates we are defining a dictionary rather than a set. The empty case is the
only possibility for confusion: as noted above, {} defines an empty dictionary.
Note also that the order in which the pairs are entered does not matter. Indeed, the order in which
Python prints the dictionary may be different to that shown above and different to the order we entered it.
The dictionary is indexed not by the order, but by its keys.
>>> eng2sp["two"]
"dos"
We can add additional key-value pairs by assigning a value to the dictionary indexed at the new key as
follows:
>>> eng2sp ["four"] = "cuatro"
>>> end2sp
{’one’: ’uno’, ’four’: ’cuatro’, ’three’: ’tres’, ’two’: ’dos’}
Dictionaries are mutable, so we can edit and update the values. For example
>>> stock = {"oranges":55, "apples":43, "bananas":31}
>>> stock["apples"] = stock["apples"]-3
>>> stock
{’bananas’: 31, ’oranges’: 55, ’apples’: 40}
The keys cannot be edited. We can remove a key-value pair entirely we use the del keyword:
>>> del stock["bananas"]
>>> stock
{’oranges’: 55, ’apples’: 40}
Like sequences, we can test for inclusion in dictionaries using the in operator. Note that this looks for keys
not values.
>>> "oranges" in stock
True
>>> "tres" in eng2sp
False
We can hence use loops to traverse through dictionaries by key.
Also like lists there are numerous methods defined for working with dictionaries (see the help documentation
for full details). Three particularly useful ones are keys, values and items. The first returns all the
keys in a dictionary, the second all the values and the third all the pairs where each pair is a tuple with first
entry the key and second entry the value.
4
121COM: Introduction to Computing Worksheet 6: Working with Data
>>> eng2sp.keys()
dict_keys([’four’, ’three’, ’two’])
>>> eng2sp.values()
dict_values([’cuatro’, ’tres’, ’dos’])
>>> stock.items()
dict_items([(’oranges’, 55), (’apples’, 40)])
In Python 3 these are stored as dictionary view objects which change with the dictionary, but they can
be easily converted to lists using the built in list function.
>>> list(stock.items())
[(’oranges’, 55), (’apples’, 40)]
If we try to access a key that does not exist in the dictionary we get a key error. The get method is useful
for avoiding this: given a key it returns the value if in the dictionary; or None otherwise.
>>> stock.get("apples")
40
>>> k = stock.get("kiwis")
>>> type(k)
<class ’NoneType’>
The values in a dictionary can be anything, but the keys must be something immutable. Thus keys can
be tuples and strings but not lists or other dictionaries. Suppose we wanted a dictionary for a timetable
where the keys were days and hours and the values what we should be doing. We must encode the days and
hours into tuples, not lists.
Timetable.py
1 # Define timetable dictionary
2 timetable = { ("Mon" ,9):"121 COM", ("Mon", 3):"ALL", ("Wed", 10): "121 COM"}
3 timetable [("Fri", 5)] = " Party !"
4
5 # Print out timetable
6 for K in timetable :
7 print (K , timetable [ K ])
8
9 # Function to say where I should be
10 def whatNow ( Day , Time ):
11 Value = timetable . get (( Day , Time ))
12 if Value == None :
13 print (" Free ")
14 else :
15 print ( Value )
The script Timetable.py produced output
(’Wed’, 10) 121COM
(’Mon’, 3) ALL
(’Fri’, 5) Party!
(’Mon’, 9) 121COM
>>> whatNow("Wed", 10)
121COM
>>> whatNow("Mon", 12)
Free
5
121COM: Introduction to Computing Worksheet 6: Working with Data
2 Files
2.1 Open, close, read and write
We can use files to store data outside of a particular program, so that it does not need to be recomputed the
next time you need it. To work with a file we must first open it, using the built in open function. The first
argument should be the name of a file (including the file extension) as a string; and the second argument
the mode. There are three main modes:
"r" for reading a file. The file must already exist in the directory we are working.
"w" for writing into a new file. If the file does not exist it is created and if it does exist it is overwritten.
"a" : for appending into an existing file. If the file already exists anything written is appended to the end.
If the file does not exist it is created.
There are many other modes available (see documentation for more details). The output of open is a special
datatype for files.
>>> f = open("test.txt", "w")
>>> f
<_io.TextIOWrapper name=’test.txt’ mode=’w’ encoding=’cp1252’>
>>> type(f)
<class ’_io.TextIOWrapper’>
This special datatype has two particularly useful methods:
read When opened with mode "r" the method read outputs the contents of the file as a string.
write When opened with mode "w" or "a" the method write takes a parameter as string and writes it to
the end of the file.
A third method is close which closes the file on the filesystem. All programs that work with files should
ideally ensure that all files are closed before exiting (even when errors are triggered).
The following scripts demonstrate these commands. In the first I created a text file called address.txt
and wrote my address into it. In the second I added the postcode and then in the third I read the file.
File1.py
1 f = open (" Address .txt", "w")
2 f . write ("Dr Matthew England ")
3 f . write ("\ nEngineering & Computing Building \ nCoventry University \ nCoventry ")
4 f . close ()
File2.py
1 f = open (" Address .txt", "a")
2 f . write ("\ nCV1 5FB\n")
3 f . close ()
File3.py
1 f = open (" Address .txt", "r")
2 text = f . read ()
3 print ( text )
4 f . close ()
6
121COM: Introduction to Computing Worksheet 6: Working with Data
The third file will give an error unless the above have been run, and so the file already created. Note
that these are separate files and could be run in separate IDLE sessions without making a difference. After
running them you should be able to see the text file in your current directory which you can work with like
any other text file.
Note the presence of the special characters \n in the string. These create new lines in the text file. The
file object can make use of these to break the file up. For example, the method readline will output just
one line (the next line) from an open file. Alternatively, if we iterate over a file the loop parameters takes
the value of each line, as in the next script.
File4.py
1 f = open (" Address .txt", "r")
2 for line in f :
3 print ( line )
4 f . close ()
Note that the print command adds its own new line character on top of the one already there. Working
line by line is useful if we want to edit each line as in this last script to right align the address.
File5.py
1 f = open (" Address .txt", "r")
2 for line in f :
3 text = line [0: -1]
4 text = (60 - len( text ))*" " + text
5 print ( text )
6 f . close ()
2.2 Pickling
The above commands are fine for storing strings in files. However, to store anything else we must first
convert to a string, and even then, we lose the original type information or data structure. The pickle is
designed to preserve this information. It introduces two key functions:
dump The first argument is the piece of data to be preserved and the second argument an open file which
accepts writing in bytes. The function will write the data in a way that it can be recovered.
load This function takes one argument, an open file which can be read in bytes, and reconstructs the data
within (assuming it was written with pickle.dump).
The following two scripts demonstrate these commands. Note that the mode used when opening the file
are "wb" and "rb". The additional b is to signify the reading and writing is done with bytes rather than
strings, which is how pickle works. If you tried to view the file in a text browser it would no longer look
like the data it represents. In PickleLoad.py note that we can call pickle.load as many times as we called
pickle.dump. Each time we recover a piece of data (in the order they were dumped) complete with its type.
Note however, that we do not recover the variable name the data was assigned to.
PickleDump.py
1 import pickle
2 f = open (" DataStore .txt", "wb")
3 x = [1 ,2 ,3 ,4 ,5]
4 y = True
5 z = " Hello "
6 pickle . dump (x , f )
7 pickle . dump (y , f )
8 pickle . dump (z , f )
9 f . close ()
7
121COM: Introduction to Computing Worksheet 6: Working with Data
PickleLoad.py
1 import pickle
2 f = open (" DataStore .txt", "rb")
3 x = pickle . load ( f )
4 y = pickle . load ( f )
5 z = pickle . load ( f )
6 f . close ()
3 Exercises
Q1 Data Structures:
(a) Create a function which accepts a number between 1 and 12 and returns the name of the month in
text. Use tuples in the implementation.
(b) Write a script which takes the Spanish to English dictionary from Section 1.3 and creates an English
to Spanish dictionary. Why might this be more difficult for a general dictionary?
(c) Consider rolling two 6-sided dice and calculating the sum. Create a dictionary whose keys are the
possible sums and values those combinations which add to the sum. Which sum is the most likely?
Q2 Files: Use the text file Boring.txt on Moodle to test these (or find a more interesting one).
(a) Write a function which takes a string with a text file name; and reverses the order in which the
lines of text are written in the file.
(b) Write a function called pager. The input should be a file name. The function should print the
contents of the file 5 lines at a time, pausing each time until the user presses a key to continue.
Q3 Pickling: Save your dictionary from Q1c into a file and then access it from a separate Python session.
4 Common errors
❼ TypeError: ’tuple’ object does not support item assignment
This message occurs if you try to edit a tuple element. Tuples are immutable so you cannot do this.
❼ KeyError: keyName
This occurs if you are trying to access a value with a key not present in the dictionary.
❼ ValueError: I/O operation on closed file.
You are trying to work with a closed file
❼ io.UnsupportedOperation: not writable
You are trying to write to a file opened for reading. Similarly not readable will occur if you try to
read a file opened for writing.
❼ FileNotFoundError: [Errno 2] No such file or directory: ’<FileName>.txt’
You are trying to open a file which does not exist yet. Use mode "w".
❼ TypeError: must be str, not bytes
Would occur if you use pickle.dump but did not open a file to accept bytes. Use mode "wb".
❼ TypeError: ’str’ does not support the buffer interface
Would occur if you use pickle.load but did not open a file to read as bytes. Use mode "rb".
❼ EOFError: Ran out of input
This could occur if you tried using pickle.load more times than you used pickle.dump.
8