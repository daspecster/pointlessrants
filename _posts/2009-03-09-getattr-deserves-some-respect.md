---
layout: post
title: '# __getattr__ Deserves Some Respect'
tags:
  - design-patterns
  - getattr
  - python
  - pythonic-programming
  - pythonista
  - tutorials

---

One of Python's built-in functions is <code>__getattr__</code>, which turns out to be quite useful but at the same time slightly dangerous. It is especially helpful for creating complex classes without using inheritance. For a brief tutorial, read on.

<!--more--><code>__getattr__</code> is a built-in class function just like <code>__init__</code>. It takes two parameters: an object (self, naturally) and a string representing an attribute. It looks like this when it is declared:

<pre>def __getattr__(self, attr):</pre>

For example, calling <code>an_instance.name</code> is the same as calling <code>an_instance.__getattr__('name')</code>. Remember, the object's instance is passed as the hidden first parameter; 'name' is the <code>attr</code> parameter passed into the method. (There is a related function, <code>getattr</code>, which would do the same thing with the code <code>getattr(an_instance, 'name')</code>.)

<h3>The Design Pattern</h3>

Pythonistas are somewhat particular about how the way things look, even when it doesn't seem like there is any other way to do something. For instance, suppose you have a class with an attribute that is another class instance, something like <code>parent.child</code>. If you want to access a method of of <code>child</code>, you would typically call <code>parent.child.method()</code>. Pythoneers often consider this ugly, and would much rather prefer to use <code>parent.method()</code> if such a thing were possible. Thanks to the <code>__getattr__</code> method, it is possible. Here's how.

<pre>class Parent:
    def __init__(self, child):
        self.child = child

class Child:
    def make_statement(self):
        print("I am an instance of Child.")

kid = Child()
person = Parent(kid)</pre>

If we wanted the child to make a statement, we would have to call <code>person.kid.make_statement()</code>. If we wanted instead to call <code>person.make_statement()</code>, we could modify the Parent class as follows:

<pre>class Parent:
    def __init__(self, child):
        self.child = child

    def __getattr__(self, attr):
        if hasattr(self.child, attr):
            return getattr(self.child, attr)
        else:
            raise AttributeError(attr)</pre>

There are a few things here to explain. First, <code>hasattr</code> works like <code>getattr</code>. The first argument is a class instance and the second is a string. <code>hasattr</code> tests whether or not an instance has <code>attr</code> as an attribute. <code>getattr</code>, as mentioned above, returns the attribute rather than merely testing for its existence.

(It is important to add the else clause when using <code>__getattr__</code>. Leaving it off tends to cause a NoneType error. It is probably good practice anyway, regardless of whether or not it causes an error.)

<code>make_statement()</code> can now be called using

<pre>person.make_statement()</pre>

This example demonstrates what can be done with <code>__getattr__</code>. The advantage of this Python feature is that classes can have children whose methods and attributes are accessible to the parent. It accomplishes the same thing as inheritance, even though it reverses the terminology. The advantage over inheritance is that some attributes could be blocked. For instance, suppose we modified the above <code>__getattr__</code> method to be

<pre>def __getattr__(self, attr):
    if hasattr(self.child, attr) and attr in list_of_valid_child_attrs:
        return getattr(self.child, attr)
    else:
        raise AttributeError(attr)</pre>

Now <code>__getattr__</code> makes sure that the child has the attribute and that the attribute is in a list of attributes it is allowed to access.

<h3>The Danger</h3>

Python only calls <code>__getattr__</code> when it is unable to find the attribute declared anywhere. In fact, from what I've been able to figure out, the bytecode compiler goes over the code and if a call is made to an unknown attribute, Python determines once and for all what to do based on the <code>__getattr__</code> method. In other words, <code>__getattr__</code> is static. Changes during runtime are not reflected.

The real trouble you can get into (and it's minor trouble) is infinite recursion. Suppose I had mispelled 'self.child' in the last example. Instead of calling <code>hasattr(self.child, attr)</code>, suppose I called <code>hasattr(self.chil, attr)</code>. As Python evaluates the <code>__getattr__</code> function, it finds a call to an attribute it is not familiar with (namely, 'chil'). To find out what to do with that it calls <code>__getattr__</code>, where it finds an unknown attribute again, and it repeats <i>ad infinitum</i>.

In this case, the problem is easy to solve (i.e., fix the typo). Other times you might want to do something a bit trickier, and that requires a different solution. Until you encounter that problem, however, have some fun with interrelating classes using children and the <code>__getattr__</code> method.
