
Here are a brief study notes of Python for later quick review. 

Materials are based on: 

* Python 101 written by Michael Driscoll at https://python101.pythonlibrary.org/

* A Byte of Python at https://python.swaroopch.com/

* Python documentation: https://docs.python.org/3/tutorial/datastructures.html

* Automate the boring stuff with Python by Al Sweigart (Chapter 1 - Chapter 6)

## Basics 
Python is an interpretive language and runs in Python interpreter. 


```python
print('Hello World')
```

    Hello World


### Strings 
Strings are immutable types 

* Create strings with single, double or triple quotes. 
* Concatenate strings with + 
* String methods such as len, upper, lower ... 
* String slicing with $[i, j]$
* String formatting and substitutioin similar as in C
* Raw string can be used if strings without special processing such as escape are needed, e.g., r "Raw string. \n"
* some useful string methods such as `startswith`, `in`, `find`, `join` ...



```python
# Creation
mystring = "test string"
newstring = "new"
mystring

```




    'test string'




```python
# concatenation
newest = mystring + newstring 
print(newest)
print(id(newest))
```

    test stringnew
    139842324890096



```python
# String methods 

# upper case 
newest.upper()
```




    'TEST STRINGNEW'




```python
# lenth 
len(newest)
```




    14




```python
# help 
help(len)
```

    Help on built-in function len in module builtins:
    
    len(obj, /)
        Return the number of items in a container.
    



```python
# types of string
type(newest)
```




    str




```python
# slicing 
newest[0:1]  # start from loc 0, up to loc 1 BUT not include loc 1
```




    't'




```python
newest[:]
```




    'test stringnew'




```python
newest[0:-5] # ends 5 characters before the end of the string 
```




    'test stri'




```python
# string formatting 
string1 = 'I like %s' %'sleeping'
string1
```




    'I like sleeping'




```python
float_string = '%.2f' %(1.23423) # round to second decimal places 
float_string
```




    '1.23'




```python
# use %s with a variable inside for formatting 
print("%(lang)s is fun" %{"lang":"Python"}) # use dictionary to define the value for key lang
```

    Python is fun


### Raw string 


```python
newstring = r"Newlines are indicated by \n"
print(newstring)
```

    Newlines are indicated by \n


### String methods

* upper(), lower(), isupper(), islower()

* isalpha(), isalnum(), isdecimal(), isdigit(), isspace()...

* startswith(), endswith()

* join(), split()



```python
newstr = 'coolpython'

if newstr.startswith('co'):
    print('newstr starts with \'co\' ')

# in 
if 'py' in newstr:
    print('py in newstr')

# find: returns -1 if not in the string  
if newstr.find('th') != -1: 
    print('th is in newstr')
    
# join: join items of sequences with a string acting as delimiter

delimiter = '_*_'
fruit = ['apple', 'orange', 'peach']
print(delimiter.join(fruit))

# split 
test = 'My name is Simon.'
print(test.split())

print(test.split('m'))
```

    newstr starts with 'co' 
    py in newstr
    th is in newstr
    apple_*_orange_*_peach
    ['My', 'name', 'is', 'Simon.']
    ['My na', 'e is Si', 'on.']


#### String formatting with %s 


```python
name = 'Alice'
place = 'Main Street'
time = '6pm'
newstr = 'Hello %s, you are invited to a party at %s at %s.' %(name, place, time)
print(newstr)
```

    Hello Alice, you are invited to a party at Main Street at 6pm.


## Modules 

Modules are used when you want to re-use a number of functions in other programs that you write.  Methods to write modules include: 

* Create a file with .py extension that contains functions and variables. 
* Write modules in the native language in which Python interpreter itself was written, for example, C language. 

