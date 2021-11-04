---
layout: post
# hide_title: true
title: __str__ vs __repr__
tags: [python]
---

## Understand what the deal is between `__str__` and `__repr__`.

### Why `__str__`?

Before explaining anything about them, I would prefer to demonstrate the concept via an example.

Let's create a simple class for a dog.

    class Dog:
    	def __init__(self, size, color):
    		self.size = size
    		self.color = color

The class is now instantiated:

    mero_dog = Dog('Small','Brown')

    print(mero_dog)

Result: **<`__main__.Dog` object at `0xXXXXXXXXX`>**

Upon printing this, we don't get much valuable information. We do get the name of the class i.e. 'Dog', the namespace i.e. '`__main__`' or '`__console__`' if printing via python console and the memory location of the object.

So if we add a dunder str method to the class:

    class Dog:
    	def __init__(self, size, color):
    		self.size = size
    		self.color = color

    	def __str__(self):
    		return 'a {self.color} {self.size} dog.'.format(self=self)

And now if we,

    mero_dog = Dog('small','brown')
    print(mero_dog)

We actually get a different output:

    a brown small dog.

It is more sensible than the random output we got before the dunder str method.

However, if the mero_dog object is just inspected on the interpretor without the print statement as:

    mero_dog

The output is similar as before i.e.

**<**console**.Dog object at 0xXXXXXXXXX>**

But, if we forcibly convert the object to the string by `str(mero_dog)`, the output would change to _'a brown small dog'._

If we don't desire to forcibly convert the object to the string `__repr__` method comes to the rescue.

### Why `__repr__`?

Let's make some changes:

    class Dog:
    	def __init__(self, size, color):
    		self.size = size
    		self.color = color

        def __str__(self):
        	return '__str__: a {self.color} {self.size} dog.'.format(self=self)

        def __repr__(self):
        	return '__repr__: a {self.color} {self.size} dog.'.format(self=self)

And now if we,

    mero_dog = Dog('small','brown')

    print(mero_dog)

We get:

    __str__: a brown small dog.

But,
Inspecting the object without printing by:

    mero_dog

We get:

    __repr__: a brown small dog.

### So now we know the differences but...

#### When to use which?

So, by convention `__str__` should be more readable by users whereas `__repr__` should be more informative to developers for internal usage and debugging.

The example of this can be seen on a built-in module:

    import datetime
    today = datetime.date.today()
    str(today)
    # This would return '2021-08-14'

    repr(today)
    # This would return datetime.date(2021,08,14)

### Note: Python calls `__repr__` by default on `str()` as a fallback if `__str__` is not defined.

### Something weird:

Let's say you call `str` method on a container eg: a list, it returns the representation of a `__repr__` method.

Example:

    str([today, today])

returns

    [datetime.date(2021,08,14), datetime.date(2021,08,14)]

which is a little weird but that is how things are.

To solve the issue, you can loop the elements can apply `str` function on all of them individually.

## Thank you for reading!

### References:

Real Python (YouTube)
... and a couple of answers on stack overflow!
