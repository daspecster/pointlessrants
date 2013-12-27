---
layout: post
title: '# Function/Method Decorators'
tags:
  - decorators
  - design-patterns
  - python
  - pythonic-programming
  - tutorial

---

One of the reasons I like Python is because it's simple but powerful. All the tools are there for whatever task needs to be done. I've found <code>__getattr__</code> to be a very useful tool for creating sets of standardized class methods without having to explicitly declare them. Another useful tool is function decorators. Read on to get a quick idea of how to make your own class decorators.

<!--more--><h3>@</h3>

Function decorators are simply functions that take as their argument another function. They are a little tricky to construct, but if you're familiar with passing functions around as variables, it will be fairly easy to understand.

Here is a simple function that prints the name of the function it decorates:

<pre>def give_name(func):
    print "My name is", func.__name__
    return func</pre>

To make this function decorate another function, use the <code>@</code> operator before the function definition.

<pre>@give_name
def a_function(data):
    print data</pre>

When you call <code>a_function</code>, it really calls <code>give_name</code> because the <code>@</code> function decorates the function that is actually called. When you call <code>give_name</code>, it prints the name of the <code>func</code> variable then returns <code>func</code>. The function that was passed into <code>give_name</code> was <code>a_function</code>, because that was the function definition that came immediately after <code>@give_name</code>, the decorator.

<h3>Why?</h3>

You might be wondering why anyone would ever want to do something so convoluted. In this case, you can add a single line above a function definition if you want it to print its name when it is run. You can add the same decorator to as many functions as you want. When you call the function, they'll display their name, then run. This is especially helpful for debugging, such as when the programmer wants to see whether a function is actually being called anywhere.

I've found a lot of use for another decorator that I call <code>time_this</code>, a form of the <code>benchmark</code> decorator found <a href="http://omar.flatcloud.co.uk/index.php/2008/05/19/a-morsel-of-python/">here</a>. The code is below.

<pre>import time

def time_this(func):
    def wrapper(*args):
        t1 = time.clock()
        result = func(*args)
        t2 = time.clock()

        print("%s: %0.3f ms" %(func.__name__, (t2-t1)*1000.0))
        return result

    return wrapper</code></pre>

If I want to time the performance of a function, I just have to add <code>@time_this</code> before the function definition. Then whenever that function is called, the amount of time it takes running is printed out. This helped me identify some key bottlenecks in a simulation I wrote for a research project. In the end I was able to cut the running time to a third of what it was.

See if you can figure out what happens when this decorator is used like this:

<pre>@time_this
def a_function():
    for i in range(100):
        print i</pre>

If you have any questions, feel free to ask in the comments!
