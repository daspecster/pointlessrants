---
layout: post
title: 'Setting up for Python development in Ubuntu'
tags:
  - balthasar
  - development
  - gedit
  - graphics
  - libraries
  - packages
  - python
  - pythonpath
  - sys
  - terminal
  - ubuntu
  - windows

---

I've been working on a <a href="http://code.google.com/p/balthasar/">Python graphics library</a> and trying to do some development in Ubuntu. It wasn't going well, and most of the development took place on Windows XP. Much of the difficulty in Ubuntu was trying to make Python see the library as an installed library. To do that in Windows, I merely put the code in <code>C:\Python26\lib\site-packages\balthasar</code>, but trying to do the equivalent in Ubuntu with the <code>dist-packages</code> folder was a mess and, I gathered, a really bad idea altogether.

Fortunately, there is a simple way to edit the <code>.bashrc</code> file in Ubuntu to add a home directory folder to Python's search path. <!--more--> Open up <code>.bashrc</code> in a text editor and add the following lines:

<pre>PYTHONPATH=$HOME/Python/lib
EDITOR=gedit
export PYTHONPATH EDITOR</pre>

<code>$HOME</code>, for me, is the folder <code>/home/eric</code>, so the <code>Python</code> folder is right in the main working directory. I've put the code for Balthasar in a subdirectory named <code>lib</code>. Now I can run examples that import <code>balthasar</code> from anywhere and they know where to look.

To verify that this worked, open the terminal and start the Python interpreter with <code>python</code>. Then type

<pre>>>> import sys
>>> sys.path</pre>

The list that prints out shows all the places Python looks for packages when <code>import</code> is used. The second item for me is <code>/home/eric/Python/lib</code>, meaning this folder will work for putting work-in-progress libraries in.