Every module has an attribute `__name__`, and the statements in the module can find out this name. The purpose is to figure out whether the module is **being run alone (__name__ == '__main__) or being imported (__name__ = module name)**. 

* `dir(module_name)` function returns a list of functions, classes and variables in a module.


```python
# use standard library modules 
import sys 
print('The command line arguments are:')
for i in sys.argv:
    print(i)
    
print('\n The python path is', sys.path, '\n')
```

    The command line arguments are:
    /usr/local/lib/python3.6/site-packages/ipykernel_launcher.py
    -f
    /run/user/1000/jupyter/kernel-ebbb89b3-02de-417b-b1da-b410d50d2284.json
    
     The python path is ['', '/usr/local/lib/python36.zip', '/usr/local/lib/python3.6', '/usr/local/lib/python3.6/lib-dynload', '/home/qshan/.local/lib/python3.6/site-packages', '/usr/local/lib/python3.6/site-packages', '/usr/local/lib/python3.6/site-packages/IPython/extensions', '/home/qshan/.ipython'] 
    


### Test \__name__ attribue 


```python
# make up a file 
if __name__ == '__main__':
    print('This program has name main.')
else:
    print('This program is imported from another module.')
    print(__name__)
# save the above file in a test python file called module_using_name
```

    This program has name main.



```python
import module_using_name
```

    This program is imported from another module.
    module_using_name


### `dir()` function


```python
dir()
```




    ['In',
     'Out',
     '_',
     '__',
     '___',
     '__builtin__',
     '__builtins__',
     '__doc__',
     '__loader__',
     '__name__',
     '__package__',
     '__spec__',
     '_dh',
     '_i',
     '_i1',
     '_i10',
     '_i11',
     '_i12',
     '_i13',
     '_i14',
     '_i15',
     '_i2',
     '_i3',
     '_i4',
     '_i5',
     '_i6',
     '_i7',
     '_i8',
     '_i9',
     '_ih',
     '_ii',
     '_iii',
     '_oh',
     'exit',
     'get_ipython',
     'i',
     'module_using_name',
     'newstring',
     'quit',
     'sys']



## Data Structures

* list, mutable,  a data structure that holds an ordered collection of items enclosed in square brackets. A list is an example of usage of objects and classes. 

* List can be used as stacks and queues. 

 --- 

* tuple, immutable, hold together multiple objects. Tuples are defined by specifying items separated by commas within an optional pair of parentheses.

* dictionary contains pairs of keys (unique, immutable) and values (mutable). The dictionaries are instances/objects of the dict class.


* set, unordered collections of simple objects. Can test membership, subset, intersection between two sets and so on.



### List example 


```python
# list example 
shoplist = ['apple', 'mango', 'carrot', 'banana']


print('These items are: ', end = ' ')
for item in shoplist:
    print(item, end=' ')

print('\nI also have to buy rice.')
shoplist.append('rice')
print('My shopping list is updated as ', shoplist)



print('Don\'t want to buy', shoplist[0])

del shoplist[0]
print('My shopping list is updated as', shoplist)

# add two lists 

list1 = ['a', 'b']
list2 = ['c', 'd']
print(list1 + list2)
```

    These items are:  apple mango carrot banana 
    I also have to buy rice.
    My shopping list is updated as  ['apple', 'mango', 'carrot', 'banana', 'rice']
    Don't want to buy apple
    My shopping list is updated as ['mango', 'carrot', 'banana', 'rice']
    ['a', 'b', 'c', 'd']



```python
## More list examples 
fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
fruits.count('apple')
```




    2




```python
fruits.index('apple')  # the index of the first item 
```




    1




```python
fruits.index('apple', 4) # find next apple starting at position 4   
```




    5




```python
fruits.reverse()  # reverse the elements in place 
fruits
```




    ['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']




```python
fruits.append('grape') # equivalent to a[len(a):] = [x]
fruits
```




    ['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange', 'grape']




```python
fruits.sort(reverse = True)
fruits
```




    ['pear', 'orange', 'kiwi', 'grape', 'banana', 'banana', 'apple', 'apple']




```python
# copy a list 
newfruits = fruits.copy()  # equivalent to a[:]
newfruits
```




    ['pear', 'orange', 'kiwi', 'grape', 'banana', 'banana', 'apple', 'apple']




```python
# insert a value 
fruits.insert(0, 'new')
fruits
```




    ['new',
     'pear',
     'orange',
     'kiwi',
     'grape',
     'banana',
     'banana',
     'apple',
     'apple']




```python
# remove a value by specifying the value 
fruits.remove('new') # remove the first item in the list whose value is x 
fruits
```




    ['pear', 'orange', 'kiwi', 'grape', 'banana', 'banana', 'apple', 'apple']




```python
# remove a value by specifying the index 
del fruits[0:2]
fruits
```




    ['kiwi', 'grape', 'banana', 'banana', 'apple', 'apple']




```python
# delete the entire list 
del fruits
fruits
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-40-6994f1ab6535> in <module>()
          1 # delete the entire varible
          2 del fruits
    ----> 3 fruits
    

    NameError: name 'fruits' is not defined



```python
# list a string 
list('hello')
```




    ['h', 'e', 'l', 'l', 'o']



#### Sort list 


```python
spam = ['ant', 'dog', 'cat', 'banana']
spam.sort()
spam
```




    ['ant', 'banana', 'cat', 'dog']




```python
# if there are both lower case and upper case 
spam = ['Alice', 'ant', 'cat', 'Bot', 'dog']
spam.sort()
print(spam)  # sort bu ASCII

# use str.lower key to sort by dictionary order 
spam.sort(key = str.lower)
spam
```

    ['Alice', 'Bot', 'ant', 'cat', 'dog']





    ['Alice', 'ant', 'Bot', 'cat', 'dog']



#### Use list as stacks 


```python
# last-in, first out 
stack = [3, 4, 5]
stack.append(6)
stack.append(7)
stack
```




    [3, 4, 5, 6, 7]




```python
# pop 
stack.pop()
```




    7




```python
stack
```




    [3, 4, 5, 6]




```python
stack.pop()
stack
```




    [3, 4, 5]



#### Use list as queues (first in, first out) 

* Lists are NOT efficient as inserts / pops from the beginning of a list is slow ( all other elementss have to be shifted by one). 

* Use `collections.deque` to implement a queue, which has fast appends and pops from both ends. 



```python
from collections import deque 
queue = deque(['Eric', 'John', 'Michael'])
queue.append('Terry')
queue.append('Graham')
queue 
```




    deque(['Eric', 'John', 'Michael', 'Terry', 'Graham'])




```python
# pop 
queue.popleft()
```




    'Eric'




```python
queue
```




    deque(['John', 'Michael', 'Terry', 'Graham'])



#### List comprehensions

It provides a concise way to create new lists based on operations applied to another list or iterable. 


```python
# create a list 
squares = [x**2 for x in range(10)]
squares
```




    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]




```python
# or use map 
squares = list(map(lambda x: x**2, range(10)))
squares
```




    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]




```python
# the expression is a tuple (x, y), it must be paranthesized 
[(x, y) for x in [1, 2, 3] for y in [3, 1, 4] if x != y]
```




    [(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]



### Tuples


```python
# tuple example 
zoo = ('python', 'elephant', 'penguin')
print('Number of animals in the zoo is', len(zoo))

new_zoo = 'monkey', 'camel', zoo # parentheses not required but recommended
print('Number of cages in the new zoo is', len(new_zoo))
```

    Number of animals in the zoo is 3
    Number of cages in the new zoo is 3



```python
t = 12345, 54321, 'hello'
type(t)
```




    tuple




```python
t
```




    (12345, 54321, 'hello')




```python
u = t, (1, 2, 3, 4, 5)  # nested tuple 
u
```




    ((12345, 54321, 'hello'), (1, 2, 3, 4, 5))



##### Passing tuples around 


```python
# return multiple values 
def get_person_info():
    return(1, "Statistics")


ids, major = get_person_info()
(ids, major)
```




    (1, 'Statistics')




```python
# assign the first value to a, and the rest of values to b 
a, *b = [1, 2, 3, 4]
print('a: {0}'.format(a))
print('b: {0}'.format(b))

# swap a and b 
a = 1; b = 2
a, b = b, a
print('a: {0}'.format(a))
print('b: {0}'.format(b))
```

    a: 1
    b: [2, 3, 4]
    a: 2
    b: 1


### Dictionary


```python
# dictionary example 

ab = {
    'Swaroop': 'swaroop@swaroopch.com',
    'Larry': 'larry@wall.org',
    'Matsumoto': 'matz@ruby-lang.org',
    'Spammer': 'spammer@hotmail.com'
}

print("Swaroop's address is", ab['Swaroop']) # specify the key 

# Deleting a key-value pair
del ab['Spammer']

# print contents in dictionary 
for name, address in ab.items():
    print('Contact {} at {}'.format(name, address))

# Adding a key-value pair
ab['Guido'] = 'guido@python.org'

if 'Guido' in ab:
    print("\nGuido's address is", ab['Guido'])
```

    Swaroop's address is swaroop@swaroopch.com
    Contact Swaroop at swaroop@swaroopch.com
    Contact Larry at larry@wall.org
    Contact Matsumoto at matz@ruby-lang.org
    
    Guido's address is guido@python.org



```python
# dict() constructor builds dictionaries directly from sequences of key-value pairs 
dict([('sape', 4178), ('guido', 4234)])
```




    {'guido': 4234, 'sape': 4178}




```python
# dict comprehension 
{x: x**2 for x in (2, 4, 6)}
```




    {2: 4, 4: 16, 6: 36}



#### Methods in dictionary

* keys()

* values()

* items()


```python
cat = {'name':'cat', 'age': '3', 'color':'orange'}
for v in cat.values():
    print(v)
```

    cat
    3
    orange



```python
for k in cat.keys():
    print(k)
```

    name
    age
    color



```python
for item in cat.items():
    print(item)
```

    ('name', 'cat')
    ('age', '3')
    ('color', 'orange')



```python
# or obtain a list from dict 
print(cat.keys())
print(list(cat.keys()))
```

    dict_keys(['name', 'age', 'color'])
    ['name', 'age', 'color']


#### Use `get()` and `setdefault()`


```python
# use get to search if a key is in dict, and return a default value if not 
print(cat.get('age', 0))
print(cat.get('new', 0))
```

    3
    0



```python

# use setdefault to given a key a default value when using it while it doesn't exist 
import pprint
message = 'It was a bright warm day in March.'
count = {}

for char in message:
    count.setdefault(char, 0)
    count[char] += count[char] + 1
pprint.pprint(count)
```

    {' ': 127,
     '.': 1,
     'I': 1,
     'M': 1,
     'a': 31,
     'b': 1,
     'c': 1,
     'd': 1,
     'g': 1,
     'h': 3,
     'i': 3,
     'm': 1,
     'n': 1,
     'r': 7,
     's': 1,
     't': 3,
     'w': 3,
     'y': 1}


To summarize, lists, tuples and strings are all examples of sequences that can do
    
   * membership tests (in and not in)
   * indexing operations 
   * slicing



### Set 

* Created by curly braces or `set()`, curly braces can NOT create empty set and `set()` can. 


```python
basket = {'apple', 'orange', 'apple', 'orange'}
basket  # no duplicates
```




    {'apple', 'orange'}




```python
# operations 
a = set('abcdefghijk')
b = set('jklmnopq')
a
```




    {'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k'}




```python
a - b
```




    {'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i'}




```python
a | b
```




    {'a',
     'b',
     'c',
     'd',
     'e',
     'f',
     'g',
     'h',
     'i',
     'j',
     'k',
     'l',
     'm',
     'n',
     'o',
     'p',
     'q'}




```python
a ^ b  # in a or b, but NOT both 
```




    {'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'l', 'm', 'n', 'o', 'p', 'q'}




```python
a & b 
```




    {'j', 'k'}




```python
# list comprehensions in set 
a = {x for x in 'abcdefg' if x not in 'abc'}
a
```




    {'d', 'e', 'f', 'g'}




```python
# set example 
egset = set(['brazil', 'russia', 'india'])
print('russia' in egset) 

egset.add('china')
print('china' in egset) 

print(egset.issuperset(egset))

newset = egset.copy()
newset.remove('brazil')

# intersection 
egset & newset
```

    True
    True
    True





    {'china', 'india', 'russia'}



### References 

When creating an object and assign it to a variable, the variable only referes to the object and doesn't represent the object itself (variable names points to the part of computer memory where the object is stored).  

* When making copies of a list or other sequences, need to use slicing operation to make a copy. See example below.


```python
# reference example 
test = ['apple', 'mango', 'orange', 'banana']
list1 = test 

print('Original list1 is', list1)

# delete one element from test 
del test[0]

print('list1 after deletion from test is', list1)

# do a full slice 
list2 = test[:]

# delement one element from test 
del test[0]
print('list1 is', list1)
print('list2 is', list2) # not affected 
```

    Original list1 is ['apple', 'mango', 'orange', 'banana']
    list1 after deletion from test is ['mango', 'orange', 'banana']
    list1 is ['orange', 'banana']
    list2 is ['mango', 'orange', 'banana']



```python
# passing reference 
def eggs(param):
    param.append('Hello')
test = [1, 2, 3]
eggs(test)
test
# we passed a reference, so the function modifies the test list directly even the function eggs returns nothing
```




    [1, 2, 3, 'Hello']




```python
#### Use copy to copy lists / dictionaries, not just referencing 
import copy 
spam = [1, 2, 3, 4]
cheese = copy.copy(spam)
cheese[1] = 42
# spam is not modified 
print('spam', spam)
print('cheese', cheese)
```

    spam [1, 2, 3, 4]
    cheese [1, 42, 3, 4]



```python
help(copy.deepcopy)
```

    Help on function deepcopy in module copy:
    
    deepcopy(x, memo=None, _nil=[])
        Deep copy operation on arbitrary Python objects.
        
        See the module's __doc__ string for more info.
    


## Object Oriented Programming
Combine data and functionality, and wrap them inside an **object**. Classes and objects are two main aspects of object oriented programming. 

* **Classes** created a new type where **objects** are _instances_ of the class.
* Variables that belong to an object or class are called as **fields**. 
* Functionality of objects are called **methods**.
* The **fields** and **methods** can be referred as **attributes** of a class.
* 
* **self** is like **this** in Java / C++. When calling MyObject.method(arg1, arg2), it automatically converts into MyClass.method(MyObject, arg1, arg2).

* \__init__ method is reversed by Python, it runs as soon as an object of the class is called. Usful to do initialization with the object. It's like the **constructor** function in Java / C++.

-- **fields** (data part) are ordinary variables which are bound to the **namespace** of classes and objects. 

-- Two types of fields: **class variables** (shared by all instances of the class) and **object** variables (owned by each individual object/instance).



```python
# a simple class with a simple object methods 
class Person():
    def sayHi(self):
        print('Hello!')
# test 
p = Person()
p.sayHi()
        
```

    Hello!



```python
# add __init__ method 
class Person():
    def __init__(self, name):
        self.name = name
    def sayHi(self):
        print('Hello', self.name)
# test 
p = Person("Cy")
p.sayHi()
```

    Hello Cy



```python
class Robot:
    """Represents a robot, with a name."""

    # A class variable, counting the number of robots
    population = 0

    def __init__(self, name):
        """Initializes the data."""
        self.name = name
        print("(Initializing {})".format(self.name))

        # When this person is created, the robot
        # adds to the population
        Robot.population += 1

    def __del__(self):
        """I am dying."""
        print("{} is being destroyed!".format(self.name))

        Robot.population -= 1

        if Robot.population == 0:
            print("{} was the last one.".format(self.name))
        else:
            print("There are still {:d} robots working.".format(
                Robot.population))

    def say_hi(self):
        """Greeting by the robot.

        Yeah, they can do that."""
        print("Greetings, my masters call me {}.".format(self.name))

    @classmethod
    def how_many(cls):
        """Prints the current population."""
        print("We have {:d} robots.".format(cls.population))


droid1 = Robot("R2-D2")
droid1.say_hi()
Robot.how_many()

droid2 = Robot("C-3PO")
droid2.say_hi()

```

    (Initializing R2-D2)
    R2-D2 is being destroyed!
    R2-D2 was the last one.
    Greetings, my masters call me R2-D2.
    We have 0 robots.
    (Initializing C-3PO)
    C-3PO is being destroyed!
    C-3PO was the last one.
    Greetings, my masters call me C-3PO.


#### Customization of classes 

The following example redefines the `__lt__` (Less Than) method in class `Interval`. 


```python
class Interval: 
    def __init__(self, left, right):
        self.left = left
        self.right = right 
    
    def __lt__(self, other):
        return self.left < other.left
    
if __name__ == "__main__":
    A = []
    A.append(Interval(1, 7))
    A.append(Interval(4, 5))
    A.append(Interval(2, 6))
    print('Before sorting:')
    for i in A:
        print("[{}, {}]".format(i.left, i.right))
    A.sort()
    print('After sorting:')
    for i in A:
        print('[{}, {}]'.format(i.left, i.right))
    
```

    Before sorting:
    [1, 7]
    [4, 5]
    [2, 6]
    After sorting:
    [1, 7]
    [2, 6]
    [4, 5]


##### We can also define a key function passed to sort() to define how to sort 


```python
# sort by the right element 
def interval_key(interval):
    return interval.right
A.sort(key = interval_key)
for i in A:
    print('[{}, {}]'.format(i.left, i.right))

```

    [4, 5]
    [2, 6]
    [1, 7]


## Input and Output 

* Input from user

* Input from files using `open`

* Use `pickle` to store _any_ Python object in a file and then get it back later


```python
# input from user example 
# reverse a string 
def reverse(string):
    return string[::-1]
reverse('niu')
```




    'uin'




```python
def is_palindrome(string):
    return string == string[::-1]
is_palindrome('wow')
```




    True



### Input from files 

* `open` with read mode `r`, write mode `w`, append mode `a`, text file mode `t` or binary mode `b` 


```python
sentence = r'''I like Python as 
            it's fast and simple'''
sentence
# write it into a file 
f = open('inputexample.txt', 'w') # open for writing 
f.write(sentence) # write sentence into inputexample.txt 
f.close() # close the file 
```


```python
# read the file 

sentence = open('inputexample.txt')  # 'r' mode by default
sentence 
```




    <_io.TextIOWrapper name='inputexample.txt' mode='r' encoding='UTF-8'>




```python
# access the file with readline()
while True: 
    line = sentence.readline()
    if len(line) == 0:
        break 
    print(line, end = '') # end = '' suppress the automatic new line of each print 
sentence.close()
```

    I like Python as 
                it's fast and simple

#### `pickle`

* `pickle.dump(f1, f2)` dumps f1 into f2
* `pickle.load(f2)` loads f2 


```python
import pickle 
stored_file = 'stored.data'
# file to be stored 
shoplist = ['apple', 'orange', 'banana', 'coke']

# write shoplist to stored_file 
f = open(stored_file, 'wb')
pickle.dump(shoplist, f)
f.close()

del shoplist 

# read from storage 
f = open(stored_file, 'rb')
shoplist = pickle.load(f)
print(shoplist)
```

    ['apple', 'orange', 'banana', 'coke']


### Exceptions 
* Use `try` ... `except` 

* `raise` statement 

* `try`...`finally`, useful when you want to ensure that a file object is closed properly event there are exceptions raised. 

* Use `with` to do the `try`...`finally` in a cleaner way.


```python
# try ... except 
try:
    text = input('Enter a color: ')
except EOFError:
    print('Nothing was entered.')
except KeyboardInterrupt:
    print('Operation was canceld.')
else:
    print('You entered {0}'.format(text))
```

    Enter a color: red
    You entered red



```python
# raise statement 

# create personalized exception class 
class ShortInputException(Exception):
    def __init__(self, length, atleast):
        Exception.__init__(self)
        self.length = length
        self.atleast = atleast 
try:
    text = input('Enter a color:')
    if len(text) < 3:
        raise ShortInputException(len(text), 3)
except EOFError:
    print('Nothing was entered')
except ShortInputException as ex:
    print('Input was too short: {0}'.format(ex.length))
else: 
    print('No exception was raised.')

```

    Enter a color:we
    Input was too short: 2



```python
# try... finally 
import time 
try:
    f = open('inputexample.txt')
    while True:
        line = f.readline()
        if len(line) == 0:
            break
        print(line, end = '')
        time.sleep(1)
except KeyboardInterrupt:
    print("Reading of the file was cancelld.")
finally:
    f.close()
    print('\n File closed.')
```

    I like Python as 
                it's fast and simple
     File closed.



```python
# use with statement 
from contextlib import contextmanager 
@contextmanager 
def opened(filename, mode = 'r'):
    f = open(filename, mode)
    try:
        yield f
    finally:
        f.close()
# now open the file with 'with'
with opened('inputexample.txt') as f:
    for line in f:
        print(line, end = '')
```

    I like Python as 
                it's fast and simple
