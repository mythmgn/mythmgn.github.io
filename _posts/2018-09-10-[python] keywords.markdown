---
layout: post
title: Python keywords
categories: Programming
tags: python, keywords
---

[TOC]

# 1.\__xx__ #

## \__repr__ ##

My rule of thumb: __repr__ is for developers, __str__ is for customers.


## \__future__ ##
division
absolute_import




## \__getstate\__ / \__setstate__ ##
object._\___getstate\_\_()
Classes can further influence how their instances are pickled; if the class defines the method _\__getstate__(), it is called and the returned object is pickled as the contents for the instance, instead of the contents of the instance’s dictionary. If the \__getstate__() method is absent, the instance’s \__dict__ is pickled as usual.
object.*__setstate__*(state)¶
Upon unpickling, if the class defines __setstate__(), it is called with the unpickled state. In that case, there is no requirement for the state object to be a dictionary. Otherwise, the pickled state must be a dictionary and its items are assigned to the new instance’s dictionary.
Note
If __getstate__() returns a false value, the __setstate__() method will not be called upon unpickling.


## \__getattribute__ / __getattr__ ##

__getattribute__ is invoked before looking at the actual attributes on the object, and so can be tricky to implement correctly.  You can end up in infinite recursions very easily.
New-style classes derive from object, old-style classes are those in Python 2.x with no explicit base class.  But the distinction between old-style and new-style classes is not the important one when choosing between __getattr__ and __getattribute__.

# 2. Algorithm functions #
## all / any ##


# 3. Python features #
## 3.1 yield ##
*  a lot more memory efficient and faster too
*
Note that a for loop doesn't know what kind of object it's dealing with - it just follows the iterator protocol, and is happy to get item after item as it calls next(). Built-in lists return their items one by one, dictionaries return the keys one by one, files return the lines one by one, etc. And generators return... well that's where yield comes in:

```python
def f123():
        yield 1
        yield 2
        yield 3for item in f123():
        print item
```
Instead of yield statements, if you had three return statements in f123() only the first would get executed, and the function would exit. But f123() is no ordinary function. When f123() is called, itdoes not return any of the values in the yield statements! It returns a generator object. Also, the function does not really exit - it goes into a suspended state. When the for loop tries to loop over the generator object, the function resumes from its suspended state, runs until the next yield statement and returns that as the next item. This happens until the function exits, at which point the generator raisesStopIteration, and the loop exits.
So the generator object is sort of like an adapter - at one end it exhibits the iterator protocol, by exposing__iter__() and next() methods to keep the for loop happy. At the other end however, it runs the function just enough to get the next value out of it, and puts it back in suspended mode.

## 3.2 lambda ##

lambda is just a fancy way of saying function. Other than its name, there is nothing obscure, intimidating or cryptic about it. When you read the following line, replace lambda by function in your mind:

a. list lambda
mult3 = [x for x in [1, 2, 3, 4, 5, 6, 7, 8, 9] if x % 3 == 0]

b. function lambda

f = lambda x: x**2 + 2*x - 5
