---
layout: post
title: 'Functional Programming in Python'
tags:
  - functional-programming
  - python
  - wikipedia

---

Way back in the <a href="http://www.daspecster.com/2009/01/episode-0/">0th Episode</a>, Steve talked about functional programming languages, specifically Scheme. Curious, I checked out <a href="http://en.wikipedia.org/wiki/Functional_programming#Coding_styles">Tom's favorite resource</a> to learn more. What do you know, but there's a Python example. And I thought I would have to change languages in order to parallelize better. Chalk one up for PHP/Python/Ruby, Dr. V.

In the spirit of infecting other people with the Python bug, let me explain the Wikipedia example a little. There are some tricks in Python that seem a little cryptic at times, and six months ago this would have been one of them for me. For those of you still learning Python (or those of you sticking to Curly Brackets instead of adopting the Whitespace Rules), here's an explanation of what's going on.

<!--more-->Here's the example Wikipedia gives. Suppose you want to do something like apply two functions/methods/routines to every element in a list. For those of you who are doing math-related functions, let's call those functions <em>F</em> and <em>G</em>, and let's call the list <em>x</em>.If you're math-aware, you might recognize the notation <em>F(G(x))</em>. In other words, we're going to apply the function <em>G</em> to every element in <em>x</em> and get a new list back. Then we're going to apply the function <em>F</em> to every element in the new list and get an even newer list back.

If you wanted to do this the standard way, it would work like this (in Python):
<pre>result = []  <em># This is a new empty list.</em>
for value in x: <em># Loop through the elements in the list x.</em>
    first_result = G(value)  <em># Get the G(x)</em>
    second_result = F(first_result)  <em># Get F(G(x))</em>
    result.append(second_result)  <em># Add the result to the list of results.</em></pre>

While this works, it could be more succinct. There are two pythonic ways to do this. One uses syntactic sugar (list comprehensions), and one uses something a bit more complex that does it the way function programming languages do. Since this post is about functional programming, we'll focus on that one.
<pre>composition = lambda F, G: lambda x: F(G(x))
result = map(composition(F, G), x)</pre>

That's it. If you know something about lambda functions in Python, it's not too bad. If you're not familiar with lambda functions, let me try to clear things up a bit.

A lambda function is an anonymous function that only has one line of code and returns something.  For instance, I could write,
<pre>def func(x):
    return 2*x</pre>
or, using a lambda function, I could write,
<pre>func = lambda x: 2*x</pre>
Lambda functions let the programmer define all sorts of simple functions without cluttering up the code with function definitions. They don't even have to be stored as a variable.

To demonstrate, let's skip ahead a little and look at the <i>map</i> function. <i>map</i> takes two arguments: a function, and a list (or tuple). <i>map</i> takes each element from the list, runs it through the function, and returns a list containing all the results. For instance,
<pre>doubled_values = map(func, x)</pre>
This creates a list called <i>doubled_values</i>. The <i>map</i> function takes each element in <i>x</i> and runs it through the function <i>func</i> (remember the function definitions above). Since <i>func</i> returns two times the input value, each element in <i>doubled_values</i> is two times the corresponding element in <i>x</i>.

Now that you know how the <i>map</i> function works, let's rewrite it simpler. If you only need <i>func</i> this one time, it doesn't make a lot of sense to have that lingering function definition in the code. Instead, you can write it like this:
<pre>doubled_values = map(lambda a: 2*a, x)</pre>

This defines a function with a parameter <i>a</i> that returns 2*<i>a</i>. That becomes the function that <i>map</i> runs every value of <i>x</i> through in order to produce <i>doubled_values</i>.

Let's take another look at our functional programming example.
<pre>composition = lambda F, G: lambda x: F(G(x))
result = map(composition(F, G), x)</pre>

This creates the variable <i>composition</i> and stores in it a function in terms of <i>F</i> and <i>G</i>. <i>composition(F, G)</i> is in turn a function of <i>x</i>. Thus, if you were going to call <i>composition</i> for some specific value of <i>x</i>, say 2, you would write
<pre>composition(F,G)(2)</pre>
This works because <i>composition(F,G)</i> is a function, and functions can be called.

This makes the second line of our example a little clearer. <i>map</i> is passing each element of <i>x</i> through the function <i>composition(F,G)</i> and storing the outputs in <i>result</i>.

The trickiest part of this is understanding the lambda functions. The great thing is that lambda functions can easily be experimented with in Python's interactive mode. Just open up the interactive interpreter and play around with it. Here is an example of what you can do based on this tutorial.

<pre>&gt;&gt;&gt; x = [1,2,3,4,5]
&gt;&gt;&gt; F = lambda x: 2*x
&gt;&gt;&gt; G = lambda x: x**2
&gt;&gt;&gt; composition = lambda A, B: lambda x: A(B(x))
&gt;&gt;&gt; result = map(composition(F,G), x)
&gt;&gt;&gt; print(result)
[2, 8, 18, 32, 50]</pre>
