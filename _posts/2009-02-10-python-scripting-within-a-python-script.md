---
layout: post
title: 'Python Scripting within a Python Script'
tags:
  - modules
  - programming
  - python
  - pythonic-programming
  - scripting
  - tutorial

---

<b>UPDATE:</b> In order to use <code>reload</code> in Python 3, it must be imported from the <code>imp</code> built-in module. Thus, some of the examples below will require the line <code>from imp import reload</code> in order to work in Python 3.

I've been mulling over an idea for a little while now, but didn't have the chance to do anything with it until today. Turns it it was way easier than I thought it would be. For reasons I won't go into here, I wanted to have a Python program which could write and run other Python programs. Clearly Python can write programs (since it can save text as a .py file), and it can easily run programs just by importing a module. The trouble was editing those files and running the updated code in the master program without having to restart the master program. Here's how I did it.

<!--more--><h3>The Problem</h3>

When the Python interpreter runs a script, it compiles the code into Python bytecode to run on the Python virtual machine. It also compiles all the imported modules. Thus, you cannot change the imported modules at any point and see the changes without stopping the original program and starting it back up again. To demonstrate, try the following. Write a simple script that prints something to the screen.

<pre>print("Test")</pre>

(This is the standard syntax for Python 3, which works in Python 2.5 as well.)

Save this as "test.py". Start Python's interactive mode and do the following.

<pre>&gt;&gt;&gt; import test
Test</pre>

While interactive mode is still running, edit the source file to print something else, for instance, "Cahoots", then save it. Go back to interactive mode and import 'test' again. It will still print out 'Test'.

The reason this happens is because Python makes a dictionary of all the modules that are currently loaded. Since you have already imported the <code>test</code> module, it does not re-import it even when you invoke the <code>import</code> statement.

The simple solution to this is to use the <code>reload</code> function. In this case:
<pre>&gt;&gt;&gt; reload(test)
Cahoots</pre>

<h3>The Deeper Problem and Its Solution</h3>

My problem was that the user gets to specify which program to run. I cannot specify a particular <code>import</code> statement at design time. Fortunately Python has a built-in <code>__import__</code> function which can take a module name as a string and import it. For instance,

<pre>&gt;&gt;&gt; __import__('test')</pre>

This will load the <code>test</code> module just like <code>import test</code> does. But if I change <code>test</code>, I can't use this statement a second time just like I can't use the regular 'import' a second time.

Fortunately, <code>__import__</code> returns the module it imports. That means we can say something like this:

<pre>&gt;&gt;&gt; x = __import__('test')</pre>

This allows us to use the <code>reload</code> statement. When we make a change, all we have to do is invoke 'reload(x)'.

This will let the user import a module at runtime, then make a change to it and re-import it.

<h3>Addendum</h3>

Suppose, however, that one wants to reload a user-specified module without having to store it as a variable. Never fear. Python's system module has a dictionary of all the modules that are currently loaded. Just do the following in interactive mode (or a script file, if you like):

<pre>&gt;&gt;&gt; __import__('test')
Test</pre>

Then change what prints out from 'Test' to 'Cahoots'.

<pre>&gt;&gt;&gt; __import__('test')
Test
&gt;&gt;&gt; import sys
&gt;&gt;&gt; test_module = sys.modules['test']
&gt;&gt;&gt; reload(test_module)
Cahoots</pre>

<code>sys.modules</code> is a dictionary of all the currently loaded modules. If you want, you can call <code>del sys.modules['test']</code>, then simply re-import the <code>test</code> module, but that is a little dangerous and not as transparent as simply reloading the module.
