---
layout: post
title: '# Iterators'
tags:
  - design-patterns
  - iterators
  - oop
  - python
  - tutorial

---

I got the <a href="http://www.amazon.com/Design-Patterns-Object-Oriented-Addison-Wesley-Professional/dp/0201633612/ref=pd_bbs_sr_1?ie=UTF8&amp;s=books&amp;qid=1234297499&amp;sr=8-1">Gang of Four</a> book on design patterns a couple of years ago and it was way beyond me (Alex Martelli at Google doesn't suggest it as an introduction, I've since learned). I still haven't mastered it, but every now and then I do find a useful idea.

Let me introduce you to the object-oriented idea of iterators.

<!--more--><h3>Concept</h3>

The iterators I'll demonstrate here are pretty simple, and could easy be done using simple expressions (for instance, <code>k++</code> or <code>k += 2</code>) but more complex iterators would be difficult using this method. Sometimes it is necessary to have an entire routine determine the next value.

If you're not sure what I mean, read on. It'll become clearer with some examples.

<h3>Iterators as a Class</h3>

Suppose we want to re-invent the wheel for <code>k += 1</code>. Here's a class that does just that.

<pre>class CountingIterator:
    def __init__(self):
        # Initialize the value we'll be using.
        self._k = 0

    def next(self):
        # Return the next value when this method is called.
        self._k += 1
        return self._k</pre>

This class would get used like this:

<pre>&gt;&gt;&gt; simple_iterator = CountingIterator()
&gt;&gt;&gt; simple_iterator.next()
1
&gt;&gt;&gt; simple_iterator.next()
2
&gt;&gt;&gt; simple_iterator.next()
3</pre>

It seems simple, I know, but this structure lets more complicated iterations be done. Suppose you don't want to count indefinitely. Instead, maybe, you want to loop indefinitely. For instance, let's make an iterator that will cycle through a set of colors.

<pre>class LoopingIterator:
    def __init__(self, color_list):
        self._color_list = color_list
        self._k = -1

    def next(self):
        self._k += 1
        self._k %= len(self._color_list)
        return self._color_list[self._k]</pre>

This is a little more complex, but it's not too bad. The <code>__init__</code> method initializes a list of colors and sets <code>_k</code> to -1. Then, when <code>next()</code> is called, <code>_k</code> is incremented. The <code>%=</code> operator finds the remainder when the value on the left is divided by the value on the right, then assigns that value to the variable on the left. In other words, we don't want the third line in <code>next()</code> to try and get an out of bounds index in the list, so we use the mod operator to reduce the value of <code>_k</code>.

This iterator would be used like this.

<pre>&gt;&gt;&gt; colors_iterator = LoopingIterator(['red','green','blue'])
&gt;&gt;&gt; colors_iterator.next()
red
&gt;&gt;&gt; colors_iterator.next()
green
&gt;&gt;&gt; colors_iterator.next()
blue
&gt;&gt;&gt; colors_iterator.next()
red</pre>

Clearly the <code>next()</code> method can be written for whatever purpose suits your needs. These two examples are very simple, but more complex iterators can be made using this method. In fact, other methods can be added such as <code>previous()</code> or <code>skip()</code>. That is what makes the iterator design pattern so powerful.

In Python, custom iterators like this can be made for use in <code>for</code> loops. In other words, rather than simply iterating over entries in a list, something more interesting can be made. I'll cover that, though, in another post.

<h3>Iterators in Python</h3>

The examples above can be achieved in Python using the <code>yield</code> statement in a function definition. Some of the advanced functions of iterators are not available (such as the hypothetical <code>previous()</code> and <code>skip()</code>), but it works quite well for the <code>next()</code> method.

Rather than declaring a class to do this, we'll only have a function, but it will do the same things. Here it is for the first example.

<pre>def CountingIterator():
    k = 0
    while True:
        k += 1
        yield k</pre>

When the iterator is initialized, it sets <code>k</code> equal to 0, then goes into an infinite loop. When the <code>next()</code> method is called, it returns the value of <code>k</code> at the <code>yield</code> statement, then goes through another iteration. When it reaches <code>yield</code> again, it waits until <code>next()</code> is called, then returns that value and goes through another iteration.

The second example from above looks like this.

<pre>def LoopingIterator(list):
    k = -1
    while True:
        k += 1
        k %= len(list)
        yield list[k]</pre>

That's all there is to it.

<h3>Conclusion</h3>

Iterators are powerful things, especially in Python where there is a built-in <code>__iter__()</code> method. They can be very useful in <code>for</code> loops if one knows how to use them, but I'll wait to think of a good tutorial example before I go into that.
