---
layout: post
title: '# Python Dictionary Coolness'
tags:
  - dictionaries
  - function-definitions
  - python
  - pythonic-programming
  - tricks

---

Lately I've been working with dictionaries, specifically as a device for storing settings. I ran into a little annoyance and thought of programming a little routine to take care of it. Come to find out, Python already has such a routine built into the dictionary class. Read on to find out more.

<!--more--><h3>*args and **kwargs</h3>

Let's suppose I have the following dictionary of settings:

<pre>settings = {
    'left': 100,
    'top': 100,
    'height': 500,
    'width': 500,
}</pre>

I also have a function for changing settings. Let's call it <code>change_settings</code> just to be obvious.

Python functions can handle extra arguments and keyword arguments with just a little function definition trick. For instance, trying to call <code>change_settings(1, 2, 3)</code> when the function definition is <code>def change_settings(number):</code> would be problematic. The function only takes one argument and three were given. If, however, you define the function as <code>def change_settings(number, *args):</code>, the 2 and 3 will be stored as the tuple (2, 3) in the variable <code>args</code>. (<code>args</code> is just the typical name for this variable. In reality it can be anything, though it is not recommended for reasons of transparency.)

The same things can be done with keyword arguments, only instead of using one asterisk, use two. The keyword arguments are stored in a dictionary, where the keyword is a string (one of the keys) and the value is the value for that key. The dictionary is generally called <code>kwargs</code> for 'keyword arguments'. 

The function definition now looks like this:

<pre>def change_settings(number, *args, **kwargs):</pre>

If we make a call such as <code>change_settings(1, 2, 3, 4, color='white', size=400)</code>, the value of <code>number</code> inside the function is 1, the value of <code>args</code> is (2, 3, 4), and the value of <code>kwargs</code> is the dictionary {'color': 'white', 'size': 400}.

<h3>Changing Settings</h3>

Now, if I want to change my default settings, all I have to do is make declare a function as <code>def change_settings(**kwargs):</code>. Then I can call <code>change_settings(left=200, top=30, width=400, height=60)</code>. This is passed into the change_settings function as the dictionary

<pre>kwargs = {
    'left': 200,
    'top': 30,
    'width': 400,
    'height': 60,
}</pre>

Then, to update the settings, all I have to do is set <code>settings</code> equal to <code>kwargs</code>. This, however, will replace the original settings dictionary with the new keyword arguments dictionary, which means that every time I call <code>change_settings</code>, I have to set every single value, and if I don't want some of them to change, I have to set them to be what they were before.

What I would like to do is change only certain values in <code>settings</code> using the keyword arguments dictionary. In other words, if I want to change only the 'width' setting, I want to be able to call <code>change_settings(width=80)</code> without losing all the other settings as well.

One way to do this is to run through all the keys in <code>kwargs</code> and replace the values of <code>settings</code> for those keys with the values in <code>kwargs</code>. The code for this is pretty simple.

<pre>for key in kwargs.keys():
    settings[key] = kwargs[key]</pre>

This is fairly straight forward, but I wanted it to be simpler. A little poking around gave me the solution. Dictionaries have a built-in method which already does this: <code>update</code>. Using the <code>update</code> method, the code above can be accomplished with one line:

<pre>settings.update(kwargs)</pre>

This does the exact same thing as the for loop.

<h3>Conclusion</h3>

This is why I use Python for my everyday programming. It's not only fast and easy, but often there are built-in ways to simplify common tasks.
