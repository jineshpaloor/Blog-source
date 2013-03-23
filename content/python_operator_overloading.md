Title: Operator overloading in Python
Date: 2013-03-21 10:20
Tags: python, Operator overloading
Category: Python, Programming
Slug: operator-overloading-in-python
Author: Jinesh
Summary: How to do operator overloading in Python

Very recently my friend Hari wrote an article about operator overloading in ruby, and he asked me to implement the same program which he used in his article in python. His aim was to compare the two hottest languages of technology lovers.

Though our example is very simple and straight forward, we consider this as a stepping stone for our comparative study. Below we are giving our example which compares the operator overloading for ‘+’ (addition).
I expect you know about operator overloading. If you dont know, in simple words, it is just like giving special meaning to a language’s operators(‘+’, ‘-’,'/’,'*’ etc) via new definition though class methods.Read more about operator overloading from here.
In python, operator overloading is achieved via overriding python’s special methods from a python class. If you want to do operator overloading in python you should know about it’s special methods ( which is also called magic methods). Python has a number of special methods, which should be of the form __xxx__. The list is very big, but most commonly used ones are, __add__, __sub__, __repr__, __str__, __len__, __gt__, __lt__ etc. you will get the complete list from here.
lets see how we can give special meaning to `__add___`. I hope you should be knowing that we cant add two objects, we can add only two numbers. In python you can use ‘+’ to append two strings too. But look how we can add special meaning to ‘+’ to add two objects.

    :::identifier
    class Add(object):
        def __init__(self, val):
            self.val = val
    
        def __add__(self, obj):
            return self.val + obj.val
    
    a = Add(10)
    b = Add(20)
    
    print a + b

as you expect this will print 30. In order to understand how this works, you can read the print statement like this.  `print a.__add__(b)`

    :::identifier
    a = Add('Hello')
    b = Add(' World')
    print a + b   #This will print 'Hello World'.
 
The above examples are straight forward use of  ’+’ operator. We can further extend our __add__ method to intelligently add different data types. Normally python wont allow to add different datatypes. ( try some examples on your python shell)
Here is our extended __add__  method. And see the examples.

    :::identifier
    class Add(object):
        def __init__(self, val):
            self.val = val
    
        def __add__(self, obj):
            if isinstance(self.val, str) or isinstance(obj.val, str):
                return str(self.val) + str(obj.val)
            return self.val + obj.val
    
    a = Add(10)
    b = Add(20)
    
    print a + b  #30
    
    c = Add('Hello')
    d = Add(' World')
    
    print c + d  # Hello world
    
    e = Add(5)
    f = Add(' is my number.')
    
    print e + f  # 5 is my number
 
In the above definition of __add__ we are checking whether any of the value is a string, if then we will append the two values, otherwise add the values.
