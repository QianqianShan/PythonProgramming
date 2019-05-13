
## Debugging

* Use `try` ... `except` 

* `raise` statement 

* `try`...`finally`, useful when you want to ensure that a file object is closed properly event there are exceptions raised. 

* Use `with` to do the `try`...`finally` in a cleaner way.

* Use `assert` to insert debugging assertions into a program (https://docs.python.org/3/reference/simple_stmts.html#the-assert-statement)

* User `logging` module

### `try` ... `except` 


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

### `raise` statement 


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

###  `try`...`finally`


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

### `with`


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

### `assert`


```python
open_status = 'open'
# expression , a string to display when expression is False 
assert open_status == 'open', 'The status needs to be "open"'

```


```python
# AssertionError is raised
open_status = 'close'
assert open_status == 'open', 'The status needs to be "open"'
```


    ---------------------------------------------------------------------------

    AssertionError                            Traceback (most recent call last)

    <ipython-input-9-76538a26f503> in <module>
          1 open_status = 'close'
    ----> 2 assert open_status == 'open', 'The status needs to be "open"'
    

    AssertionError: The status needs to be "open"


### `logging` module 

Advantages are:

* Easy to see timestemp of each message 

* Can set different levels of importance of messages 

* Can find or remove the log messages without manually cleaning all statements from code 

* Can conveniently save the log messages to a file 



```python
import logging 
# create a LogRecord object 
logging.basicConfig(level = logging.DEBUG, format = ' %(asctime)s - %(levelname)s - %(message)s')

# call debug function
logging.debug('Start of program')

def factorial(n):
    logging.debug('Start of factorial (%s%%)' % (n))
    total = 1 
    for i in range(n + 1):
        total *= i 
        logging.debug('i is ' + str(i) + ' total is ' + str(total))
    logging.debug('End of factorial (%s%%)' % (n))
    return total 
print(factorial(5))

logging.debug('End of program')

```

     2019-05-13 01:09:50,798 - DEBUG - Start of program
     2019-05-13 01:09:50,800 - DEBUG - Start of factorial (5%)
     2019-05-13 01:09:50,801 - DEBUG - i is 0 total is 0
     2019-05-13 01:09:50,802 - DEBUG - i is 1 total is 0
     2019-05-13 01:09:50,804 - DEBUG - i is 2 total is 0
     2019-05-13 01:09:50,805 - DEBUG - i is 3 total is 0
     2019-05-13 01:09:50,806 - DEBUG - i is 4 total is 0
     2019-05-13 01:09:50,806 - DEBUG - i is 5 total is 0
     2019-05-13 01:09:50,807 - DEBUG - End of factorial (5%)
     2019-05-13 01:09:50,808 - DEBUG - End of program


    0



```python
# disable the debug 
import logging 
# create a LogRecord object 
logging.basicConfig(level = logging.DEBUG, format = ' %(asctime)s - %(levelname)s - %(message)s')

# disable all logging on critical level or lower (critical is the highest level)
logging.disable(logging.CRITICAL)

# call debug function
logging.debug('Start of program')

def factorial(n):
    logging.debug('Start of factorial (%s%%)' % (n))
    total = 1 
    for i in range(n + 1):
        total *= i 
        logging.debug('i is ' + str(i) + ' total is ' + str(total))
    logging.debug('End of factorial (%s%%)' % (n))
    return total 
print(factorial(5))

logging.debug('End of program')

```

    0



```python
# write debug contents to a file 
import logging 
# create a LogRecord object 
logging.basicConfig(filename = 'debugfile.txt',level = logging.DEBUG, format = ' %(asctime)s - %(levelname)s - %(message)s')

# call debug function
logging.debug('Start of program')
def factorial(n):
    logging.debug('Start of factorial (%s%%)' % (n))
    total = 1 
    for i in range(n + 1):
        total *= i 
        logging.debug('i is ' + str(i) + ' total is ' + str(total))
    logging.debug('End of factorial (%s%%)' % (n))
    return total 
print(factorial(5))

logging.debug('End of program')
```

     2019-05-13 01:21:13,234 - DEBUG - Start of program
     2019-05-13 01:21:13,246 - DEBUG - Start of factorial (5%)
     2019-05-13 01:21:13,247 - DEBUG - i is 0 total is 0
     2019-05-13 01:21:13,249 - DEBUG - i is 1 total is 0
     2019-05-13 01:21:13,250 - DEBUG - i is 2 total is 0
     2019-05-13 01:21:13,252 - DEBUG - i is 3 total is 0
     2019-05-13 01:21:13,254 - DEBUG - i is 4 total is 0
     2019-05-13 01:21:13,259 - DEBUG - i is 5 total is 0
     2019-05-13 01:21:13,261 - DEBUG - End of factorial (5%)
     2019-05-13 01:21:13,263 - DEBUG - End of program


    0

