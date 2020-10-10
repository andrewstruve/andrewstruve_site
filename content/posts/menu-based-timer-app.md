---
title: "Menu Based Timer App"
date: 2020-10-04T17:07:09-04:00
draft: false
tags: ["menu-based", "timer", "python"]
---
A common type of app that is always useful is a menu app. We can create a command line 
application that stays open and we can interact with it. I have used menu based apps to 
turn on and off pins on a microcontroller.

We will use python for this application.

Lets create a menu that does the following things:
- Set a Start Time (0)
- Get Time Elasped Since Start Time (1)
- Get Current time (2)
- Exit (3)

First we start with declaring our dependencies.

We will need to use the time and sys libraries.
```
import sys
import time
```

Lets create the menu using a multi-line print:
- https://pythonprogramming.net/multi-line-printing-python-3/

```
print('''
- Set a Start Time (0)
- Get Time Elasped Since Start Time (1)
- Get Current time (2)
- Exit (3) 
''')
```

We will need 2 variables, start_time, and elapsed_time.

``` 
start_time = time.time()
elapsed_time = 0.0
```

To keep the application from dieing, everything will be enclosed in a while 
```
while True:
```

Use the input method to get input from the keyboard. Press enter after a selection is made.
```
text = input("")
```

The above code stores whatever we enter into text as a string. we can then use if blocks to 
execute code based on what we enter. 

```
text = input("")
if ( text == '0'):
    print("0 was entered")
if ( text == '1')
    print("1 was entered")
if ( text == '2')
    print(" 2 was entered")
if ( text == '3')
    print("3 was entered")
```

Our Input is a number between 0 and 3. All other characters mean nothing to us. 

- Entering 0 sets the start_time to the current time at the moment 0 is pressed
- Entering 1 calculates the difference between current time and the past
- Entering 2 shows us the current time value.
- Entering 3 exits this application.

Lets Explore ways to exit this app:
- https://www.geeksforgeeks.org/python-exit-commands-quit-exit-sys-exit-and-os-_exit/

I like sys.exit() as it will exit cleanly and print out a message if we choose to pass a message parameter.

In this case we could easily just use 'break' to exit as well.

The final code is:
```
import sys
import time

print('''
- Set a Start Time (0)
- Get Time Elasped Since Start Time (1)
- Get Current time (2)
- Exit (3) 
''')

start_time = time.time()
elapsed_time = 0.0

while True:
    text = input("") 
    if (text == '0'):
        start_time = time.time()
        print('start_time = '+ str(start_time))
    if (text == '1'):
        elapsed_time = time.time() - start_time
        print('Time Since Start Time:' + str(elapsed_time))
    if (text == '2'):
        cur_time = time.time()
        print(cur_time)
    if (text == '3'):
        sys.exit('exiting app')

```
Example Execution
```
[andrew@localhost menu-based-timer-app]$ python3 menu-based-timer-app.py 

- Set a Start Time (0)
- Get Time Elasped Since Start Time (1)
- Get Current time (2)
- Exit (3) 

0
start_time = 1602342431.9504595
1
Time Since Start Time:4.488875865936279
1
Time Since Start Time:6.254856586456299
0
start_time = 1602342442.3718617
1
Time Since Start Time:1.9416639804840088
1
Time Since Start Time:3.6616978645324707
2
1602342448.1476638
3
exiting app
```